# 调研笔记：Agent 的“npm 时刻”来了，但真正的坑才刚开始

> Issue：GST-9  
> 目标公众号：AI架构师江小北  
> 当前阶段：阶段一｜调研与大纲  
> 调研日期：2026-08-07（Asia/Shanghai）

## 一、输入完整性

Issue 已提供完成阶段一所需的关键输入：

- 目标公众号：AI架构师江小北；
- 选题：Agent Plugins 1.0.0 统一打包 Agent Skills 与 MCP Server；
- 推荐标题：《Agent 的“npm 时刻”来了，但真正的坑才刚开始》；
- 核心论点：统一包装提升能力复用效率，也扩大恶意指令、过期依赖和越权工具的传播半径；
- 原始来源：Google Developers Blog、Agent Plugins Specification、Compatible Clients；
- 建议文章结构与可执行建议。

没有用户授权的个人项目经历、亲测数据或采访材料。本篇不得写成江小北“已经安装、测试或上线过 Agent Plugin”。

## 二、调研后的核心判断

标题中的“npm 时刻”可以保留，但正文必须尽早纠偏：

> Agent Plugins 1.0.0 更像 Agent 生态终于出现了共同的“包格式”，还不是完整的 npm 生态。它解决“能力怎样装进同一个盒子”，没有解决“去哪里找、怎样安装、依赖怎样锁定、发布者是否可信、能拿什么权限、出事怎样追踪”。

因此，文章的主线不应只是“又一个标准发布”，而应是：

1. Skills 和 MCP 已分别标准化了工作方法与工具连接，但跨客户端交付仍要维护不同包装；
2. Agent Plugins 用极小的公共核心解决包装漂移问题；
3. 同一个公共格式会同时降低优质能力和恶意能力的分发成本；
4. 真正决定它能否进入团队生产环境的，是格式之外的软件供应链与运行时治理能力。

## 三、已经核验的关键事实

### F-01｜发布时间、参与方与 Google 的角色

- Google Developers Blog 于 2026-08-06 发布介绍文章。
- 官方称 Agent Plugins 1.0.0 是开放、厂商中立的规范。
- 初始核心维护者来自 Amazon、Cursor、Microsoft、OpenAI、Vercel；Google 宣布以 Kevin Hou 为代表加入 Core Maintainers。
- Google 表示 Agents CLI 与 Data Agent Kit 已支持该格式，并计划在更多已支持 Skills/MCP 的产品中采用。

证据：S01、S06。

### F-02｜规范的正式程度需要带限定语

- 规范网站标注 `Spec Version: 1.0.0`，状态为 `Working Draft`。
- GitHub README 同时把 1.0.0 称为“current published release”。
- 截至 2026-08-07，GitHub Releases 与 Tags 页面均为空。

写作口径：可称“1.0.0 已公开发布的工作草案/规范版本”，不写“稳定 ABI 已经定型”。

证据：S02、S07。

### F-03｜一个插件到底是什么

一个合规插件是一个自包含目录，最小要求是根目录存在 `plugin.json`：

```text
reports-plugin/
├── plugin.json
├── skills/
│   └── summarize/
│       ├── SKILL.md
│       ├── scripts/
│       └── references/
├── mcp.json
└── com.example.client/
```

核心规则：

- `plugin.json` 必须位于根目录；必填字段只有 `$schema` 和 `name`；
- Skills 固定从 `skills/` 的直接子目录发现；
- MCP Server 固定从根目录 `mcp.json` 发现；
- `plugin.json` 不能内联组件，也不能改写组件发现路径；
- 客户端专属能力放到反向域名命名空间，例如 `com.example.client/`；其他客户端可以忽略；
- v1 的便携核心只标准化 Skills 和 MCP Servers 两种组件；commands、hooks、agents、rules、LSP 等仍属于客户端扩展。

证据：S02、S03。

### F-04｜MCP 配置的可移植范围

- `mcp.json` 明确支持 `stdio`、`streamable-http` 和兼容旧版的 `sse` 三种类型；
- 客户端支持 MCP 时，至少实现 `stdio` 或 `streamable-http` 之一即可，不要求两者全支持；
- 合规客户端也可以只支持 Skills 或只支持 MCP，只要至少支持一种组件类型；
- 某个 MCP Server 启动、连接、认证或握手失败时，客户端应跳过该条目并继续加载独立组件；
- v1 不定义 OAuth 配置或可移植的凭据引用字段，认证发现、用户交互和凭据存储由客户端管理。

