# 来源与事实映射：MCP 删掉 Session 后，Agent 工程开始像真正的分布式系统

> 核验日期：2026-08-08
> 原则：正式规范、官方发布博客、官方 SDK 与 GitHub 生产案例承担关键事实；中文开发者平台只补充迁移语境和常见误解。

## S01｜Scaling AI Agent Infrastructure with the MCP Stateless updates

- 发布方：Google Developers Blog
- 来源类型：官方技术博客 / 厂商工程解读
- 发布日期：2026-08-05
- 链接：https://developers.googleblog.com/en/scaling-ai-agent-infrastructure-with-the-mcp-stateless-updates/
- 支持的事实或观点：Google Cloud 推动无状态传输的工程背景；旧 Session 对负载均衡、扩缩、故障切换与 Redis 的影响；标准 HTTP 头；缓存、MRTR、Tasks、授权变化；建议从 staging 开始验证；官方配图候选。
- 核验状态：已下载并读取原文；其中“release candidate/Beta SDK”状态落后于 7 月 28 日正式发布，以 S02、S03、S10 为准

## S02｜The 2026-07-28 Specification

- 发布方：Model Context Protocol Core Maintainers
- 来源类型：官方正式发布博客
- 发布日期：2026-07-28
- 链接：https://blog.modelcontextprotocol.io/posts/2026-07-28/
- 支持的事实或观点：`2026-07-28` 已正式发布；移除握手与 Session；每请求元数据；MRTR；标准头；缓存；Tasks 扩展；弃用项；四个 Tier 1 SDK 当天支持新规范。
- 核验状态：已打开原文核验

## S03｜MCP Specification 2026-07-28

- 发布方：Model Context Protocol 项目
- 来源类型：官方规范
- 发布日期：2026-07-28
- 链接：https://modelcontextprotocol.io/specification/2026-07-28
- 支持的事实或观点：MCP 的权威协议要求；基础协议采用无状态、自包含请求和按请求能力；JSON-RPC、核心能力、安全与扩展边界。
- 核验状态：已打开正式规范核验

## S04｜Key Changes in 2026-07-28

- 发布方：Model Context Protocol 项目
- 来源类型：官方变更日志
- 发布日期：2026-07-28
- 链接：https://modelcontextprotocol.io/specification/2026-07-28/changelog
- 支持的事实或观点：移除 `Mcp-Session-Id`、`initialize`/`initialized`；`server/discover`；`subscriptions/listen`；MRTR；Tasks 扩展；SSE resumability 移除；缓存提示；标准头；弃用与错误码。
- 核验状态：已打开全文关键章节核验

## S05｜Streamable HTTP Transport 2026-07-28

- 发布方：Model Context Protocol 项目 / GitHub
- 来源类型：官方传输规范
- 发布日期：2026-07-28；持续维护
- 链接：https://github.com/modelcontextprotocol/modelcontextprotocol/blob/main/docs/specification/2026-07-28/basic/transports/streamable-http.mdx
- 支持的事实或观点：`MCP-Protocol-Version`、`Mcp-Method`、`Mcp-Name` 的要求；头体不一致拒绝；`x-mcp-header` 与 `Mcp-Param-*`；POST 可返回 JSON 或 SSE；HTTP+SSE 已弃用。
- 核验状态：已打开规范原文核验

## S06｜SEP-2575: Make MCP Stateless

- 发布方：Model Context Protocol 项目
- 来源类型：官方 Standards Track SEP（Final）
- 发布日期：创建于 2025-06-18；当前状态 Final
- 链接：https://modelcontextprotocol.io/seps/2575-stateless-mcp
- 支持的事实或观点：无状态设计动机；sticky session、故障恢复与实现复杂度；按请求自包含；显式状态引用优先；请求范围内的 SSE 不违背无状态原则；`server/discover` 设计。
- 核验状态：已打开原文核验；最终要求以 S03、S04 为准

