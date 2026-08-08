# 调研笔记：MCP 删掉 Session 后，Agent 工程开始像真正的分布式系统

> Issue：GST-11
> 目标公众号：AI架构师江小北
> 当前阶段：阶段一｜调研与大纲
> 调研日期：2026-08-08（Asia/Shanghai）

## 一、输入完整性

Issue 已提供完成阶段一所需的关键输入：

- 目标公众号：AI架构师江小北；
- 选题：MCP `2026-07-28` 移除协议层 Session，改用无状态、自包含请求；
- 资讯素材卡：包含发生了什么、工程价值、程序员影响与江小北观点角度；
- 原始来源：Google Developers Blog 与 MCP `2026-07-28` Specification；
- 禁止虚构的边界可从团队规则直接确定：不能写成江小北亲自完成过迁移、压测或生产部署。

Issue 没有提供个人项目经历、实测数据或团队迁移案例。正文只能使用官方案例和明确标注的工程推论。

## 二、先纠正素材卡中的时间状态

素材卡依据 Google 2026-08-05 的文章，沿用了“release candidate”和“四个 Beta SDK”的表述。以当前日期核验，权威状态已经更新：

- MCP 官方于 2026-07-28 正式发布 `2026-07-28` 规范，不再是 RC；
- MCP 正式发布博客写明 TypeScript、Python、Go、C# 四个 Tier 1 SDK 当天都能讲新协议；
- Go SDK 在 7 月 28 日发布稳定版 `v1.7.0`，明确写有 full support；
- Google 文章仍建议在 staging 开始迁移验证。这个建议可以保留，但不能据此把正式规范写成仍处 Beta。

写作口径：

> `2026-07-28` 已是正式规范；SDK 和客户端的升级节奏并不一致，生产迁移仍应先做兼容性盘点与 staging 验证。

证据：S01、S02、S10。

## 三、调研后的核心判断

这次变化不能只写成“删掉一个 Session ID”。真正改变的是状态的归属：

> MCP 不再让传输层会话替应用隐藏状态。协议状态被拆回每个请求，业务状态则必须成为显式句柄、可恢复任务、受保护的 `requestState` 或持久化业务对象。

这会产生两个同时成立的结果：

1. MCP Server 更容易放进普通 HTTP 基础设施：轮询负载均衡、弹性扩缩、滚动发布、Serverless 和网关治理都更直接；
2. 应用不会因此自动变得无状态。重试幂等、授权校验、任务恢复、跨实例通知和状态令牌安全，反而更难继续藏在 SDK 或一条长连接后面。

因此文章主线应是：MCP 的云原生化不是“状态消失”，而是“状态责任显式化”。对 Agent 开发者来说，这是一堂分布式系统基本功补课。

## 四、关键时间线

| 日期 | 事件 | 对本文的意义 |
|---|---|---|
| 2024-11 | MCP 首次推出 | 初始形态更适合本地 `stdio` 和单客户端/单服务端连接 |
| 2025-03-26 | Streamable HTTP 成为远程传输主方向 | 已允许部分无状态实现，但当时协议生命周期仍以 `initialize` 与 Session 为核心 |
| 2025-12-19 | MCP Transports Working Group 公开无状态方向 | 明确指出 sticky session、分布式 Session 存储与故障恢复问题 |
| 2026-05-21 | `2026-07-28` Release Candidate 锁定 | 无状态核心、MRTR、Tasks 扩展等进入验证期 |
| 2026-07-23 | GitHub MCP Server 提前支持新规范 | 删除 Redis Session、避免网关深度解析请求体 |
| 2026-07-28 | `2026-07-28` 正式规范发布 | 移除协议 Session 与初始化握手，Tier 1 SDK 同步支持 |
| 2026-08-05 | Google 发布工程解读 | 从 Google Cloud 的大规模部署视角解释云原生收益与迁移入口 |

证据：S01、S02、S09、S11。

## 五、已经核验的关键事实

### F-01｜`initialize` / `initialized` 握手被移除

在 `2026-07-28` 中，客户端不再先建立一个协议生命周期，再发送工具请求。每个请求在 `_meta` 中携带协议版本和客户端能力，客户端身份为 SHOULD 字段。

服务端必须实现 `server/discover` 来声明支持的版本、能力与身份；客户端可以在第一次业务请求前调用它，也可以直接发送请求。因此它是“服务端必须提供、客户端按需调用”，不能写成新的强制握手。