这意味着“格式兼容”不等于“每个客户端表现完全一致”。

证据：S02、S04。

### F-05｜规范已经处理的安全边界

规范并非完全不谈安全，它明确规定：

- 插件包内路径解析后不能逃逸出插件根目录；
- 本地 MCP 的 `command` 是单个可执行 token，不是任意 shell 命令字符串；
- 远程非回环地址必须使用 HTTPS；
- `env` 与 HTTP headers 不得被当作可移植的秘密存储机制；
- `PLUGIN_ROOT` 与 `PLUGIN_DATA` 由客户端提供，后者用于持久化依赖、缓存与状态。

但规范同时明确指出：这些路径约束不构成进程沙箱，也不限制插件子进程运行时能够访问的路径。

证据：S02。

### F-06｜v1 刻意没有解决什么

官方文档明确把以下事项放在可移植规范之外：

- 安装机制、分发协议、启用与更新流程、用户界面；
- 信任模型、权限声明、沙箱要求和用户授权体验；
- 发布来源与完整性验证、签名与证明链；
- 秘密注入、隔离、轮换与撤销；
- 企业 allowlist/blocklist、私有注册中心和审批流；
- 生命周期审计事件标准；
- 插件之间的依赖声明、传递依赖解析和冲突处理；
- 统一测试工具、插件 linter 与客户端一致性测试。

证据：S03、S05。

### F-07｜当前列出的兼容客户端

Compatible Clients 页面在访问日列出：

- VS Code；
- Cursor；
- GitHub Copilot；
- ChatGPT & Codex；
- Kiro。

页面同时强调客户端可以渐进采用组件与 MCP transport，因此不应把这张名单理解为“所有插件在五个客户端上功能完全相同”。

证据：S04。

## 四、把三层关系讲清楚

| 层 | 解决的问题 | 主要载体 | 没解决的问题 |
|---|---|---|---|
| Agent Skills | Agent 应该怎样完成某类任务 | `SKILL.md`、脚本、参考资料、素材 | 跨组件打包、工具协议、安装与信任 |
| MCP | Agent 怎样连接和调用外部工具/数据 | MCP 协议与 Server | 工作方法、插件包、发布来源 |
| Agent Plugins | Skills 与 MCP Server 怎样作为一个单元交付 | `plugin.json`、固定目录、`mcp.json`、客户端扩展命名空间 | 注册中心、安装器、权限、沙箱、签名、依赖治理 |

可用类比，但正文应提醒读者类比只用于理解分层：

- Skills 像“工作说明书 + 可选脚本”；
- MCP 像“工具连接协议”；
- Agent Plugin 像“把说明书和工具配置装在一起的发行目录”。

不要把 Skills 简化成纯 Prompt。Agent Skills 规范允许 `scripts/`，也允许在 `SKILL.md` 中指导 Agent 执行命令；这正是其可复用价值和风险来源之一。

证据：S08、S09。

## 五、“npm 时刻”类比的成立与不成立

| 维度 | npm 生态已有能力 | Agent Plugins 1.0.0 | 判断 |
|---|---|---|---|
| 包的身份与元数据 | `package.json` | 根目录 `plugin.json` | 类比成立 |
| 约定目录/内容发现 | 包内容与入口约定 | 固定 `skills/`、`mcp.json` | 类比成立 |
| 版本表达 | SemVer 成熟使用 | `version` 可选，建议 SemVer | 只完成基础表达 |
| 依赖声明与解析 | dependencies、传递依赖解析 | 不支持插件依赖 | 尚未具备 |
| 锁文件与完整性 | `package-lock.json`、integrity | 核心规范没有 lockfile | 尚未具备 |
| 注册中心与分发 | npm registry | 安装、分发由客户端或其他项目处理 | 尚未具备 |
| 发布者信任与签名 | 2FA、provenance、registry signatures 等 | 核心规范不定义 | 尚未具备 |
| 安装/运行脚本治理 | 生命周期脚本与 allow/ignore policy | 由客户端决定 Skill/MCP 如何加载和执行 | 尚未统一 |
| 漏洞与成分治理 | audit、SBOM 等生态工具 | 核心规范不定义 | 下一层基础设施 |

更准确的表达：

> “npm 时刻”不是说 Agent Plugins 已经等于 npm，而是 Agent 能力第一次有机会沿着软件包生态的路径演化。包装格式出现后，注册、依赖、锁定、签名、审计和沙箱才有了共同对象。

