# 来源清单与事实映射

> 文章：GPT-5.6 Luna 降价 80%，Agent 成本优化进入“分层路由”阶段
> 核验日期：2026-08-06
> 原则：价格、型号、API 能力和发布时间以 OpenAI 当前官方页面为准；论文和中文社区资料用于补充路由方法、关注点与争议。

## S01｜Advancing the price-performance frontier with GPT-5.6

- 发布方：OpenAI
- 来源类型：官方产品公告、原始来源
- 发布日期：2026-07-30
- 链接：https://openai.com/index/advancing-the-price-performance-frontier-with-gpt-5-6/
- 支持的事实或观点：Luna 降价 80%，Terra 降价 20%；Luna 当前 `$0.20 / $1.20`，Terra 当前 `$2 / $12`；Sol 标准价不变；Sol Fast mode 最高 2.5 倍速度、价格 2 倍；“Sol 规划、Luna 执行和测试”的官方编码工作流示例；风险、错误代价、时效和规模决定模型选择。
- 使用边界：合作方评价和效果数据均来自官方公告，不视为独立验证；官方明确说明不同工作流可能采用不同平衡。
- 核验状态：已打开原文逐段核验；访问日期 2026-08-06。

## S02｜GPT-5.6: Frontier intelligence that scales with your ambition

- 发布方：OpenAI
- 来源类型：官方模型发布公告
- 发布日期：2026-07-09；页面于 2026-07-30 增加降价更新
- 链接：https://openai.com/index/gpt-5-6/
- 支持的事实或观点：GPT-5.6 Sol、Terra、Luna 全面可用；降价前 API 价格分别为 `$5 / $30`、`$2.50 / $15`、`$1 / $6`；三个档位的定位；模型和合作方 benchmark；缓存写入与读取计费概览。
- 使用边界：页面的 benchmark 主要是 OpenAI 报告结果；用于说明产品定位和降价基数，不把分数外推到用户业务。
- 核验状态：已打开原文核验；当前页面明确标注 7 月 30 日降价更新。

## S03｜How GPT-5.6 fuses frontier intelligence with frontier efficiency

- 发布方：OpenAI
- 来源类型：官方工程文章
- 作者：Matthew Ferrari、Phil Tillet、Ahmed Ibrahim、Joe Gershenson、Steve Coffey
- 发布日期：2026-07-29
- 链接：https://openai.com/index/gpt-5-6-frontier-intelligence-efficiency/
- 支持的事实或观点：效率优化覆盖负载均衡、调度、Kernel、缓存、推测解码、上下文与工具管理；Sol 参与生产 Kernel 优化，使端到端服务成本降低 20%；推测模型改进让 Token 生成效率提升 15% 以上；Agent 多轮循环会放大重复上下文和工具成本。
- 使用边界：20% 和 15% 是 OpenAI 内部生产结果，没有独立复现；正文必须标注“OpenAI 表示”。
- 核验状态：已打开原文核验。

## S04｜GPT-5.6 Luna model

- 发布方：OpenAI Developers
- 来源类型：官方模型文档
- 发布日期：页面未标注；访问日期 2026-08-06
- 链接：https://developers.openai.com/api/docs/models/gpt-5.6-luna
- 支持的事实或观点：Luna 当前输入、缓存输入、输出价格为 `$0.20 / $0.02 / $1.20`；1.05M 上下文、128K 最大输出；工具与端点支持；超过 272K 输入时的长上下文计费规则。
- 使用边界：价格是动态信息，阶段二和发布前需再次打开核验；搜索结果摘要曾显示旧价，不能只引用摘要。
- 核验状态：已打开当前模型页核验。

## S05｜GPT-5.6 Terra model

- 发布方：OpenAI Developers
- 来源类型：官方模型文档
- 发布日期：页面未标注；访问日期 2026-08-06
- 链接：https://developers.openai.com/api/docs/models/gpt-5.6-terra
- 支持的事实或观点：Terra 当前输入、缓存输入、输出价格为 `$2 / $0.20 / $12`；定位为能力与成本平衡；1.05M 上下文、128K 最大输出；长上下文加价规则。
- 使用边界：动态价格发布前复核。
- 核验状态：已打开当前模型页核验。

## S06｜GPT-5.6 Sol model

- 发布方：OpenAI Developers
- 来源类型：官方模型文档
- 发布日期：页面未标注；访问日期 2026-08-06
- 链接：https://developers.openai.com/api/docs/models/gpt-5.6-sol
- 支持的事实或观点：Sol 当前输入、缓存输入、输出价格为 `$5 / $0.50 / $30`；`gpt-5.6` 别名路由到 Sol；定位为复杂专业工作的旗舰模型；1.05M 上下文、128K 最大输出。
- 使用边界：Fast mode 的速度和溢价另由 S07 核验。
- 核验状态：已打开当前模型页核验。

## S07｜Fast mode