证据：S02、S03、S04。

### F-02｜`Mcp-Session-Id` 从 Streamable HTTP 中被移除

旧版服务端可在初始化响应中发回 `Mcp-Session-Id`，后续请求携带它。实现通常把 Session 绑定到某个进程或 Pod，扩容时需要粘性路由，或用共享存储保存协议会话。

新规范明确移除协议级 Session 和该请求头。`tools/list`、`resources/list`、`prompts/list` 等列表也不再允许按连接变化。

证据：S03、S04、S06。

### F-03｜“无状态”限定在协议层

官方明确说明，无状态协议上仍然可以构建有状态应用。需要跨调用保存状态时，服务端可以签发显式句柄，例如 `basket_id`、`browser_id`，由模型在后续工具参数中带回。

这类句柄是业务对象引用，不是把旧的 Session ID 换个名字。服务端仍要验证句柄归属、权限、生命周期和并发访问。

证据：S02、S06、S07。

### F-04｜HTTP 头让网关不必解析 JSON-RPC Body

Streamable HTTP POST 现在要求：

- `MCP-Protocol-Version`：协议版本；
- `Mcp-Method`：JSON-RPC 方法；
- `Mcp-Name`：在 `tools/call`、`resources/read`、`prompts/get` 中表示具体名称或 URI；
- 工具还可通过 `x-mcp-header` 把特定原始参数镜像为 `Mcp-Param-*`。

头部值必须与 Body 对应字段一致，不一致时服务端应拒绝请求。网关可以据此路由、计量、限流和审计，但认证授权仍需独立校验，不能因为头部“看起来像某个工具”就信任它。

证据：S03、S05。

### F-05｜列表与资源结果增加缓存提示

`tools/list`、`prompts/list`、`resources/list`、`resources/read`、`resources/templates/list` 等结果包含 `ttlMs` 与 `cacheScope`。客户端可判断多久仍然新鲜，以及是否可在用户间共享缓存。

这改善的是目录与读取结果的缓存治理，不等于所有工具调用都可以缓存。

证据：S02、S04。

### F-06｜MRTR 把中途补充信息改造成“返回—重试”

旧模式下，服务端可能在处理期间向客户端发起 `elicitation/create`、`sampling/createMessage` 或 `roots/list`。新规范引入 Multi Round-Trip Requests：

1. 服务端返回 `resultType: "input_required"`、`inputRequests` 和可选 `requestState`；
2. 客户端获取用户或模型的答案；
3. 客户端以 `inputResponses` 和原样 `requestState` 重试原始请求；
4. 任何实例都可以继续处理，只要它能验证和理解状态。

`requestState` 经过客户端再返回，因此必须被当作不可信输入。若含用户数据，规范要求把它与原用户做密码学绑定；多副本部署还要共享验签/解密密钥与一致的 audience。

证据：S02、S07、S12。

### F-07｜Tasks 是扩展，不是“所有长请求自动异步化”

实验性 Tasks 从核心协议移到 `io.modelcontextprotocol/tasks` 扩展。客户端与服务端都声明支持后，服务端可返回持久任务句柄；客户端使用 `tasks/get` 轮询，使用 `tasks/update` 补充输入，使用 `tasks/cancel` 请求取消。

服务端必须先持久化任务，再返回 `taskId`。Task 状态和结果仍需要可靠存储；扩展只是统一生命周期，不替团队提供任务队列或数据库。

证据：S04、S08。

### F-08｜仍然存在流，但流被限制在请求范围

“无状态”不等于 MCP 从此没有 SSE 或长连接：

- 某个 POST 的响应仍可使用 SSE；
- `subscriptions/listen` 是一条客户端显式打开的长时 POST 响应流，用于订阅工具、Prompt 或资源变化；
- 请求相关的进度和日志仍沿当前请求的响应流发送。

协议不再要求跨请求保留传输 Session，但订阅跨实例分发仍可能需要共享 Pub/Sub。

证据：S04、S06、S12。

### F-09｜SSE 断点续传被移除

`Last-Event-ID` 和 SSE 事件重放从 `2026-07-28` Streamable HTTP 中移除。响应流断开后，当前请求丢失，客户端必须使用新的 JSON-RPC 请求 ID 重新发起。

