# 来源清单与事实映射

> 文章：AI Coding 的新瓶颈——让代码可审查  
> 核验日期：2026-08-05  
> 原则：关键事实优先使用官方资料、源码与论文；中文内容平台仅补充开发者关注点。

## S01｜Turn one giant AI-generated pull request to a reviewable stack

- 发布方：GitHub Blog
- 来源类型：官方工程博客
- 作者：Julia Muiruri
- 发布日期：2026-08-04
- 链接：https://github.blog/engineering/turn-one-giant-ai-generated-pull-request-to-a-reviewable-stack/
- 支持的事实或观点：GitHub 用 1,721 行左右的购物助手示例演示四层 stacked PR；`gh stack` CLI 与 Agent skill；每层 CI、review 顺序、底层修改后的级联 rebase；网页 rebase 的签名限制。
- 使用边界：示例行数不是行业统计；文中 Gartner 数据不作为本文关键依据。
- 核验状态：已打开原文与 WordPress API 正文核验。

## S02｜Stacked sessions and pull requests in the GitHub Copilot app

- 发布方：GitHub Blog
- 来源类型：官方产品实践文章
- 作者：Cassidy Williams
- 发布日期：2026-07-30
- 链接：https://github.blog/ai-and-ml/github-copilot/stacked-sessions-and-pull-requests-in-the-github-copilot-app/
- 支持的事实或观点：旧项目改造案例；one-shot 尝试失败；scope creep；stacked session 继承前序上下文并创建依赖 PR；stack 的官方定义。
- 使用边界：这是单个作者的个人案例，不代表普遍效果。
- 核验状态：已打开原文核验。

## S03｜About stacked pull requests

- 发布方：GitHub
- 来源类型：官方产品文档
- 发布日期：页面未标注；访问日期 2026-08-05
- 链接：https://docs.github.com/en/pull-requests/get-started/about-stacked-prs
- 支持的事实或观点：stack map、每层独立 diff、最终目标分支规则、每层 CI、`gh stack` CLI、Agent skill；功能状态为 Public Preview；同仓库限制与 GitHub Desktop 暂不支持。
- 状态变更说明：阶段一初次核验的旧 `gh-stack` 页面仍标注 Private Preview；阶段二复核时该入口已跳转到新版 GitHub Docs，本文采用最新的 Public Preview 状态。
- 核验状态：已打开官方文档核验。

## S04｜Quickstart for stacked pull requests

- 发布方：GitHub
- 来源类型：官方使用指南
- 发布日期：页面未标注；访问日期 2026-08-05
- 链接：https://docs.github.com/en/pull-requests/get-started/stacked-prs-quickstart
- 支持的事实或观点：Public Preview 状态；`gh stack` 扩展安装与 `init/add/push/submit/view` 工作流；每层 PR 只展示该层 diff。
- 核验状态：已打开官方文档核验。

## S05｜Creating stacked pull requests

- 发布方：GitHub
- 来源类型：官方使用指南
- 发布日期：页面未标注；访问日期 2026-08-05
- 链接：https://docs.github.com/en/pull-requests/how-tos/create-pull-requests/creating-stacked-pull-requests
- 支持的事实或观点：可以通过 GitHub CLI 或网页创建 stack；所有分支必须在同一仓库；PR 页面展示 stack map；已有依赖 PR 可以被识别并关联为 stack。
- 核验状态：已打开官方文档核验。

## S06｜GitHub Stacked PRs FAQ

- 发布方：GitHub
- 来源类型：官方 FAQ
- 发布日期：页面未标注；访问日期 2026-08-05
- 链接：https://github.github.com/gh-stack/faq/
- 支持的事实或观点：stacked PR 的精确定义；同仓库限制；暂不支持跨 fork；目标分支与拆分规则。
- 核验状态：已打开官方文档核验。

## S07｜Alibaba OpenCodeReview repository