## S07｜SEP-2322: Multi Round-Trip Requests

- 发布方：Model Context Protocol 项目
- 来源类型：官方 Standards Track SEP
- 发布日期：2026（页面当前已发布）
- 链接：https://modelcontextprotocol.io/seps/2322-MRTR
- 支持的事实或观点：`InputRequiredResult`、`inputRequests`、`inputResponses`、`requestState`；客户端重试；服务端必须验证状态；含用户数据时需密码学绑定；防篡改、重放和跨用户劫持要求。
- 核验状态：已打开原文关键安全章节核验

## S08｜MCP Tasks Extension

- 发布方：Model Context Protocol 项目
- 来源类型：官方扩展文档 / 扩展规范
- 发布日期：2026；持续维护
- 链接：https://modelcontextprotocol.io/extensions/tasks/overview
- 支持的事实或观点：Tasks 是 `io.modelcontextprotocol/tasks` 扩展；双方能力声明；`taskId`、`tasks/get`、`tasks/update`、`tasks/cancel`；返回句柄前必须持久创建；轮询、补充输入与终态。
- 核验状态：已打开原文核验；具体线级要求同时核对 https://tasks.extensions.modelcontextprotocol.io/specification/draft/tasks

## S09｜GitHub MCP Server supports the next MCP specification

- 发布方：GitHub Changelog
- 来源类型：官方产品 / 生产实践公告
- 发布日期：2026-07-23
- 链接：https://github.blog/changelog/2026-07-23-github-mcp-server-supports-the-next-mcp-specification/
- 支持的事实或观点：GitHub MCP Server 提前支持新规范；删除 Redis Session 与 initialize 写入/每请求读取；标准头替代请求体深度解析；Go SDK 兼容新旧 elicitation；Tier 1 SDK 保持向后兼容。
- 核验状态：已打开原文核验；这是 GitHub 实现案例，不外推到所有 Server

## S10｜modelcontextprotocol/go-sdk v1.7.0 Release

- 发布方：Model Context Protocol Go SDK
- 来源类型：官方 GitHub Release
- 发布日期：2026-07-28
- 链接：https://github.com/modelcontextprotocol/go-sdk/releases/tag/v1.7.0
- 支持的事实或观点：稳定版 `v1.7.0` full support `2026-07-28`；无状态模型、`server/discover`、MRTR、标准头；新旧协议兼容；新版只在 stateless Streamable HTTP 路径接受；旧客户端仍可回退。
- 核验状态：已打开 Release 原文核验

## S11｜Exploring the Future of MCP Transports

- 发布方：Model Context Protocol Blog / Transports Working Group
- 来源类型：官方设计背景
- 发布日期：2025-12-19
- 链接：https://blog.modelcontextprotocol.io/posts/2025-12-19-mcp-transport-future/
- 支持的事实或观点：协议无状态化的前因；旧 Session 固定于连接导致 sticky routing 或分布式存储；目标是让普通无状态基础设施承载 MCP。
- 核验状态：已打开原文核验；用于历史背景，不替代最终规范

## S12｜Deploy & scale – MCP Python SDK

- 发布方：Model Context Protocol Python SDK
- 来源类型：官方 SDK 部署指南
- 发布日期：持续更新；访问日期 2026-08-08
- 链接：https://py.sdk.modelcontextprotocol.io/run/deploy/
- 支持的事实或观点：新协议路径没有 Session；多副本 MRTR 需共享 `RequestStateSecurity` 密钥与 audience；默认每进程密钥会导致跨 Worker 重试失败；跨副本通知需要共享 `SubscriptionBus`；授权与 Host/Origin 设置。
- 核验状态：已打开原文核验

## S13｜Python SDK What’s New / 2026-07-28 migration notes