这正是文章应强调幂等性的事实依据：协议定义了如何重发，却没有自动保证有副作用的工具只执行一次。JSON-RPC `id` 用于请求/响应关联，不应被当成业务幂等键。

证据：S04、S10、S12。

### F-10｜GitHub 已给出真实的基础设施收益案例

GitHub MCP Server 在 7 月 23 日宣布提前支持新规范，披露了三项改动：

- 删除 Redis Session，去掉初始化写入与每次调用读取；
- 网关从标准 HTTP 头获取日志与 secret scanning 所需字段，不再解析每个 Payload；
- 用 Go SDK 的兼容封装同时服务旧版与新版 elicitation 流程。

这是特定服务的官方案例，不应外推成所有 MCP Server 都能删除 Redis。只要应用仍有浏览器状态、审批任务、作业进度或业务缓存，Redis/数据库仍可能必要。

证据：S09、S10。

### F-11｜旧客户端不会自动消失

官方 SDK 强调向后兼容。2025 时代的客户端仍会执行 `initialize` 并携带 Session；新版服务端通常需要同时提供 legacy 与 modern 两条路径，或者明确切断旧版本。

因此，迁移期内不能一边删除旧会话设施，一边假设所有客户端已经升级。版本分布应先通过日志和 staging 验证。

证据：S09、S10、S12。

### F-12｜四个 Tier 1 SDK 已支持正式规范，但版本与默认行为不同

MCP 官方发布博客写明 TypeScript、Python、Go、C# 都已支持 `2026-07-28`。具体迁移行为并不完全一致：

- Go `v1.7.0` 是稳定发布，并对旧协议保留兼容；
- Python v2 会优先探测 `server/discover`，失败时回退 legacy；
- TypeScript v2 的迁移文档说明，部分构造方式仍需显式打开新版协商；
- 扩展支持也可能晚于核心协议，例如某些 SDK 尚未实现 Tasks。

正文不逐一罗列版本号，只给出判断：规范正式，不代表团队当前依赖组合已经自动切换。

证据：S02、S10、S12、S13。

## 六、旧模式与新模式的工程差异

| 维度 | 2025-11-25 时代 | 2026-07-28 | 新责任 |
|---|---|---|---|
| 生命周期 | `initialize` / `initialized` | 请求自包含，`server/discover` 按需 | 每次请求携带并校验版本与能力 |
| 传输会话 | `Mcp-Session-Id` 可跨请求 | 协议 Session 被移除 | 业务状态必须显式建模 |
| 负载均衡 | 常需粘性路由或共享 Session | 任意实例可处理普通请求 | 共享业务存储、密钥和订阅总线仍按需存在 |
| 中途补充输入 | 服务端在持有通道上反向请求 | MRTR 返回 `input_required` 后由客户端重试 | 保护、校验并限时使用 `requestState` |
| 长任务 | 实验性核心 Tasks / 持有连接 | Tasks 扩展与持久 `taskId` | 任务必须先持久化，处理轮询、取消和恢复 |
| 网关识别 | 可能解析 JSON-RPC Body | 标准方法/名称头 | 头体一致性、鉴权与细粒度策略 |
| 流恢复 | 可使用 SSE Event ID 重放 | 取消协议层重放 | 重新请求、业务幂等、去重 |
| 观察性 | 连接/Session 常被当作关联线索 | W3C Trace Context 约定 | 为业务工作流另设 trace/workflow 标识 |

## 七、“状态没有消失”应怎样拆开讲

可以把新架构里的状态分成五类，避免一句“放进 Redis”带过所有问题。

| 状态类型 | 推荐载体 | 主要风险 |
|---|---|---|
| 请求协议信息 | 每次请求的 `_meta` 与标准 HTTP 头 | 头体不一致、版本/能力误判 |
| 业务实体状态 | 服务端签发的显式 handle + 业务存储 | 越权引用、猜测 ID、并发更新、过期 |
| 短暂交互状态 | 受保护的 `requestState` | 篡改、重放、跨用户劫持、跨实例密钥不一致 |
| 长任务状态 | 持久 `taskId`、任务队列/数据库 | 返回句柄前未落盘、重复执行、取消语义不清 |
| 通知订阅状态 | `subscriptions/listen` + 共享 Pub/Sub | 多副本事件丢失、重复、顺序与背压 |

