# 来源与事实映射

> 文章：Kimi K3 进入 GitHub Copilot  
> 核验日期：2026-08-07  
> 说明：`S` 为事实或观点来源，`H` 为历史风格与观点参考。关键事实优先采用官方页面；开发者文章只用于补充实践与争议，不外推为普遍结论。

## S01｜Kimi K3 is now available in GitHub Copilot

- 发布方：GitHub Changelog
- 来源类型：官方公告
- 发布日期：2026-08-06；页面元数据最后修改于 2026-08-07 02:01 UTC 左右
- 链接：https://github.blog/changelog/2026-08-06-kimi-k3-is-now-available-in-github-copilot/
- 支持的事实或观点：Kimi K3 为 GA；GitHub 曾因 Actions 事故临时暂停 rollout，后已恢复；渐进开放到各 Copilot 计划和多种客户端；Business/Enterprise 默认关闭；K3 由 GitHub 托管在 Fireworks AI；价格为 provider list pricing。
- 核验状态：已打开原始页面及 WordPress API 正文核验；页面当前同时保留“暂停”和“恢复”两条编辑说明。

## S02｜Incident with Actions

- 发布方：GitHub Status
- 来源类型：官方状态页 API
- 发布日期：2026-08-06 至 2026-08-07
- 链接：https://www.githubstatus.com/api/v2/incidents.json
- 事件短链：https://stspg.io/rcz3fcm83sff
- 事件 ID：`qcvjkzcs7j74`
- 支持的事实或观点：事故从 2026-08-06 15:22 UTC 持续至 2026-08-07 02:04 UTC，影响等级为 critical；workflow、runner、webhook、Pages、Copilot code review 和 Copilot coding agent 受到影响；部分触发事件无法自动重放；详细根因分析尚未发布。
- 核验状态：已通过官方 JSON API 逐条核验时间和更新内容。

## S03｜Models and pricing for GitHub Copilot

- 发布方：GitHub Docs
- 来源类型：官方计费文档
- 发布日期：持续更新；访问日期 2026-08-07
- 链接：https://docs.github.com/en/copilot/reference/copilot-billing/models-and-pricing
- 支持的事实或观点：1 AI credit = 0.01 美元；Kimi K3 每百万输入/缓存输入/输出 token 为 3/0.30/15 美元；K2.7 Code 为 0.95/0.19/4 美元；不同模型价格和超过套餐额度后的计费方式。
- 核验状态：已核验当前表格。

## S04｜Supported AI models in GitHub Copilot

- 发布方：GitHub Docs
- 来源类型：官方产品文档
- 发布日期：持续更新；访问日期 2026-08-07
- 链接：https://docs.github.com/en/copilot/reference/ai-models/supported-models
- 支持的事实或观点：Kimi K3 当前为 GA；支持的计划和客户端；VS Code 最低版本为 1.131；开放权重模型不属于默认启用资格；扩展上下文与 reasoning 的客户端边界。
- 核验状态：已核验当前页面。

## S05｜Hosting of models for GitHub Copilot

- 发布方：GitHub Docs
- 来源类型：官方托管与数据路径文档
- 发布日期：持续更新；访问日期 2026-08-07
- 链接：https://docs.github.com/en/copilot/reference/ai-models/model-hosting
- 支持的事实或观点：Kimi K3 是开放权重模型；由 GitHub 托管在 Fireworks AI；客户提示词和回复不会发送给原始模型开发者；GitHub 提醒评估 alignment、地域偏差、安全、合规和数据治理。
- 核验状态：已核验当前页面。

## S06｜Kimi K2.7 Code is generally available in GitHub Copilot

- 发布方：GitHub Changelog
- 来源类型：官方历史公告
- 发布日期：2026-07-01
- 链接：https://github.blog/changelog/2026-07-01-kimi-k2-7-is-now-available-in-github-copilot/
- 支持的事实或观点：Kimi K2.7 Code 才是 Copilot model picker 中第一个可选择的开放权重模型；Kimi K3 的意义是扩展这条路线，而非首次出现。
- 核验状态：已打开官方页面核验。