旁证：Microsoft 的开源 APM 已在另一个项目中提供 `apm.yml`、`apm.lock.yaml`、完整性哈希、SBOM 导出与策略文件；Vercel 的 `npx skills` 已提供跨多种 Agent 客户端的 Skill 安装。这些项目说明“包管理层”正在出现，但它们不是 Agent Plugins 1.0.0 核心规范的一部分。

证据：S15、S16。

## 六、真正值得写的安全变化

### 1. 风险不只在可执行代码，也在可执行意图

传统依赖审查主要检查源代码、二进制与依赖树。Agent Plugin 还会带入会被模型读取的指令。一个恶意 `SKILL.md` 可以诱导 Agent 读取敏感文件、调用工具或执行脚本，即使它看起来只是 Markdown。

这是本文区别于普通“软件插件安全”文章的关键点。

### 2. 本地 MCP Server 可能与客户端同权限运行

MCP 官方安全文档明确警告：本地 MCP Server 是下载到用户机器并执行的二进制或命令，缺乏沙箱和授权时可能产生任意代码执行、数据外传与数据损坏。客户端应显示完整命令、要求明确同意，并以最小权限沙箱运行。

证据：S10、S11、S12。

### 3. 工具元数据也可能成为提示注入入口

MCP 规范要求把工具描述等注解视为不可信数据。2026 年一篇针对七类 MCP 客户端的研究把“tool poisoning”作为重点攻击面，说明静态校验、参数可见性和用户透明度仍有不足。

论文结论只能作为研究信号，不把预印本结果外推为所有客户端的普遍安全水平。

证据：S11、S13。

### 4. 可移植性会放大传播半径

过去每个客户端的包装不兼容，既是维护成本，也是一层摩擦。公共格式消除摩擦后，好的工作流可以更快复用，恶意或过期组件同样可以更快到达更多宿主。

这是推论，不是规范原文。正文应明确写成工程判断。

## 七、下一层基础设施应如何展开

可按五个问题组织，不写成空泛的“安全很重要”：

1. **它从哪里来？** 发布者身份、源仓库、构建来源、签名和 provenance；
2. **里面有什么？** Skills、脚本、MCP Server、二进制、运行时依赖与 SBOM；
3. **这次到底装了哪一版？** 版本、commit/digest、锁文件、升级 diff 与回滚；
4. **运行时能做什么？** 文件、网络、凭据、工具与子进程的最小权限和沙箱；
5. **发生过什么？** 安装、启用、更新、命令执行、授权和失败的审计记录。

SLSA、Sigstore 和 SBOM 是可借鉴的软件供应链工具，不应写成 Agent Plugins 已经采用的机制。

证据：S17、S18、S19。

## 八、国内开发者平台观点与争议

本次检索了知乎、稀土掘金与 CSDN。由于 Agent Plugins 1.0.0 发布不足一天，暂未检索到可作为关键事实来源的中文深度讨论；中文内容主要集中在三类既有问题：

1. **概念辨析**：开发者仍在反复区分 Agent、Prompt、Rules、Skills 与 MCP，说明文章必须先把层次讲清，不能直接进入 manifest 细节；
2. **客户端格式不兼容**：现有 Claude/Codex/Cursor 插件教程常使用不同 manifest 路径和专属目录，正好解释统一包装层为何出现；
3. **安全关注上升**：Skill 安全讨论已从“脚本有没有恶意代码”扩展到声明文本、提示注入、依赖、网络行为和运行时权限。

这些平台内容只用于理解读者疑问和实践语境，不承担发布时间、规范条款和安全数据的事实证明。部分文章存在二手转述或无法打开完整正文的问题，正文不引用其中的统计数字。

参考：S20、S21、S22。

## 九、历史文章与账号风格学习

已读取：

- `content/style/jiangxiaobei-writing-style.md`；
- `content/style/jiangxiaobei-image-style.md`；
- `content/articles/2026-08-05-ai-coding-reviewability/final.md`；
- `content/articles/2026-08-06-trainable-coding-agent/final.md`；
- `gzh-history/liuxiaopai/Claude_Skills_不就是把提示词存个文件夹吗_.md`；
- `gzh-history/liuxiaopai/装了一大堆Skill_你的AI_Coding_Agent编程能力就会自动提升_.md`；
- `gzh-history/liuxiaopai/OpenAI悄悄放大招_Codex_Security_Plugin_一键扫爆你代码的安全隐患.md`。

本篇只学习以下稳定表达习惯：

- 从程序员熟悉的安装/复制/多客户端适配场景切入；
- 先给判断，再拆机制和边界；
- 技术概念落到目录、命令、权限、升级与回滚；
- 结尾给少量可执行动作，不做机械总结。