授权上下文不应被放进可由模型任意构造的工具参数中。OAuth Bearer Token 仍随每个 HTTP 请求发送，服务端逐次验证 token 的受众与权限；业务 handle 也要再次核对归属。

证据：S07、S08、S12、S21。

## 八、云原生收益应该写到什么程度

### 可以明确写

- 普通请求不再绑定某个实例，标准轮询负载均衡更自然；
- Pod 重启、滚动发布和横向扩缩不再因为协议 Session 本身要求回到原实例；
- 无需只为 MCP 传输会话维护 Redis；
- 方法与名称进入 HTTP 头后，网关更容易做路由、计量、限流和审计；
- Serverless/scale-to-zero 对无状态工具服务更可行。

### 必须加边界

- 正在执行的请求不会因为另一实例健康而自动恢复；流断开后要重新发起；
- 冷启动、模型调用、下游数据库和外部 API 的延迟仍然存在；
- 业务状态、任务状态、锁、队列和通知总线不会因协议升级而消失；
- 旧版客户端仍可能要求 legacy Session；
- 标准头提高可治理性，不等于自动获得安全策略和审计系统。

## 九、迁移时最容易踩的坑

### 1. 把 `Mcp-Session-Id` 直接重命名成 `conversation_id`

如果新 ID 仍由客户端任意指定、后端不校验归属，并被拿来承载全部上下文，只是把隐藏 Session 搬到了工具参数。应先区分业务实体、工作流、用户会话和一次请求，再决定句柄粒度。

### 2. 在 `initialize` 里只做一次授权检查

协议握手被移除后，每次请求都可能落到新实例。认证、token audience、工具权限和资源归属必须在请求边界重新验证。

### 3. 用 JSON-RPC `id` 当幂等键

流断开后规范要求用新请求 ID 重试。扣款、退款、发消息、建资源等有副作用操作需要应用自己的幂等键、去重记录和结果缓存。

### 4. 让每个 Pod 自己生成 `requestState` 密钥

MRTR 第一次落在 A，重试落到 B 时，B 可能无法验签或解密。多实例必须共享密钥轮换策略与 audience，并为 token 设置 TTL、用户绑定和重放防护。

### 5. 返回 `taskId` 后才异步落盘

Tasks 规范要求任务在返回句柄之前已经可查询。否则客户端立刻轮询会得到“任务不存在”，故障切换时也无法恢复。

### 6. 立即删除所有 Session 兼容设施

先统计客户端协议版本，再决定保留双栈多久。灰度期间至少监控新版协商率、legacy 回退率、`HeaderMismatch`、重复请求和任务恢复失败。

## 十、建议的迁移验证清单

### 协议兼容

- 记录服务端收到的协议版本和 SDK/客户端分布；
- 验证 `server/discover`、legacy `initialize` 回退和不支持版本错误；
- 检查 `Mcp-Method`、`Mcp-Name` 与 Body 不一致时是否被拒绝；
- 确认旧客户端是否仍需要粘性路由或共享 Session。

### 状态与可靠性

- 盘点所有读取 `Mcp-Session-Id`、连接内存和 initialize 缓存的代码；
- 为有副作用工具定义业务幂等键、重复请求结果和补偿策略；
- 在请求处理过程中强制切换 Pod，验证普通请求、MRTR 和 Tasks；
- 验证任务在进程退出、滚动发布和客户端重连后仍可查询；
- 测试 `requestState` 篡改、过期、跨用户重放和跨实例验签。

### 权限与可观测性

- 每次请求验证 access token、audience、scope 与 handle 所属用户；
- 网关可按方法/名称限流，但后端仍做头体一致性与业务鉴权；
- 传播 `traceparent`，并为跨多个 MCP 请求的业务工作流记录独立关联 ID；
- 对重试次数、重复执行、任务停留时间和 legacy 回退建立指标。

## 十一、国内开发者平台观点与读者语境

本次按要求检索了知乎、稀土掘金、CSDN/火山引擎开发者社区等平台。未检索到足够成熟的中文文章系统解读 `2026-07-28` 正式规范；可见内容多数仍基于 2025 版 SDK 和旧生命周期。

### 稀土掘金

