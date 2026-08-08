# 配图计划：MCP 删掉 Session 后，Agent 工程开始像真正的分布式系统

> 目标公众号：AI架构师江小北
> 正文长度：约 3200 字（不含参考资料）
> 规划：封面 1 张；正文 4 张
> 视觉策略：2 张 Google 官方事实图 + 2 张原创工程信息图。网络图片保持原貌，转载权限不明确时按规则标记人工审阅。

## 写作风格更新说明

终稿确认没有逐句修改。`content/style/jiangxiaobei-writing-style.md` 仅记录本次再次确认的长期结构偏好：“具体故障切入—状态归属分层—迁移验收清单”；没有从一次无修改确认中推断新的个人口癖。

## COVER｜公众号封面

- 文章位置：公众号封面，不插入正文。
- 用途：用一条被移除的 Session 依赖与五个显式状态去向，表达“无状态不是没有状态”。
- 文件：`assets/generated-images/cover.png`
- 无文字底图：`assets/generated-images/cover-art.png`
- 确定性排版稿：`assets/generated-images/cover.svg`
- 尺寸：1080×1440，3:4。
- 标题来源：`dbs-xhs-title.md` Top 1。
- 生成方式：内置 `image_gen` 以已确认封面作为风格参考生成无文字底图；中文标题、栏目标签和主题关键词采用本地 SVG 确定性排版，再导出 PNG。
- 封面文字：
  - 栏目：`AI思考`
  - 主题：`MCP · STATE OWNERSHIP`
  - 主标题：`关于 MCP，程序员 / 太晚知道的 5 个教训`
  - 关键词：`无状态 × 状态归属`
  - 底部：`TECH INSIGHT｜2026`
- 最终提示词：

```text
Use case: stylized-concept
Asset type: portrait WeChat public-account cover background, strict 3:4 aspect ratio
Primary request: create an original minimalist editorial technology visual about MCP removing a transport-layer Session and redistributing state into explicit cloud-native components
Input images: Image 1 is a style and composition reference only; do not copy its objects or text
Scene/backdrop: deep matte charcoal-to-black background with very subtle paper grain and a faint technical grid, no physical environment
Subject: one central session node or capsule in the lower-right and bottom half cleanly separated into five precise destinations: per-request metadata, business handle, protected request state, durable task, and subscription bus; express these as abstract stacked cards, small nodes, routes, and a load-balancer gateway, with one broken link showing the old sticky-session dependency being removed
Style/medium: sober premium editorial technology illustration, architectural linework, mostly flat with subtle isometric depth, visually compatible with Image 1
Composition/framing: strict portrait 3:4; reserve the upper-left and middle-left 58 percent as calm negative space for a two-line Chinese headline added later; concentrate the architecture in the lower-right and bottom half; strong silhouette at mobile thumbnail size; generous safe margins
Lighting/mood: analytical, calm, trustworthy, restrained
Color palette: black, graphite gray, white, muted silver; one small amber accent only on the removed session link
Materials/textures: matte paper, brushed graphite, precise thin lines, restrained dependency-graph geometry
Constraints: no text, no letters, no numbers, no pseudo-text, no logos, no watermark; no people; no robot; no AI brain; no neon; no cyberpunk city; no glowing sci-fi effects
Avoid: marketing poster look, generic circuit board, busy background, excessive 3D, shiny plastic, large saturated areas
```

- 是否带水印：否。
- 处理状态：正常。

## IMAGE-01｜旧版多轮请求的跨实例上下文问题

- 文章位置：开头核心判断之后，“MCP 到底删掉了什么”之前。
- 用途：展示后续请求经负载均衡落到另一实例时，服务端缺少前一轮上下文。
- 文件：`assets/source-images/google-mcp-session-bound-pods.png`
- 来源平台：Google Developers Blog。
- 来源页面：https://developers.googleblog.com/en/scaling-ai-agent-infrastructure-with-the-mcp-stateless-updates/
- 原始链接：https://storage.googleapis.com/gweb-developer-goog-blog-assets/images/Screenshot_2026-08-03_at_11.42.20AM.original.png
- 作者：Kurtis Van Gent、Alan Blount。
- 是否带水印：否。
- 处理说明：保持 2630×1354 原图比例与全部英文标注，不裁剪、不改色。
- 处理状态：待人工审阅（官方博客图片的公众号转载授权需人工确认）。

## IMAGE-02｜五类状态的显式归属

- 文章位置：“状态去了哪里”小节开头。
- 用途：将协议与鉴权、业务状态、交互中间态、长任务和通知的载体放在同一张图中，避免把“无状态”误读为“没有状态”。
- 文件：`assets/generated-images/state-ownership-map.png`
- 可编辑源文件：`assets/generated-images/state-ownership-map.svg`
- 来源平台：原创信息图。
- 来源页面：本文 `final.md`、`research.md` 与 `sources.md`。
- 原始链接：不适用。
- 作者：Gstack。
- 是否带水印：否。
- 处理状态：正常。

## IMAGE-03｜SEP-2322 的两个自包含请求

- 文章位置：MRTR 与 `requestState` 说明之后。
- 用途：展示服务端返回 `input_required` / `requestState`，客户端补齐信息后以第二个请求继续处理的流程。
- 文件：`assets/source-images/google-mcp-stateless-pods.png`
- 来源平台：Google Developers Blog。
- 来源页面：https://developers.googleblog.com/en/scaling-ai-agent-infrastructure-with-the-mcp-stateless-updates/
- 原始链接：https://storage.googleapis.com/gweb-developer-goog-blog-assets/images/Screenshot_2026-08-03_at_11.51.27AM.original.png
- 作者：Kurtis Van Gent、Alan Blount。
- 是否带水印：否。
- 处理说明：保持 2534×1378 原图比例与全部英文标注，不裁剪、不改色。
- 处理状态：待人工审阅（官方博客图片的公众号转载授权需人工确认）。

## IMAGE-04｜无状态迁移故障注入矩阵

- 文章位置：“迁移前先做五项检查”小节末尾。
- 用途：把轮询切 Pod、MRTR 跨实例、响应流重试、Worker 重启和跨用户重放对应到可验证的工程结果。
- 文件：`assets/generated-images/migration-fault-matrix.png`
- 可编辑源文件：`assets/generated-images/migration-fault-matrix.svg`
- 来源平台：原创信息图。
- 来源页面：本文 `final.md`、`research.md` 与 `sources.md`。
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