## S07｜Kimi K3 Model Card

- 发布方：Moonshot AI
- 来源类型：官方模型卡
- 发布日期：2026-07；访问日期 2026-08-07
- 链接：https://huggingface.co/moonshotai/Kimi-K3
- 支持的事实或观点：2.8T 总参数、104B 激活参数、MoE、1M 上下文、原生多模态、长程编程定位、官方 benchmark 及其 harness/effort 注释。
- 核验状态：已打开完整模型卡核验；benchmark 仅作为官方披露，不视为独立结论。

## S08｜MoonshotAI/Kimi-K3

- 发布方：Moonshot AI
- 来源类型：官方 GitHub 仓库与技术报告
- 发布日期：2026-07
- 链接：https://github.com/MoonshotAI/Kimi-K3
- 技术报告：https://github.com/MoonshotAI/Kimi-K3/blob/main/k3_tech_report.pdf
- 支持的事实或观点：模型架构、权重发布、部署方式、模型用法和技术报告；权重和代码使用 Kimi K3 License。
- 核验状态：已核验 README 和仓库文件。

## S09｜Kimi K3 License

- 发布方：Moonshot AI
- 来源类型：官方许可证
- 发布日期：2026
- 链接：https://github.com/MoonshotAI/Kimi-K3/blob/main/LICENSE
- 支持的事实或观点：允许使用、复制、修改、部署和微调；对年收入超过 2000 万美元的 Model-as-a-Service 业务和超大商业产品有附加条款；因此准确称为“开放权重”，不等同于无条件标准开源许可。
- 核验状态：已逐条核验许可证正文。

## S10｜Kimi K3 API & Playground

- 发布方：Fireworks AI
- 来源类型：官方托管模型页
- 发布日期：模型页显示创建于 2026-07-19；访问日期 2026-08-07
- 链接：https://fireworks.ai/models/fireworks/kimi-k3
- 支持的事实或观点：Fireworks serverless 价格为每百万输入/缓存输入/输出 token 3/0.30/15 美元；支持约 1M 上下文、图像输入和 function calling。
- 核验状态：已打开官方模型页核验。

## S11｜从零手写物理引擎、小游戏和逻辑求解器：我用 Kimi Code 实测 Kimi K3

- 发布方：方子敬 / 博客园
- 来源类型：国内开发者实践
- 发布日期：2026-07
- 链接：https://www.cnblogs.com/zhchoice/p/21614793/kimi-k3-local-engineering-review
- 支持的事实或观点：一项可复验的小型工程测试记录了长任务、模块拆分、测试和构建结果；作者同时强调产品体验、物理真实性、无障碍和主动决策仍需人工判断。
- 核验状态：已打开正文核验；仅作为单次实践，不外推为通用性能。

## S12｜Kimi K3 实测：编程能力、Kimi Code、100 万上下文与真实项目结果

- 发布方：XBSTACK
- 来源类型：国内开发者实践
- 发布日期：2026-07-18，后续有更新
- 链接：https://www.xbstack.com/ai/tools-lab/kimi-k3-real-astro-project-test/
- 支持的事实或观点：跨文件调查能力、首轮工程决策错误及补充证据后的纠正；1M 上下文、缓存失效和真实项目验证的实践提醒。
- 核验状态：已打开正文核验；作者自述结果仅作为观点素材。

## S13｜实测 Kimi K3：国产模型见过能打的，没见过这么敢要价的

- 发布方：光子星球，经新浪转载
- 来源类型：中文技术媒体实测
- 发布日期：2026-07-18
- 链接：https://finance.sina.cn/stock/jdts/2026-07-18/detail-iniiefhq1428043.d.html
- 支持的事实或观点：国内讨论集中在前端能力、价格、不同任务偏科和“跑分不等于真实体验”；文章使用原创 prompt，但仍属于媒体单次测试。
- 核验状态：已打开正文核验；不把其评分和结论写成普遍事实。