一篇 2026 年初的 MCP 工程教程仍以 `Mcp-Session-Id`、内存 `transports` Map 和“每个会话一个 MCP Server 实例”为核心示例。它很好地反映了国内开发者现有代码的迁移面：Session 不只是概念，还进入了路由、实例管理和清理逻辑。

用途：解释为什么升级不是删一个 Header，而是要审计应用对 Session 的依赖。不能把旧教程写成新规范要求。

证据：S15。

### CSDN / 火山引擎开发者社区

多篇实践文章把 Streamable HTTP 分成 stateful 与 `stateless_http=True` 两种模式，并讨论 Session ID、DELETE 清理、GET/SSE 通知、EventStore 和断线重放。它们反映了 2025 时代的真实关注点，也暴露出容易混淆的地方：SDK 的“无状态模式”不等于 `2026-07-28` 已删除协议 Session 的新生命周期。

用途：提醒正文必须区分“旧 SDK 的可选 stateless 配置”和“新规范的 sessionless core”。

证据：S16、S17。

### 知乎

可检索讨论主要围绕 Streamable HTTP 是否需要 HTTP/2、SSE 与 HTTP 流的关系，说明读者容易把“无状态协议”误解成“没有流”或“只能普通 JSON 响应”。正文应明确：流仍可存在，只是不再承担跨请求的协议 Session。

证据：S18。

这些平台材料只用于理解迁移语境和常见误解，发布时间、规范条款和 SDK 状态仍以官方来源为准。

## 十二、争议与反方判断

### “2025 版已经能开无状态模式，这次只是改默认值”

不准确。旧 SDK 确实允许部分 Streamable HTTP Server 不签发 Session ID，但协议仍要求初始化生命周期，能力协商与多种反向请求仍围绕连接存在。`2026-07-28` 同时移除了握手与 Session，并重做 MRTR、订阅、缓存和 Tasks。

### “所有状态显式化后，请求会变得很胖”

请求会重复携带版本和能力元数据，也可能带显式 handle。这是无状态协议常见的带宽换复杂度取舍。文章不必声称它在所有场景都更快；核心收益是实例解耦、故障边界和可治理性。

### “不用 Redis 了，所以成本一定下降”

只能说“只为协议 Session 使用的 Redis 可以减少”。真正有业务状态的服务仍需要存储，甚至会因为任务、幂等和审计而使用更明确的数据模型。

### “长任务和通知仍要流或存储，所以无状态是伪命题”

无状态指接收方无需从前一次请求推断当前请求。请求范围内的 SSE、显式任务句柄和外部业务存储并不违反这个定义。它们把复杂度按需引入，而不是让每个普通调用都承担会话成本。

## 十三、对程序员的实际影响

### MCP Server 开发者

需要从“定义 Tool Schema + 写 handler”进一步补齐：显式状态模型、请求级鉴权、幂等、任务持久化、密钥轮换、跨实例通知和故障注入测试。

### 平台与架构团队

可以把 MCP 纳入已有 API Gateway、WAF、OpenTelemetry、弹性扩缩与发布体系，但要为新头部、协议版本、Tasks 和 legacy 双栈补策略与指标。

### 普通 MCP 使用者

不必因为正式规范发布就立刻重写所有服务。先看客户端和 SDK 是否真的协商到 `2026-07-28`，再做迁移。仅使用本地 `stdio`、没有横向扩展需求的项目，收益没有远程多副本服务那么明显。

## 十四、江小北可表达的观点

1. “无状态”不是没有状态，而是不能再把状态含糊地塞在连接里；
2. MCP 走向生产，不是多了几个 Tool，而是开始接受普通分布式系统的约束；
3. 标准把负载均衡变简单了，却没有替团队解决幂等、授权与恢复；
4. 对 Agent 开发者来说，下一项稀缺能力不是再学一种 Schema，而是把工作流设计成可重试、可恢复、可审计的状态机；
5. 正式规范可以采用，生产迁移仍应由版本分布、故障演练和监控数据决定。

## 十五、历史文章与账号风格学习

已读取：

- `content/style/jiangxiaobei-writing-style.md`；
- `content/style/jiangxiaobei-image-style.md`；
- `content/articles/2026-08-07-agent-plugins-npm-moment/final.md`；
- `content/articles/2026-08-05-ai-coding-reviewability/final.md`；
- `content/articles/2026-08-06-trainable-coding-agent/final.md`；
- `content/articles/2026-08-07-kimi-k3-copilot-rollout/final.md`。

