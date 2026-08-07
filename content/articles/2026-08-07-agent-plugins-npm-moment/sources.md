# 来源与事实映射：Agent 的“npm 时刻”来了，但真正的坑才刚开始

> 核验日期：2026-08-07  
> 原则：官方规范与原始资料承担关键事实；技术媒体、论文和中文开发者平台只补充背景、研究信号与读者语境。

## S01｜Agent Plugins package your skills, tools, and more

- 发布方：Google Developers Blog
- 来源类型：官方公告 / 官方技术博客
- 发布日期：2026-08-06
- 链接：https://developers.googleblog.com/en/agent-plugins-package-your-skills-tools-and-more/
- 支持的事实或观点：Agent Plugins 1.0.0 的定位；初始 TSC 参与方；Google 加入 Core Maintainers；Kevin Hou 为代表；Agents CLI 与 Data Agent Kit 已支持；规范刻意不包含安装、分发、权限、沙箱、信任和用户体验；生态 Find/Describe/Package/Run 分层；三张官方配图候选。
- 核验状态：已打开原文核验

## S02｜Agent Plugins Specification 1.0.0

- 发布方：Agent Plugins 项目
- 来源类型：官方规范
- 发布日期：持续更新；访问时版本 1.0.0，状态 Working Draft
- 链接：https://agent-plugins.org/specification
- 支持的事实或观点：根目录 `plugin.json`；`$schema` 与 `name` 必填；固定 `skills/` 和 `mcp.json`；v1 只标准化 Skills/MCP；client extension 命名空间；路径 containment；MCP transport、失败隔离、`PLUGIN_ROOT`/`PLUGIN_DATA`；可选 SemVer；客户端可渐进采用。
- 核验状态：已打开规范全文关键章节核验

## S03｜Build an Agent Plugin

- 发布方：Agent Plugins 项目
- 来源类型：官方作者指南
- 发布日期：2026（页面未列具体日期）
- 链接：https://agent-plugins.org/plugin-authors
- 支持的事实或观点：最小插件结构；Skill 与 MCP 均为可选；安装、分发、启用、更新和 UI 由客户端管理，不属于可移植规范。
- 核验状态：已打开原文核验

## S04｜Compatible Clients

- 发布方：Agent Plugins 项目
- 来源类型：官方兼容性清单
- 发布日期：2026（页面未列具体日期）
- 链接：https://agent-plugins.org/compatible-clients
- 支持的事实或观点：访问日列出 VS Code、Cursor、GitHub Copilot、ChatGPT & Codex、Kiro；各客户端支持的 MCP transport 不完全相同；组件可渐进采用。
- 核验状态：已打开原文核验

## S05｜Future Considerations

- 发布方：agentplugins/agent-plugins-spec
- 来源类型：官方 GitHub 非规范性设计文档
- 发布日期：持续更新；访问日期 2026-08-07
- 链接：https://github.com/agentplugins/agent-plugins-spec/blob/main/FUTURE_CONSIDERATIONS.md
- 支持的事实或观点：v1 未定义信任、权限、沙箱、签名/provenance、秘密管理、企业控制、审计事件、插件依赖和统一测试/验证工具；这些只属于未来可能方向，没有承诺进入后续版本。
- 核验状态：已打开原文核验

## S06｜Agent Plugins Governance / Maintainers

- 发布方：agentplugins/agent-plugins-spec
- 来源类型：官方治理文件
- 发布日期：持续更新；访问日期 2026-08-07
- 链接：https://github.com/agentplugins/agent-plugins-spec/blob/main/GOVERNANCE.md
- 支持的事实或观点：项目的开放、厂商中立治理目标；治理角色由个人而非组织持有；任何单一厂商不得控制多数 Core Maintainer 席位。
- 核验状态：已打开原文核验；`MAINTAINERS.md` 在访问时仍列原始五名维护者，尚未反映 Google 公告，故维护者变化以 S01 的当日公告为准

## S07｜agentplugins/agent-plugins-spec GitHub repository

- 发布方：Agent Plugins 项目
- 来源类型：官方 GitHub 仓库
- 发布日期：持续更新；访问日期 2026-08-07
- 链接：https://github.com/agentplugins/agent-plugins-spec
- 支持的事实或观点：README 将 1.0.0 称为当前公开版本；仓库公开规范、schema、治理与未来考虑；访问时 Releases 与 Tags 页面为空。
- 核验状态：已核验仓库首页、Releases 与 Tags 页面

## S08｜Agent Skills Specification

- 发布方：Agent Skills 项目
- 来源类型：官方规范
- 发布日期：持续更新；访问日期 2026-08-07
- 链接：https://agentskills.io/specification
- 支持的事实或观点：Skill 目录至少包含 `SKILL.md`，可包含 `scripts/`、`references/`、`assets/`；`allowed-tools` 仍为实验字段；渐进加载机制。
- 核验状态：已打开原文核验

## S09｜Using scripts in skills

- 发布方：Agent Skills 项目
- 来源类型：官方开发指南
- 发布日期：持续更新；访问日期 2026-08-07
- 链接：https://agentskills.io/skill-creation/using-scripts
- 支持的事实或观点：Skills 可以指导 Agent 执行 shell 命令，也可以携带可复用脚本；这说明 Skill 不应被简化为静态 Prompt 文件。
- 核验状态：已打开原文核验

