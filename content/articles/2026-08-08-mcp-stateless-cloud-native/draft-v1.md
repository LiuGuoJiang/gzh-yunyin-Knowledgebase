# MCP 删掉 Session 后，Agent 工程开始像真正的分布式系统

把一个远程 MCP Server 从单机扩到三个 Pod，过去很容易遇到这样的情况：

```text
initialize  → Pod A → 返回 Mcp-Session-Id
tools/call  → Pod B → Session Not Found
```

服务本身没有宕机，负载均衡也在正常工作。问题在于，第二次调用没有回到保存 Session 的那台实例。

常见的补丁是开启粘性路由，或者把 Session 搬进 Redis。单机 Demo 里不明显的连接状态，到了 Kubernetes、滚动发布和 Serverless 环境里，就开始和基础设施较劲。

MCP 在 7 月 28 日正式发布的 `2026-07-28` 规范，直接移除了 `initialize` / `initialized` 握手和 `Mcp-Session-Id`。Google 又在 8 月 5 日从云基础设施角度解读了这次调整。

这次变化真正值得注意的，不是少了一个 Header，而是状态责任重新分配了：MCP 删除的是协议层 Session，不是应用状态。

## MCP 到底删掉了什么

旧版 MCP 先通过 `initialize` 协商协议版本和能力。服务端可以返回一个 Session ID，客户端后续请求继续携带它。实现一旦把能力、订阅或中间状态放进某个进程内存，请求就最好回到原来的实例。

新版不再建立这段协议生命周期。每个请求都在 `_meta` 中携带协议版本和客户端能力，客户端身份也建议随请求提供。如果客户端想在调用工具前知道服务端支持什么，可以调用 `server/discover`；但它不是换了名字的强制握手。

普通请求因此不再依赖上一次请求落在哪台机器上。只要实例拥有相同代码、配置和必要的外部依赖，轮询负载均衡就可以把请求交给任意一台。

这里需要纠正一个时间口径。Google 8 月 5 日的文章仍使用 release candidate 和 Beta SDK 的说法，但 `2026-07-28` 已经正式发布。TypeScript、Python、Go、C# 四个 Tier 1 SDK 也已经能使用新协议。规范正式，并不代表所有客户端、框架和扩展已经升级，生产环境仍要看自己的版本分布。

## 为什么它终于更像普通云服务

协议 Session 被拿掉后，最直接的收益出现在基础设施层。

负载均衡不再只为 MCP 会话配置 sticky routing。Pod 重启、横向扩容和滚动发布，也不必为了保住协议 Session 把后续请求送回原实例。对于没有业务状态的工具服务，Serverless 和 scale-to-zero 会更自然。

网关治理也更直接。新版 Streamable HTTP 请求要求带上 `MCP-Protocol-Version`、`Mcp-Method`，调用 Tool、读取 Resource 或获取 Prompt 时还会带 `Mcp-Name`。网关可以根据协议版本、方法和名称做路由、计量、限流与审计，不必先解析完整 JSON-RPC Body。

列表和部分资源结果还增加了 `ttlMs` 与 `cacheScope`。客户端能知道结果多长时间仍然新鲜，以及能否被共享缓存。不过，这只覆盖目录和读取结果，不代表有副作用的 Tool 可以随便缓存。

GitHub MCP Server 已经给出一个真实案例。它在支持新规范时，删除了只为协议 Session 存在的 Redis 读写，网关也不再为了日志和 secret scanning 深度解析每个 Payload。

这个案例有明显边界。GitHub 删除的是协议会话存储，不是宣布 MCP Server 从此不需要 Redis。只要服务仍有浏览器实例、审批任务、作业进度、锁或业务缓存，数据库、队列和 Redis 仍然可能存在。

## 状态没有消失，它只是换了位置

“无状态”最容易被误读成“系统里没有状态”。更准确的说法是：接收方处理一个请求时，不需要依靠前一次传输会话才能理解它。

第一类状态，是协议与授权信息。协议版本和客户端能力回到每个请求里。启用 HTTP 授权时，Bearer Token 也随每个请求发送，服务端逐次验证 token 的 audience 和权限。过去如果只在 `initialize` 做一次授权判断，现在就需要重构。

第二类是业务状态。购物篮、浏览器实例、工作区或代码任务仍然可以跨调用保存，但应由服务端签发明确的 handle，再让模型作为 Tool 参数带回。这个 handle 需要验证所属用户、权限、有效期和并发访问。把 `Mcp-Session-Id` 改名为 `conversation_id`，然后继续承载所有上下文，并没有解决问题。

第三类是交互中间状态。新版用 Multi Round-Trip Requests，也就是 MRTR，替代服务端在持有通道时反向发起的部分请求。服务端先返回 `input_required`，客户端补齐确认或参数，再带着 `inputResponses` 重试原调用。可选的 `requestState` 会经过客户端再返回，所以必须按不可信输入处理。它需要防篡改、限制有效期，并在包含用户数据时绑定原用户。多 Pod 部署还要共享验签或解密配置，否则第一次落在 A、重试落在 B 时，B 可能读不懂这段状态。