当前仓库没有 `content/published/`，因此使用已完成且带确认记录的 `content/articles/` 作为最接近的历史样本。

本篇只学习以下稳定习惯：

- 从真实工程矛盾切入，不先复述发布公告；
- 先给边界，再给判断；
- 用一张对比表或简短代码说明技术变化；
- 把建议落到迁移步骤、验收条件和故障场景；
- 不用厂商宣传口径替代工程结论。

不得复制历史文章句子，也不得移植任何他人的亲测经历。

## 十六、图片候选（阶段一仅记录，不下载）

### IMG-CANDIDATE-01｜Google 官方旧 Session 部署问题图

- 用途：展示客户端请求被绑定到 Pod、粘性路由/共享 Session Store 的旧问题；
- 来源：Google Developers Blog；
- 来源页面：https://developers.googleblog.com/en/scaling-ai-agent-infrastructure-with-the-mcp-stateless-updates/
- 原始链接：https://storage.googleapis.com/gweb-developer-goog-blog-assets/images/Screenshot_2026-08-03_at_11.42.20AM.original.png
- 优先级：高；官方图，阶段三下载并核对清晰度。

### IMG-CANDIDATE-02｜Google 官方新无状态请求图

- 用途：展示任意请求可落到任意实例；
- 来源：Google Developers Blog；
- 来源页面：同上；
- 原始链接：https://storage.googleapis.com/gweb-developer-goog-blog-assets/images/Screenshot_2026-08-03_at_11.51.27AM.original.png
- 优先级：高。

### IMG-CANDIDATE-03｜原创“状态去了哪里”分层图

- 用途：协议元数据 → 每请求；业务实体 → handle/业务库；交互 → `requestState`；长任务 → `taskId`；通知 → Subscription Bus；
- 形式：黑白灰架构图；
- 优先级：高，作为全文核心判断图。

### IMG-CANDIDATE-04｜原创“迁移故障注入矩阵”

- 用途：Pod 切换、重复请求、流中断、任务恢复、跨用户重放分别对应验证项；
- 形式：适合手机阅读的 2×3 信息卡；
- 优先级：中高。

### IMG-CANDIDATE-05｜Google 官方文章横幅

- 用途：如正文需要新闻事实配图，可作为发布背景图；
- 来源页面：同上；
- 原始链接：https://storage.googleapis.com/gweb-developer-goog-blog-assets/images/banner-4209x1253.original.png
- 优先级：低；解释性弱于架构图。

## 十七、正文中的事实边界

必须保留：

- `2026-07-28` 是正式规范，不再称 RC；
- 无状态限定为协议层，不写“应用从此不需要状态”；
- `server/discover` 是服务端必备 RPC，但客户端不是每次请求前都必须调用；
- `Mcp-Method`/`Mcp-Name` 便于网关治理，不等于头部天然可信；
- MRTR 的 `requestState` 需要校验、用户绑定和跨实例密钥一致；
- Tasks 是双方显式支持的扩展，不是自动后台执行；
- SSE 与长时订阅仍存在，但不再构成跨请求 Session；
- GitHub 删除 Redis 是特定实现案例，不能写成普遍收益；
- 四个 Tier 1 SDK 支持新规范，不等于所有客户端、框架和扩展已经默认启用；
- 不虚构压测结果、迁移成本、故障数据或亲身实践。

禁止写法：

- “MCP 彻底无状态了，Redis 可以删了”；
- “所有 MCP 请求现在都是短连接”；
- “升级后故障切换完全无感”；
- “HTTP 头让 MCP 自动获得企业级安全”；
- “Task ID 天然保证恰好执行一次”；
- “JSON-RPC ID 就是幂等键”；
- “我把三副本 MCP Server 升级后发现……”；
- “国内开发者普遍认为……”等无法量化的归因。

## 十八、建议篇幅与信息密度

- 建议正文：2500～2900 字；
- 文章类型：架构变化 + 迁移判断；
- 代码/协议示例：保留一组旧、新请求对比，不逐字段翻译规范；
- 核心图：旧/新部署对比 + “状态去了哪里”分层图；
- 行动建议：用一份迁移清单收束，重点覆盖版本、幂等、权限、恢复与观测；
- 结尾：落在“Agent 工程开始回到分布式系统常识”，不做口号式升华。