- 发布方：Model Context Protocol Python SDK
- 来源类型：官方 GitHub 迁移文档
- 发布日期：持续更新；访问日期 2026-08-08
- 链接：https://github.com/modelcontextprotocol/python-sdk/blob/main/docs/whats-new.md
- 支持的事实或观点：新版优先 `server/discover` 并回退 legacy；现代请求无 `Mcp-Session-Id`；旧客户端仍需旧路径；MRTR、订阅、缓存、OpenTelemetry；Tasks 在 Python SDK 的实现状态边界。
- 核验状态：已打开原文关键章节核验

## S14｜MCP Just Went Stateless — What the 2026 Spec Changes About Scaling on App Service

- 发布方：Microsoft Community Hub / Apps on Azure Blog
- 来源类型：官方云平台工程解读
- 发布日期：2026-06-23
- 链接：https://techcommunity.microsoft.com/blog/appsonazureblog/mcp-just-went-stateless-%E2%80%94-what-the-2026-spec-changes-about-scaling-on-app-servic/4530222
- 支持的事实或观点：App Service 负载均衡下的新旧模式；协议无状态不等于应用无状态；显式 handle 与仍然需要 Redis/数据库的场景。
- 核验状态：已打开原文核验；发布时仍处 RC，用于架构解释

## S15｜当 LLM 开始连接真实世界：MCP 的原理、通信与工程落地

- 发布方：稀土掘金作者“不吃不吃的菜菜”
- 来源类型：国内开发者平台教程
- 发布日期：2026-01-07（搜索结果所示）
- 链接：https://juejin.cn/post/7592540388298702911
- 支持的事实或观点：国内常见 Streamable HTTP 实现把 `Mcp-Session-Id`、内存 transport Map、每 Session Server 实例和清理流程写进业务代码；用于识别迁移面。
- 核验状态：已通过搜索结果正文片段核对；基于旧协议，不承担新规范事实

## S16｜LLM——基于 MCP 协议（Streamable HTTP 模式）的工具调用实践

- 发布方：CSDN / 火山引擎 ADG 社区作者“青衫客36”
- 来源类型：国内开发者平台实践文章
- 发布日期：2025（页面搜索结果标注）
- 链接：https://adg.csdn.net/694deb905b9f5f31781ae98c.html
- 支持的事实或观点：旧 Python SDK 中 `stateless_http=True/False` 的行为差异；国内开发者已关注有状态与无状态部署，但讨论仍围绕旧版 initialize、Session 与 SDK 配置。
- 核验状态：已通过页面摘要和代码片段核验；只用于读者语境

## S17｜深度剖析 MCP SDK 最新版：Streamable HTTP 模式

- 发布方：CSDN / 火山引擎 ADG 社区作者“supingemail”
- 来源类型：国内开发者平台源码实践
- 发布日期：2025（搜索结果标注）
- 链接：https://adg.csdn.net/694cf2725b9f5f31781a9c8f.html
- 支持的事实或观点：旧版 Session ID、DELETE、GET/SSE、进度通知与无状态配置差异；用于说明新规范会影响初始化、通知和重放假设。
- 核验状态：已通过搜索结果正文片段核验；不采用其中未回到官方原始材料的性能或兼容结论

## S18｜知乎：Streamable HTTP 是最近才提出的吗？

- 发布方：知乎用户讨论
- 来源类型：国内开发者问答 / 观点
- 发布日期：2025（页面讨论时间）
- 链接：https://www.zhihu.com/en/answer/1908503298744514266
- 支持的事实或观点：开发者对 Streamable HTTP、HTTP/2、SSE 与双向流关系存在概念混淆；用于决定正文需明确“无状态不等于无流”。
- 核验状态：已通过公开可访问的问答片段核对；不承担规范事实

## S19｜TypeScript SDK Issue #330: Both SSE and StreamableHttp transport require sticky sessions

