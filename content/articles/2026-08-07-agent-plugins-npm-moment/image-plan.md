# 配图计划：Agent 的“npm 时刻”来了，但真正的坑才刚开始

> 目标公众号：AI架构师江小北  
> 正文长度：约 2660 字（不含参考资料）  
> 规划：封面 1 张；正文 4 张  
> 视觉策略：2 张 Google 官方事实图 + 2 张原创工程信息图。网络图片保持原貌，转载权限不明确时按规则标记人工审阅。

## COVER｜公众号封面

- 文章位置：公众号封面，不插入正文。
- 用途：用“可移植插件包 → 验证门 → 多客户端”的关系表达统一包装与供应链责任同时出现。
- 文件：`assets/generated-images/cover.png`
- 无文字底图：`assets/generated-images/cover-art.png`
- 确定性排版稿：`assets/generated-images/cover.svg`
- 尺寸：1080×1440，3:4。
- 生成方式：内置 `image_gen` 生成无文字底图；中文标题、栏目标签和主题关键词采用本地 SVG 确定性排版，再导出 PNG。
- 封面文字：
  - 栏目：`AI思考`
  - 主题：`AGENT PLUGINS · SUPPLY CHAIN`
  - 主标题：`Agent 的“npm 时刻” / 真正的坑才刚开始`
  - 关键词：`包格式 × 供应链`
  - 底部：`TECH INSIGHT｜2026`
- 最终提示词：

```text
Use case: stylized-concept
Asset type: portrait WeChat public-account cover background, strict 3:4 aspect ratio
Primary request: an original minimalist editorial technology visual about portable Agent Plugins becoming a software-supply-chain risk; show a precise modular package made of three stacked architectural layers, with a folder-like outer shell, two component cards, connector lines, and a guarded execution boundary represented by a restrained lock-and-gate motif
Scene/backdrop: deep matte charcoal to black background with subtle paper grain and a faint technical grid; no physical environment and no people
Subject: one abstract portable plugin package in the lower-right and bottom half, assembled from clean cards and nodes; the package connects to several small client endpoints but passes through a visible verification gate before reaching them
Style/medium: sober premium editorial technology illustration, clean architectural linework, mostly flat with very subtle isometric depth
Composition/framing: strict portrait 3:4; reserve the upper-left and center-left 58% as calm negative space for a two-line Chinese headline added later; concentrate the modular package and verification gate in the lower-right and bottom half; strong silhouette at mobile thumbnail size; generous safe margins
Lighting/mood: calm, analytical, trustworthy, restrained
Color palette: black, graphite gray, white, muted silver; one very small amber warning accent only at the verification gate
Materials/textures: matte paper, brushed graphite, precise thin lines, restrained dependency-graph geometry
Constraints: no text, no letters, no numbers, no pseudo-text, no logos, no watermark; no recognizable brand UI; no human figure; no robot; no AI brain; no npm logo; no neon; no cyberpunk city; no glowing sci-fi effects
Avoid: marketing poster look, generic circuit-board cliché, busy background, excessive 3D, shiny plastic, large saturated areas
```

- 是否带水印：否。
- 处理状态：正常。

## IMAGE-01｜多客户端包装分叉与漂移

- 文章位置：开头介绍多客户端重复包装之后、解释“npm 时刻”边界之前。
- 用途：展示同一组 `SKILL.md` 与 `mcp.json` 被复制进不同客户端包装后产生漂移。
- 文件：`assets/source-images/google-agent-plugins-fork-and-drift.jpg`
- 来源平台：Google Developers Blog。
- 来源页面：https://developers.googleblog.com/en/agent-plugins-package-your-skills-tools-and-more/
- 原始链接：https://storage.googleapis.com/gweb-developer-goog-blog-assets/images/agent-plugins-figure-fork-and-drift.original.jpg
- 作者：Kevin Hou、Haoyu Wang、Alan Blount（来源文章作者）。
- 是否带水印：否。
- 处理说明：保持 1600×893 原图比例与全部英文标注，不裁剪、不改色。
- 处理状态：待人工审阅（官方博客图片的公众号转载授权需人工确认）。

## IMAGE-02｜Skills、MCP 与 Agent Plugin 三层分工

- 文章位置：“有了 Skills 和 MCP，为什么还需要 Plugin？”小节末尾。
- 用途：把“怎样做事、怎样连接、怎样交付”三层关系压缩成手机端易读的信息图，并强调 Plugin 不替代前两层执行协议。
- 文件：`assets/generated-images/skills-mcp-plugin-layers.png`
- 可编辑源文件：`assets/generated-images/skills-mcp-plugin-layers.svg`
- 来源平台：原创信息图。
- 来源页面：本文 `final.md` 与 `sources.md`。
- 原始链接：不适用。
- 作者：Gstack。
- 是否带水印：否。
- 处理状态：正常。

## IMAGE-03｜Find、Describe、Package、Run 四层生态

- 文章位置：“1.0.0 标准化了什么，又没管什么？”小节末尾。
- 用途：说明 Agent Plugins 只负责 Package，发现、描述与执行可以独立采用，避免把统一包格式误读成完整包管理生态。
- 文件：`assets/source-images/google-agent-plugins-ecosystem-layers.jpg`
- 来源平台：Google Developers Blog。
- 来源页面：https://developers.googleblog.com/en/agent-plugins-package-your-skills-tools-and-more/
- 原始链接：https://storage.googleapis.com/gweb-developer-goog-blog-assets/images/agent-plugins-figure-ecosystem-layers.original.jpg
- 作者：Kevin Hou、Haoyu Wang、Alan Blount（来源文章作者）。
- 是否带水印：否。
- 处理说明：保持 1600×893 原图比例与全部英文标注，不裁剪、不改色。
- 处理状态：待人工审阅（官方博客图片的公众号转载授权需人工确认）。

## IMAGE-04｜进入生产环境前的五道门

- 文章位置：“离真正的‘npm 时刻’，还差五层”小节五个问题之后。
- 用途：汇总来源、成分、版本、权限和审计五项准入检查，突出“格式解决可移植性，治理决定能否进生产”。
- 文件：`assets/generated-images/five-supply-chain-gates.png`
- 可编辑源文件：`assets/generated-images/five-supply-chain-gates.svg`
- 来源平台：原创信息图。
- 来源页面：本文 `final.md`。
- 原始链接：不适用。
- 作者：Gstack。
- 是否带水印：否。
- 处理状态：正常。

## 人工发布前检查

- 确认 IMAGE-01、IMAGE-03 的公众号转载权限；若不采用，可用本文已有文字说明与原创图替换，不影响文章结论。
- 微信编辑器上传时使用本地文件，不依赖网页热链。
- 封面上传后检查两行主标题在列表缩略图中的可读性。
- 正文图片保持原比例，不拉伸；Google 官方图的来源图注不得删除。
- 原创信息图使用可编辑 SVG 与导出 PNG 双份保存，发布时使用 PNG。