## H01｜别再看榜单了！普通人也可以测出了各大编程模型真实差距

- 发布方：刘小排
- 来源类型：已发布历史文章 / 观点参考
- 发布日期：2026-01-07
- 本地文件：`gzh-history/liuxiaopai/别再看榜单了_普通人也可以测出了各大编程模型真实差距.md`
- 原文：https://mp.weixin.qq.com/s/pAMcP5-tFyIouOpIVzmU0Q
- 支持的事实或观点：用综合任务和真实项目比较模型，榜单只作为参考。
- 核验状态：已读取本地归档；不作为 K3 当前事实来源。

## H02｜难以置信！Kimi K2 Thinking 编程力正面超车 GPT-5 和 Sonnet 4.5

- 发布方：刘小排
- 来源类型：已发布历史文章 / 表达边界参考
- 发布日期：2025-11-07
- 本地文件：`gzh-history/liuxiaopai/难以置信_Kimi_K2_Thinking_编程力正面超车_GPT_5_和_Sonnet_4_5.md`
- 原文：https://mp.weixin.qq.com/s/r7wipKvD22K3SOxjPyPMVw
- 支持的事实或观点：历史 Kimi 选题常用实测和对比；本篇不继承“全面超车”的夸张结论。
- 核验状态：已读取本地归档；不作为 K3 当前事实来源。

## H03｜何止是“看图写代码”，Kimi K2.5 甚至可以“看视频写代码”！

- 发布方：刘小排
- 来源类型：已发布历史文章 / 观点参考
- 发布日期：2026-01-27
- 本地文件：`gzh-history/liuxiaopai/何止是_看图写代码__Kimi_K2_5甚至可以_看视频写代码__.md`
- 原文：https://mp.weixin.qq.com/s/ZwQQRfRdd2tPsrid3OTCIQ
- 支持的事实或观点：多模态亮点与复杂 Bug 处理能力需要分开测试。
- 核验状态：已读取本地归档；不作为 K3 当前事实来源。

## H04｜告别“切模型”与账单焦虑：Claude 1/6 价格的 Kimi K2.6，原生多模态编码实测

- 发布方：刘小排
- 来源类型：已发布历史文章 / 观点参考
- 发布日期：2026-04-21
- 本地文件：`gzh-history/liuxiaopai/告别_切模型_与账单焦虑_Claude_1_6_价格的_Kimi_K2_6_原生多模态编码实测.md`
- 原文：https://mp.weixin.qq.com/s/Vsp3jymh_GEkUq0N8xDSFg
- 支持的事实或观点：模型能力要放回 Agent 工具链、故障归因和总任务成本中评估。
- 核验状态：已读取本地归档；不作为 K3 当前事实来源。

## 关键事实映射

| 文章事实 | 来源 |
|---|---|
| Kimi K3 当前为 GA，rollout 曾暂停后恢复 | S01、S04 |
| Actions 事故起止时间、影响和恢复要求 | S02 |
| 暂无证据表明 Kimi 导致 Actions 事故 | S01、S02（基于两份官方页面的事实边界） |
| K2.7 Code 是 Copilot 第一个可选开放权重模型 | S06 |
| K3 由 GitHub 托管在 Fireworks AI | S01、S05 |
| Business/Enterprise 默认关闭 | S01、S04 |
| K3 价格为 3/0.30/15 美元 | S01、S03、S10 |
| 开放权重不等于 Copilot 本地运行 | S05、S08、S09 |
| 2.8T、104B 激活、1M 上下文等模型规格 | S07、S08 |
| 团队应做真实仓库测试，不只看 benchmark | S07、S11、S12、H01 |