- 发布方：modelcontextprotocol/typescript-sdk GitHub 社区
- 来源类型：官方仓库 Issue / 开发者痛点
- 发布日期：2025-04-13
- 链接：https://github.com/modelcontextprotocol/typescript-sdk/issues/330
- 支持的事实或观点：多副本部署下内存 transport 与 sticky session 的实际问题；开发者要求可序列化 Session 或真正无状态的实现；为 2026 设计动机提供历史工程语境。
- 核验状态：已打开 Issue 正文核验；观点不代表最终规范

## S20｜MCP Conformance Tests

- 发布方：Model Context Protocol 项目
- 来源类型：官方 GitHub 测试套件
- 发布日期：持续更新；访问日期 2026-08-08
- 链接：https://github.com/modelcontextprotocol/conformance
- 支持的事实或观点：测试套件区分 2025 stateful lifecycle 与 2026 stateless lifecycle；可用于客户端/服务端升级验证。
- 核验状态：已打开仓库 README 核验

## S21｜Authorization – MCP Specification 2026-07-28

- 发布方：Model Context Protocol 项目
- 来源类型：官方授权规范
- 发布日期：2026-07-28
- 链接：https://modelcontextprotocol.io/specification/2026-07-28/basic/authorization
- 支持的事实或观点：授权为 HTTP MCP 的可选能力；启用时客户端必须在每个 HTTP 请求使用 `Authorization: Bearer`；服务端必须逐请求验证 token，并确认 token 的预期 audience 是当前 MCP Server；scope、401/403 与授权服务发现要求。
- 核验状态：已打开正式规范关键章节核验

## 关键事实映射

| 文章事实或判断 | 来源 |
|---|---|
| `2026-07-28` 已正式发布 | S02、S03 |
| 移除 `initialize` / `initialized` 与 `Mcp-Session-Id` | S02、S04、S06 |
| 每请求携带协议版本和能力 | S02、S04、S06 |
| `server/discover` 是服务端必须实现、客户端按需调用 | S04、S06 |
| 标准 HTTP 头及头体一致性校验 | S04、S05 |
| 缓存提示 `ttlMs` / `cacheScope` | S02、S04 |
| MRTR 的返回—补充—重试模型 | S02、S04、S07 |
| `requestState` 需防篡改、绑定用户和跨实例共享安全配置 | S07、S12 |
| Tasks 是扩展，任务句柄返回前必须持久创建 | S04、S08 |
| `subscriptions/listen` 和请求范围 SSE 仍存在 | S04、S05、S12 |
| SSE Event ID 重放被移除，断流后重新发起请求 | S04、S10 |
| GitHub MCP Server 删除了用于协议 Session 的 Redis | S09 |
| 旧客户端仍可能走 legacy Session 路径 | S09、S10、S13 |
| 四个 Tier 1 SDK 已讲新协议 | S02 |
| 启用授权时 Bearer Token 随每个 HTTP 请求发送并校验 audience | S21 |
| 国内现有教程大量依赖 Session 生命周期 | S15、S16、S17 |
| “无状态不等于无流”是需要主动解释的读者误区 | S05、S06、S18 |

## 不采用或必须降级表述的材料

- 不采用 Google 文中“release candidate”作为当前状态；正式发布时间早于该文，以 S02、S03 为准。
- 不采用“所有四个 SDK 仍是 Beta”的概括；Go 已有稳定 `v1.7.0`，各语言版本状态应分别判断。
- 不采用 Google 文中“Pod 故障对客户端完全不可见”的绝对表述；正在执行的请求仍可能中断并需要重试。
- 不把 GitHub 删除 Redis 外推为“所有 MCP Server 都能删除 Redis”。
- 不采用中文平台文章中的性能数字、连接数比例或未经原始测试核验的兼容性结论。
- 不把国内旧版教程的 `stateless_http` 配置写成 `2026-07-28` 新生命周期的等价实现。
- 不使用 Reddit、Medium 等二手文章承担关键事实；它们只用于观察争议，不进入正文参考资料优先列表。