第四类是长任务状态。Tasks 已从实验性核心能力移到 `io.modelcontextprotocol/tasks` 扩展。双方都声明支持后，服务端可以返回持久化的 `taskId`，客户端通过 `tasks/get` 轮询，用 `tasks/update` 补充输入，或请求取消。规范统一了任务生命周期，但没有替团队提供任务队列、数据库和 exactly-once 保证。任务必须先持久化，再把句柄交给客户端。

第五类是通知状态。无状态不等于没有 SSE。单个 POST 仍然可以流式返回进度和日志，客户端也能通过 `subscriptions/listen` 打开长时响应流。区别是，这条流不再承担跨请求 Session。多副本要可靠分发订阅通知，仍可能需要共享 Pub/Sub。

## 负载均衡简单了，可靠性问题反而更显眼

新版移除了 SSE Event ID 和 `Last-Event-ID` 断点重放。响应流断开后，客户端要用新的 JSON-RPC 请求 ID 重新发起请求。

这里藏着一个很实际的问题：重试不等于幂等。退款、创建云资源、发通知等 Tool 如果已经产生副作用，第二次调用可能重复执行。JSON-RPC `id` 只负责请求与响应的关联，不能直接拿来当业务幂等键。团队需要自己定义幂等键、唯一约束、重复结果与补偿路径。

标准 HTTP 头也不能被当成信任来源。`Mcp-Method` 和 `Mcp-Name` 方便网关制定策略，后端仍需检查头部与 Body 是否一致，并验证 token、Tool 权限和业务 handle 的归属。

还有故障恢复。普通请求能落到任意 Pod，不等于正在执行的请求会自动转移。流中断需要重试，MRTR 要在另一实例恢复，Task 要在进程退出后继续可查，订阅则要解决跨副本事件分发。它们是四种不同的问题，不能用一句“服务已经无状态”带过。

## 迁移前先做五项检查

第一，先看协议版本分布。记录客户端与 SDK 版本、新版协商成功率和 legacy 回退率。旧客户端仍可能发送 `initialize` 并要求 Session，不能在没有数据时直接拆掉兼容路径。

第二，搜出所有隐式状态。检查 `Mcp-Session-Id`、内存 transport Map、initialize 缓存、连接级能力、GET/SSE 通知和 EventStore 假设。升级不只是删一个 Header，而是找出哪些代码依赖“下一次还会回到这里”。

第三，为有副作用的 Tool 补幂等。按业务定义 idempotency key、去重记录、重复请求返回值和补偿办法，不要把传输层请求 ID 当成业务语义。

第四，做跨实例故障注入。在两轮 MRTR 之间切换 Pod，在 Task 运行中重启 Worker，主动打断响应流并重试，还要验证篡改、过期和跨用户重放的 `requestState` 会被拒绝。

第五，灰度下掉旧设施。先让新旧协议双栈运行，观察 HeaderMismatch、legacy 回退、重复执行和任务恢复失败，再决定何时移除 sticky routing 与 Session Store。

## Agent 工程正在回到分布式系统常识

过去做 MCP Server，很多人把主要精力放在 Tool Schema 和 handler 上。协议进入无状态核心后，真正决定服务能不能进生产的，会是状态机、幂等、请求级授权、任务恢复和可观测性。

MCP 这次拿掉了协议层阻碍云原生部署的一块石头，也让应用层原本含糊的责任暴露出来。它没有替团队解决分布式系统问题，只是让这些问题不再容易藏在一条 Session 后面。

下一次把 MCP Server 扩到三个副本时，不要只看请求能不能被负载均衡。主动让一台实例在请求中途退出，再看系统会不会重复执行、串错用户，或者丢掉一项长任务。

那才是无状态架构真正的验收题。

## 参考资料

1. Model Context Protocol：[The 2026-07-28 Specification](https://blog.modelcontextprotocol.io/posts/2026-07-28/)
2. Model Context Protocol：[Key Changes in 2026-07-28](https://modelcontextprotocol.io/specification/2026-07-28/changelog)
3. Google Developers Blog：[Scaling AI Agent Infrastructure with the MCP Stateless updates](https://developers.googleblog.com/en/scaling-ai-agent-infrastructure-with-the-mcp-stateless-updates/)
4. GitHub Changelog：[GitHub MCP Server supports the next MCP specification](https://github.blog/changelog/2026-07-23-github-mcp-server-supports-the-next-mcp-specification/)
5. Model Context Protocol：[SEP-2575: Make MCP Stateless](https://modelcontextprotocol.io/seps/2575-stateless-mcp)
6. Model Context Protocol：[SEP-2322: Multi Round-Trip Requests](https://modelcontextprotocol.io/seps/2322-MRTR)
7. Model Context Protocol：[MCP Tasks Extension](https://modelcontextprotocol.io/extensions/tasks/overview)
8. Model Context Protocol：[Authorization 2026-07-28](https://modelcontextprotocol.io/specification/2026-07-28/basic/authorization)
9. Model Context Protocol Python SDK：[Deploy & scale](https://py.sdk.modelcontextprotocol.io/run/deploy/)
10. Model Context Protocol：[Conformance Tests](https://github.com/modelcontextprotocol/conformance)