- 发布方：OpenAI Developers
- 来源类型：官方 API 指南
- 发布日期：页面未标注；访问日期 2026-08-06
- 链接：https://developers.openai.com/api/docs/guides/fast-mode
- 支持的事实或观点：Priority Processing 于 2026-07-30 更名为 Fast mode；Sol 最高 2.5 倍速度；请求和项目级配置；流量爬升过快时可能回落到标准处理；`service_tier` 可用于观察实际处理档位；Fast mode 按 Token 收取溢价。
- 使用边界：具体 2 倍价格由 S01 官方公告核验；指南本身只写“per-token premium”。
- 核验状态：已打开官方指南核验。

## S08｜Cost optimization

- 发布方：OpenAI Developers
- 来源类型：官方生产指南
- 发布日期：页面未标注；访问日期 2026-08-06
- 链接：https://developers.openai.com/api/docs/guides/cost-optimization
- 支持的事实或观点：成本优化包括减少请求、减少 Token、选择在维持准确率前提下更小的模型；Batch 与 Flex 适合异步或低优先级任务；成本与延迟相互关联。
- 使用边界：页面提供通用原则，不提供本文路由节省比例。
- 核验状态：已打开官方指南核验。

## S09｜Prompt caching

- 发布方：OpenAI Developers
- 来源类型：官方 API 指南
- 发布日期：页面未标注；访问日期 2026-08-06
- 链接：https://developers.openai.com/api/docs/guides/prompt-caching
- 支持的事实或观点：GPT-5.6 缓存写入按未缓存输入价 1.25 倍计费；用 `cache_write_tokens` 和 `cached_tokens` 分别记录写入与读取；显式断点、稳定前缀和 `prompt_cache_key`；缓存命中不改变生成过程。
- 使用边界：缓存只有在稳定前缀被复用时才可能净节省；不能把“有缓存”直接写成“必然省 90%”。
- 核验状态：已打开官方指南核验。

## S10｜Evaluation best practices

- 发布方：OpenAI Developers
- 来源类型：官方评测指南
- 发布日期：页面未标注；访问日期 2026-08-06
- 链接：https://developers.openai.com/api/docs/guides/evaluation-best-practices
- 支持的事实或观点：生成式 AI 具有波动性；应做任务特定、贴近真实分布的评测；尽早评测、记录日志、尽量自动评分并结合人工判断。
- 使用边界：页面说明旧 Evals 平台将于 2026 年下半年停用；本文引用的是评测方法，不推荐特定旧平台。
- 核验状态：已打开官方指南核验。

## S11｜RouteLLM: Learning to Route LLMs with Preference Data

- 发布方：LMSYS / arXiv；后发表于 ICLR 2025
- 来源类型：论文
- 作者：Isaac Ong 等
- 发布日期：2024-06-26（arXiv 初版）
- 链接：https://arxiv.org/abs/2406.18665
- 支持的事实或观点：强弱模型动态路由可优化成本—质量权衡；部分基准实现超过 2 倍成本节省；路由器需要理解意图、复杂度与候选模型能力；分布外数据会削弱路由表现。
- 使用边界：实验使用当时的 GPT-4 与 Mixtral 等模型和公开基准，不能把节省数字直接外推到 GPT-5.6 或生产 Agent；论文主要研究单请求路由，不是完整多步 Agent 轨迹。
- 核验状态：已打开摘要、方法、实验与分布外结果段落核验。

## S12｜RouteLLM GitHub repository

- 发布方：LMSYS Org
- 来源类型：官方开源仓库
- 发布日期：访问日期 2026-08-06
- 链接：https://github.com/lm-sys/RouteLLM
- 支持的事实或观点：开源路由服务和评测框架；阈值控制强模型调用比例；官方建议基于实际查询分布校准；公共数据校准后的线上比例可能偏移。
- 使用边界：README 的“最多节省 85%”是项目方在特定 benchmark 上的结果，不作为本文生产节省结论。
- 核验状态：已打开 README 核验。

## S13｜Building effective agents

- 发布方：Anthropic
- 来源类型：官方工程文章
- 作者：Erik S.、Barry Zhang
- 发布日期：2024-12-19（页面所示为约 1.6 年前；访问日期 2026-08-06）
- 链接：https://www.anthropic.com/engineering/building-effective-agents
- 支持的事实或观点：routing 将输入分类后交给专门后续流程；适合类别清晰且分类准确的复杂任务；简单常见问题可交给更小、更便宜的模型，异常困难问题交给更强模型；保持架构简单、透明和可测试。
- 使用边界：示例使用 Anthropic 自有模型名称，本文只引用跨厂商的工作流模式。
- 核验状态：已打开原文 routing 章节核验。

## S14｜AgentRouter: Heterogeneous Model Routing for Cost-Optimal Multi-Step Agentic Workflows