## S10｜MCP Security Best Practices

- 发布方：Model Context Protocol 项目
- 来源类型：官方安全指南
- 发布日期：持续更新；访问日期 2026-08-07
- 链接：https://modelcontextprotocol.io/docs/tutorials/security/security_best_practices
- 支持的事实或观点：本地 MCP Server 可能以客户端权限运行；恶意启动命令或 payload 可导致任意代码执行、数据外传和数据损坏；客户端应完整展示命令、显式征得同意、最小权限沙箱运行。
- 核验状态：已打开原文核验

## S11｜Model Context Protocol Specification 2025-11-25

- 发布方：Model Context Protocol 项目
- 来源类型：官方协议规范
- 发布日期：2025-11-25
- 链接：https://modelcontextprotocol.io/specification/2025-11-25
- 支持的事实或观点：MCP 支持任意数据访问和代码执行路径；工具代表任意代码执行，应谨慎对待；工具行为描述/annotations 在非可信来源下应视为不可信；用户应对数据与工具调用保有控制。
- 核验状态：已打开原文核验

## S12｜SEP-1024: MCP Client Security Requirements for Local Server Installation

- 发布方：Model Context Protocol 项目
- 来源类型：官方 Standards Track SEP（Final）
- 发布日期：2025-07-22
- 链接：https://modelcontextprotocol.io/seps/1024-mcp-client-security-requirements-for-local-server-
- 支持的事实或观点：一键安装本地 MCP Server 必须在执行前展示完整命令与参数、标明风险、要求明确同意；其动机包括静默命令执行、可见性不足、社会工程和任意代码执行。
- 核验状态：已打开原文核验

## S13｜Model Context Protocol Threat Modeling and Analyzing Vulnerabilities to Prompt Injection with Tool Poisoning

- 发布方：Huang 等
- 来源类型：arXiv 预印本 / 安全研究
- 发布日期：2026-03-23
- 链接：https://arxiv.org/abs/2603.22489
- 支持的事实或观点：对 MCP 客户端侧 tool poisoning 风险进行威胁建模并比较七类客户端；提出静态元数据分析、决策路径跟踪、异常检测与用户透明度等多层防御。
- 核验状态：已核验摘要；预印本，正文只作为研究信号，不作普遍因果外推

## S14｜Agent Plugins for AWS

- 发布方：AWS Developer Tools Blog / awslabs
- 来源类型：官方厂商实践
- 发布日期：2026-02-17（公告）
- 链接：https://aws.amazon.com/blogs/developer/introducing-agent-plugins-for-aws/
- 支持的事实或观点：在统一规范发布前，厂商已把 Skills、MCP、hooks、references 等作为插件式交付单元；说明行业需求真实存在，也说明各客户端原有插件格式与便携核心并不相同。
- 核验状态：已打开原文核验；不用于证明 1.0.0 规范条款

## S15｜Microsoft APM – Agent Package Manager

- 发布方：Microsoft GitHub 组织下的社区驱动开源项目
- 来源类型：官方 GitHub / 相邻包管理项目
- 发布日期：持续更新；访问日期 2026-08-07
- 链接：https://github.com/microsoft/apm
- 支持的事实或观点：另一个项目已提供 agent 依赖清单、传递依赖、lockfile、内容哈希、SBOM 导出、来源策略和 MCP 信任提示，并可导出标准 `plugin.json` 包；说明包管理与治理层正在独立演进。
- 核验状态：已打开仓库 README 核验；不是 Agent Plugins 1.0.0 核心规范

## S16｜Vercel `npx skills`

- 发布方：Vercel Labs
- 来源类型：官方 GitHub / Skill 安装工具
- 发布日期：持续更新；访问日期 2026-08-07
- 链接：https://github.com/vercel-labs/skills
- 支持的事实或观点：提供跨多种 Agent 客户端的 Skill 安装、临时使用与来源解析；说明分发工具早于统一 Agent Plugin 包格式存在。
- 核验状态：已打开仓库 README 核验；不等同于 Agent Plugins 安装器

## S17｜SLSA Provenance 1.2

- 发布方：SLSA / OpenSSF
- 来源类型：官方软件供应链规范
- 发布日期：v1.2；访问日期 2026-08-07
- 链接：https://slsa.dev/spec/v1.2/provenance
- 支持的事实或观点：provenance 是可验证的来源信息，用于追踪软件制品在何时、何地、如何被生成；可作为未来插件发布与来源验证的参考框架。
- 核验状态：已打开原文核验；属于借鉴方案，不是 Agent Plugins 当前能力

## S18｜Sigstore Overview

- 发布方：Sigstore / OpenSSF
- 来源类型：官方软件签名文档
- 发布日期：持续更新；访问日期 2026-08-07
- 链接：https://docs.sigstore.dev/
- 支持的事实或观点：Sigstore 可签名与验证发布文件、容器、二进制和 SBOM，并把签名事件写入防篡改公开日志；可作为插件制品签名思路的参考。
- 核验状态：已打开原文核验；属于借鉴方案，不是 Agent Plugins 当前能力