- 发布方：Alibaba
- 来源类型：官方 GitHub 仓库、README、源码
- 发布日期：仓库创建于 2026-05-18；访问日期 2026-08-05
- 链接：https://github.com/alibaba/open-code-review
- 核验 commit：`533b526b4ca671712191997adb3f2fac7dd93f13`
- 支持的事实或观点：项目定位、Apache-2.0 许可证、CLI 使用方式、确定性工程与 Agent 的分工、模型兼容、JSON/CI 集成。
- 使用边界：内部规模与 benchmark 效果均为项目方自报；GitHub Stars 为动态快照（查询时约 19,030）。
- 核验状态：已浅克隆仓库、阅读 README 与源码，并通过 GitHub API 核验元数据。

## S08｜OpenCodeReview 架构文档

- 发布方：Alibaba OpenCodeReview
- 来源类型：官方技术文档与源码说明
- 发布日期：随仓库更新；核验 commit 同 S07
- 链接：https://github.com/alibaba/open-code-review/blob/533b526b4ca671712191997adb3f2fac7dd93f13/pages/src/content/docs/zh/architecture.md
- 支持的事实或观点：diff provider、文件过滤、per-file subtask、plan/main 两阶段、工具调用、评论定位、每文件独立上下文、跨文件通过工具读取、默认并发与确定性边界。
- 核验状态：已对照 `internal/agent/agent.go`、`internal/diff/` 与文档核验。

## S09｜OpenCodeReview Review Rules

- 发布方：Alibaba OpenCodeReview
- 来源类型：官方技术文档
- 发布日期：随仓库更新；核验 commit 同 S07
- 链接：https://github.com/alibaba/open-code-review/blob/533b526b4ca671712191997adb3f2fac7dd93f13/pages/src/content/docs/zh/review-rules.md
- 支持的事实或观点：规则层级、路径匹配、include/exclude、默认测试文件过滤与显式纳入方式。
- 核验状态：已读取文档并对照规则源码。

## S10｜OpenCodeReview CI/CD

- 发布方：Alibaba OpenCodeReview
- 来源类型：官方集成文档
- 发布日期：随仓库更新；核验 commit 同 S07
- 链接：https://github.com/alibaba/open-code-review/blob/533b526b4ca671712191997adb3f2fac7dd93f13/pages/src/content/docs/zh/integrations/ci.md
- 支持的事实或观点：PR/MR 触发、range review、JSON 输出、内联评论回贴、规则与并发配置。
- 核验状态：已读取文档。

## S11｜OpenCodeReview v1.8.8

- 发布方：Alibaba OpenCodeReview
- 来源类型：GitHub Release
- 发布日期：2026-08-04
- 链接：https://github.com/alibaba/open-code-review/releases/tag/v1.8.8
- 支持的事实或观点：截至调研日的最新正式版本。
- 核验状态：已通过 GitHub API 核验。

## S12｜OpenCodeReview 开放问题

- 发布方：Alibaba OpenCodeReview 社区
- 来源类型：GitHub Issues
- 发布日期：访问日期 2026-08-05
- 链接：
  - https://github.com/alibaba/open-code-review/issues/709
  - https://github.com/alibaba/open-code-review/issues/369
  - https://github.com/alibaba/open-code-review/issues/313
  - https://github.com/alibaba/open-code-review/issues/207
- 支持的事实或观点：重复评论、稳定 finding fingerprint、大文件策略、更丰富上下文仍在演进。
- 使用边界：Issue 代表公开问题/需求，不等于所有用户都会遇到。
- 核验状态：已通过 GitHub API 核验 Issue 仍为 open。

## S13｜Small CLs

- 发布方：Google Engineering Practices
- 来源类型：官方工程实践
- 发布日期：页面未标注；访问日期 2026-08-05
- 链接：https://google.github.io/eng-practices/review/developer/small-cls.html
- 支持的事实或观点：小变更评审更快、更充分、易合并和回滚；“一项自包含变更”比机械行数更重要；相关测试应同层提交；依赖变更仍需保持构建可用。
- 核验状态：已打开原文核验。

## S14｜Modern Code Review: A Case Study at Google