- 发布方：ICML 2026 AdaptFM Workshop / OpenReview
- 来源类型：新近工作坊论文
- 作者：Rudrendu Kumar Paul、Sourav Nandy
- 发布日期：2026-07（会议页面）；访问日期 2026-08-06
- 链接：https://openreview.net/forum?id=nu3GPfkyJV
- 支持的事实或观点：把模型路由从单轮查询扩展到多步 Agent 轨迹；步骤难度会在同一任务内变化，前一步输出质量会影响后续步骤；作者报告逐步骤路由的成本—质量收益。
- 使用边界：新近工作坊论文，生产经历和 72% 成本下降等均为作者自报实验；正文若提及只用于说明研究方向，不引用为普遍收益。
- 核验状态：已核验论文首页、摘要与会议页面；OpenReview 正文页面存在浏览验证，采用可访问的论文索引内容交叉核验。

## S15｜GPT-5.6 API 接入指南：Sol、Terra、Luna 价格、1.05M 上下文与迁移代码

- 发布方：CSDN / AtomGit AI 社区
- 来源类型：中文开发者平台文章
- 作者：qq_42720852
- 发布日期：2026-07-10
- 链接：https://tianqi.csdn.net/6a506670662f9a54cb8dc0f4.html
- 支持的事实或观点：国内开发者关注模型显式分流、长上下文计费、缓存、失败升级、灰度、权限边界和每任务总成本。
- 使用边界：发表于本次降价前，价格已经过时；页面包含第三方网关推广，不承担关键事实证明。正文不引用其价格和收益计算。
- 核验状态：已打开全文核验并与官方当前文档对照。

## S16｜GPT-5.6 实战指南：API 接入、多 Agent 协同与成本优化策略

- 发布方：CSDN AI Agent 技术社区
- 来源类型：中文开发者平台文章
- 作者：weixin_34289454
- 发布日期：2026-07-13
- 链接：https://agent.csdn.net/6a56facc10ee7a33f28d9c9a.html
- 支持的事实或观点：国内内容常把分层模型、缓存、重试、批量和 A/B 测试作为成本优化关注点。
- 使用边界：存在无法核验的“实测”百分比、疑似无效模型 ID 和非官方参数示例；只用于识别常见误解，不作为事实或代码来源。
- 核验状态：已打开全文核验，判定为低可信观点素材。

## S17｜TRAE 中文社区：GPT-5.6 系列全量开放 API

- 发布方：TRAE 官方中文社区用户帖
- 来源类型：中文开发者社区讨论
- 发布日期：2026-07-07
- 链接：https://forum.trae.cn/t/topic/75410
- 支持的事实或观点：国内社区在产品发布初期已关注三档模型和任务分流。
- 使用边界：发布日期、上下文窗口和“速度拨盘”等多项表述与 OpenAI 当前官方资料不一致；不作为任何关键事实依据。
- 核验状态：已打开页面并与 S02、S04～S07 对照，标记为争议 / 误解素材。

## S18｜OpenAI API Pricing

- 发布方：OpenAI Developers
- 来源类型：官方实时价格表
- 发布日期：页面未标注；访问日期 2026-08-06
- 链接：https://developers.openai.com/api/docs/pricing
- 支持的事实或观点：GPT-5.6 Sol、Terra、Luna 的 Standard、Batch、Flex、Fast 短上下文和长上下文价格；缓存写入、缓存读取与输出价格；Priority Processing 于 2026-07-30 更名为 Fast mode；工具可能另行计费。
- 使用边界：价格属于动态信息，正式发布前仍需复核；不同处理档位、长短上下文和区域处理价格不能混用。
- 核验状态：阶段二写作前已通过 OpenAI Developers 文档重新打开核验。

## 文章关键事实映射

| 文章事实或判断 | 主要来源 |
|---|---|
| Luna 降价 80% 至 `$0.20 / $1.20`，Terra 降价 20% 至 `$2 / $12` | S01、S04、S05、S18 |
| Sol 标准价 `$5 / $30` 不变，Luna 同量 Token 价为 Sol 的 1/25 | S01、S04、S06、S18 |
| Fast mode 最高 2.5 倍速度、价格 2 倍，替代 Priority Processing | S01、S07、S18 |
| OpenAI 给出 Sol 规划、Luna 执行和测试的编码示例 | S01 |
| 20% 服务成本下降与 15% Token 生成效率提升 | S01、S03 |
| GPT-5.6 缓存写入、读取与长上下文计费边界 | S04～S06、S09、S18 |
| 成本优化要减少请求、Token，并在维持准确率前提下选小模型 | S08、S10 |
| 模型路由需要按实际分布校准，分布外表现可能下降 | S11、S12 |
| routing 是可复用的 Agent 工作流模式 | S13 |
| 多步 Agent 的步骤级路由是正在发展的研究方向 | S14 |
| 国内开发者关注点、旧价和错误参数等常见误解 | S15～S17 |