## S19｜CISA SBOM Resources Library

- 发布方：CISA
- 来源类型：政府官方软件供应链资料
- 发布日期：持续更新；访问日期 2026-08-07
- 链接：https://www.cisa.gov/topics/cyber-threats-and-advisories/sbom/sbomresourceslibrary
- 支持的事实或观点：SBOM 是记录软件组成和供应链关系的正式清单；用于支持“插件中有什么依赖”的治理建议。
- 核验状态：已打开原文核验；属于借鉴方案，不是 Agent Plugins 当前能力

## S20｜Agent、Skills、Rules、Prompt、MCP，一文把它们理清楚了

- 发布方：稀土掘金作者“前端AI充电站”
- 来源类型：国内开发者平台观点
- 发布日期：2026-03-17
- 链接：https://juejin.cn/post/7617745029118820388
- 支持的事实或观点：中文开发者仍需要 Agent/Prompt/Rules/Skills/MCP 的基础分层解释；用于判断读者疑问，不承担规范事实核验。
- 核验状态：已通过搜索结果摘要核对；页面动态加载，正文引用时不采用其技术断言

## S21｜给 Codex 装上外挂：0 基础也能看懂的插件开发入门

- 发布方：CSDN 智能体开发者社区作者 LHdongU
- 来源类型：国内开发者平台实践文章
- 发布日期：2026-06-04
- 链接：https://adg.csdn.net/6a3119c4662f9a54cb7fd655.html
- 支持的事实或观点：国内开发者把插件理解为 Skill、MCP 与资源的工作流包；常见关注点包括 manifest 路径、权限、场景描述、测试和版本管理；文章反映的是 Codex 客户端既有格式，不代表新 1.0.0 规范。
- 核验状态：已打开正文核验；仅用于读者语境

## S22｜SkillScan：字节团队面向 AI Agent Skills 的全链路安全检测方案

- 发布方：CSDN MCP 技术社区作者 2301_80289431
- 来源类型：国内开发者平台二手技术解读
- 发布日期：2026-07-06
- 链接：https://mcp.csdn.net/6a4bb116662f9a54cb8a59ab.html
- 支持的事实或观点：国内安全讨论已覆盖 Skill 包体、声明、代码、网络、依赖供应链与运行时；用于提炼读者关注点。
- 核验状态：已通过搜索结果与页面摘要核对；未找到文中“字节团队”原始发布页，不引用其统计和产品能力作为关键事实

## S23｜npm Scripts / package-lock 文档

- 发布方：npm Docs
- 来源类型：官方包管理器文档
- 发布日期：持续更新；访问日期 2026-08-07
- 链接：https://docs.npmjs.com/cli/install/ ；https://docs.npmjs.com/cli/using-npm/scripts/ ；https://docs.npmjs.com/packages-and-modules/securing-your-code/
- 支持的事实或观点：npm 依赖可能包含生命周期脚本；npm 生态同时具备 lockfile、安装脚本策略、audit、签名与 provenance 等治理机制。用于界定“npm 时刻”类比，不把 npm 的机制投射成 Agent Plugins 已有功能。
- 核验状态：已打开官方文档核验

## 关键事实映射

| 文章事实或判断 | 来源 |
|---|---|
| Google 8 月 6 日宣布加入 Core Maintainers | S01 |
| 初始参与方为 Amazon、Cursor、Microsoft、OpenAI、Vercel | S01、S06 |
| 1.0.0 的规范页状态为 Working Draft | S02 |
| 根目录 `plugin.json` + 固定 `skills/` + `mcp.json` | S02、S03 |
| v1 只标准化 Skills 和 MCP Servers | S02 |
| client extension 用反向域名命名空间 | S02 |
| 安装/分发/更新不在可移植规范内 | S03 |
| 权限、沙箱、签名、秘密、审计、依赖、测试未定义 | S05 |
| compatible clients 可增量支持，能力不必完全一致 | S02、S04 |
| 路径 containment 不等于子进程 sandbox | S02 |
| Skill 可包含并指导执行脚本 | S08、S09 |
| 本地 MCP Server 可能导致同权限任意代码执行风险 | S10、S12 |
| MCP 工具描述等元数据应视为不可信 | S11、S13 |
| lockfile/SBOM/policy 等正在相邻项目中出现 | S15 |
| provenance、签名、SBOM 是可借鉴的供应链机制 | S17、S18、S19 |
| “完整 npm 生态”类比必须带边界 | S02、S05、S23 |

## 不采用的事实

- 不采用知乎/CSDN 二手文章中的恶意 Skill 数量、比例、漏洞率等统计；未找到或未核对原始报告。
- 不采用“所有主流 IDE 已经完整兼容”之类的聚合结论；以 S04 的组件/transport 清单为准。
- 不采用 GitHub star、fork、Issue 数量作为生态成熟度证据；这些数字会快速变化且不能证明工程质量。
- 不把 APM、Vercel Skills CLI 或任一客户端 marketplace 写成 Agent Plugins 项目的官方统一包管理器。