- 发布方：Google Research / ICSE SEIP
- 来源类型：同行评议论文页面
- 作者：Caitlin Sadowski 等
- 发布日期：2018
- 链接：https://research.google/pubs/modern-code-review-a-case-study-at-google/
- 支持的事实或观点：现代代码评审是轻量、工具化流程；研究包含 12 次访谈、44 人调查与 900 万次 review 日志。
- 使用边界：主要用于建立代码评审背景，不直接证明 AI PR 的效果。
- 核验状态：已打开论文页面核验。

## S15｜From Industry Claims to Empirical Reality: An Empirical Study of Code Review Agents in Pull Requests

- 发布方：MSR 2026 / arXiv
- 来源类型：同行评议会议论文预印本
- 作者：Kowshik Chowdhury 等
- 发布日期：2026-04-03（arXiv）
- 链接：https://arxiv.org/abs/2604.03196
- DOI：https://doi.org/10.1145/3793302.3793614
- 支持的事实或观点：AIDev 数据集中人类-only 与 CRA-only review 的合并率差异；纯 Agent 评论信噪比分析；作者建议 CRA 增强而非替代人工。
- 使用边界：开源数据、相关性研究、关键词分类；不可直接推广到企业私有仓库，也不证明因果。
- 核验状态：已阅读摘要、方法结果与有效性威胁部分。

## S16｜阿里开源 AI Code Review 工具：ocr review 的执行链路解析

- 发布方：稀土掘金
- 来源类型：国内开发者技术文章
- 作者：candyTong
- 发布日期：2026-06-26
- 链接：https://juejin.cn/post/7655208364164612105
- 支持的事实或观点：国内开发者关注 diff 范围、项目规则、结构化输出、CI 集成；强调与通用 Agent 随口 review 的差异。
- 使用边界：辅助了解国内关注点；关键事实已用官方仓库交叉核验。
- 核验状态：已阅读页面内容并交叉核验。

## S17｜万字干货｜AI 时代的 Git 版本管理，你用对了吗？

- 发布方：稀土掘金 / TRAE 技术作者
- 来源类型：国内开发者实践观点
- 发布日期：2026 年（页面检索显示约 2026 年 5 月；精确日未公开核验）
- 链接：https://juejin.cn/post/7633720757173157923
- 支持的事实或观点：Agent 巨型 diff 混合关注点；Git 历史应保留语义单元；stacked PR 让依赖显式。
- 状态说明：文章中的 private preview 信息已过时，产品状态不采用该文，改用 S03～S05 当前官方文档。
- 使用边界：只作为观点素材，不承担产品事实证明。
- 核验状态：已阅读检索到的原文内容，产品状态用 GitHub 官方文档交叉核验。

## S18｜阿里重磅开源！Open Code Review：一周 5k star，为你的代码保驾护航

- 发布方：知乎“千问云”认证机构号
- 来源类型：厂商实践文章
- 发布日期：2026-07-07
- 链接：https://zhuanlan.zhihu.com/p/2053892567784239748
- 支持的事实或观点：厂商对覆盖、定位、规则作用域、Agent 工具调用和 CI 集成的解释。
- 使用边界：效果数字与内部规模为厂商自报，不作为本文核心证据。
- 核验状态：已阅读页面内容，架构事实用仓库与源码交叉核验。

## 关键事实—来源映射

| 关键事实 | 来源 |
|---|---|
| GitHub 7 月 30 日展示 stacked sessions 案例 | S02 |
| GitHub 8 月 4 日展示 1,721 行示例与四层 stack | S01 |
| Stacked PR 当前为 public preview，仍可能变化 | S03～S05 |
| 每层独立 diff、整链规则/CI、级联合并与 rebase | S03～S06 |
| 小变更应是单一自包含 concern，并带相关测试 | S13 |
| OpenCodeReview 为确定性流程与 LLM Agent 混合架构 | S07～S10 |
| 当前公开实现为 per-file subtask，跨文件按需取上下文 | S08 |
| OpenCodeReview 仍存在开放工程问题 | S12 |
| AI Review 不应直接替代人工责任门 | S15（带研究边界） |
| 国内开发者关注规则作用域、语义 Git 单元与 CI 集成 | S16～S18 |