不得移植刘小排的亲测、朋友观点、产品经历或口头禅。

## 十、叙事方案比较

### 方案 A｜规格说明型

结构：发生了什么 → 目录规范 → 兼容客户端 → 未覆盖内容。

优点：准确、信息密度高。  
缺点：容易写成规范翻译，缺少江小北的工程判断。

### 方案 B｜“npm 类比的前半句与后半句”型（推荐）

结构：标题类比 → 先纠偏“还不是完整 npm” → 解释共同包装层 → 风险传播 → 下一层基础设施 → 团队行动。

优点：标题与正文冲突明确，既能讲清技术，也能自然落到供应链、安全和程序员影响。  
缺点：需要严格控制类比边界，避免读者误以为已有统一 registry/installer。

### 方案 C｜团队迁移清单型

结构：一个团队如何拆出 portable core → client extension → 权限/依赖/测试基线。

优点：实操性强。  
缺点：会弱化这次标准出现的生态意义，也容易在未经实测的情况下写得过细。

推荐采用方案 B，并吸收方案 A 的规范事实和方案 C 的最后三项行动建议。

## 十一、图片候选（阶段一仅记录，不下载）

### IMG-CANDIDATE-01｜官方“多客户端包装分叉与漂移”图

- 用途：解释 Skills/MCP 本身可复用，但外层 manifest 与目录导致多份包装漂移；
- 来源：Google Developers Blog，图名 `agent-plugins-figure-fork-and-drift`；
- 来源页面：https://developers.googleblog.com/en/agent-plugins-package-your-skills-tools-and-more/
- 优先级：高；官方图，阶段三核对原图链接与许可说明。

### IMG-CANDIDATE-02｜官方“不是每个 Skill 都需要做成 Plugin”图

- 用途：强调插件适用于需要共同迁移的一组组件，避免把单个 Skill 过度包装；
- 来源：Google Developers Blog，图名 `agent-plugins-figure-not-every-skill`；
- 来源页面：同上；
- 优先级：中。

### IMG-CANDIDATE-03｜官方生态分层图

- 用途：展示 Find（ARD）→ Describe（AI Catalog）→ Package（Agent Plugins）→ Run（MCP/Skills）；
- 来源：Google Developers Blog，图名 `agent-plugins-figure-ecosystem-layers`；
- 来源页面：同上；
- 优先级：高。

### IMG-CANDIDATE-04｜原创“Agent Plugin 风险传播链”信息图

- 用途：`SKILL.md 指令 + scripts + MCP 进程/远程服务 → Agent 权限 → 文件/网络/凭据`；
- 形式：黑白灰流程图；
- 优先级：高；若阶段三没有更合适的官方图，再制作。

### IMG-CANDIDATE-05｜原创“完整 npm 生态 vs Agent Plugins 1.0.0”对比图

- 用途：左侧已标准化包格式，右侧待补注册、锁定、签名、权限、沙箱、审计；
- 优先级：高；适合作为文章核心判断图。

## 十二、正文中的事实边界

必须保留的限定：

- “1.0.0”不等于成熟稳定生态；规范页仍标记 Working Draft；
- “兼容客户端”不等于组件和 transport 全量兼容；
- 路径 containment 不等于进程 sandbox；
- SemVer 是建议，`version` 不是最小 manifest 的必填字段；
- SBOM、签名、provenance、lockfile 是建议和相邻项目实践，不是 v1 已提供功能；
- 学术论文是预印本研究，不作为所有客户端都不安全的普遍结论；
- 不使用中文平台文章中的未经原始材料核验的安全统计数据。

禁止写法：

- “Agent 插件已经实现一次开发、任何客户端无差别运行”；
- “Google 与五家公司共同发布了 1.0.0”（更准确：原 TSC 发布，Google 8 月 6 日宣布加入）；
- “plugin.json 会声明插件需要的所有权限”；
- “安装 Agent Plugin 会自动执行所有脚本”；
- “Agent Plugins 已有统一官方商店、依赖解析和审计工具”；
- “我实测发现……”或任何未经用户提供的亲身经历。

## 十三、建议篇幅与信息密度

- 建议正文：2400～2800 字；
- 文章类型：技术观点文；
- 技术细节：保留一个目录示例和一张层次表，不逐字段翻译规范；
- 行动建议：控制为三项，每项说明目标、动作和边界；
- 结尾：落在“把 Agent Plugin 当依赖，而不是当 Prompt 收藏夹”。
