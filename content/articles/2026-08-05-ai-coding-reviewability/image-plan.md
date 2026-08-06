# 配图计划：AI Coding 的新瓶颈——让代码可审查

> 目标公众号：AI架构师江小北  
> 正文长度：约 2455 个汉字（不含参考资料）  
> 规划：封面 1 张；正文 4 张  
> 视觉策略：2 张官方事实图 + 2 张原创工程信息图。网络图保持原貌，转载权限不明确时按规则标记人工审阅。

## COVER｜公众号封面

- 文章位置：公众号封面，不插入正文。
- 用途：把“巨型代码变更 → 可审查的小变更”表达为从单体代码块分解出的四层审查卡片。
- 文件：`assets/generated-images/cover.png`
- 中间底图：`assets/generated-images/cover-art.png`
- 尺寸：1080×1440，3:4。
- 生成方式：内置 `image_gen` 生成无文字底图；中文标题、栏目标签和底部署名采用本地确定性排版。
- 最终提示词：

```text
Use case: stylized-concept
Asset type: portrait WeChat public-account cover background, 3:4 aspect ratio
Primary request: an original minimalist visual metaphor for AI-generated code becoming a review bottleneck; a large dense monolithic code-diff slab at the lower right breaks into four smaller stacked review cards connected by precise dependency lines and check nodes
Scene/backdrop: deep matte charcoal-to-black background with subtle paper grain, no environment and no people
Style/medium: restrained editorial technology illustration, clean architectural linework, premium but sober, mostly flat with very subtle depth
Composition/framing: strict portrait 3:4; reserve the upper-left and center-left 60% as quiet negative space for a two-line Chinese headline that will be added later; visual system concentrated in the lower-right and bottom third; strong mobile thumbnail silhouette
Lighting/mood: calm, analytical, trustworthy, low-key contrast
Color palette: black, white, graphite gray, very limited muted silver; no saturated accent colors
Materials/textures: matte paper, fine technical grid, precise thin lines, understated code-review symbols and branching graph geometry
Constraints: no text, no letters, no numbers, no logos, no watermark; no recognizable brand UI; no human figure; no robot; no neon; no cyberpunk city; no glowing sci-fi effects; leave generous safe margins on all sides
Avoid: marketing poster look, generic AI brain, circuit-board cliché, busy background, illegible pseudo-text, excessive 3D
```

- 是否带水印：否。
- 处理状态：正常。

## IMAGE-01｜巨型 PR 的体量

- 文章位置：开头事实案例之后，“新瓶颈不是产码”小节之前。
- 用途：直接展示 GitHub 教程示例中的 1,535 行新增、186 行删除和 33 个文件，帮助读者感受评审负担。
- 插入文件：`assets/source-images/github-pr-size-counter-static.png`
- 保留原图：`assets/source-images/github-pr-size-counter.gif`
- 来源平台：GitHub Blog。
- 来源页面：https://github.blog/engineering/turn-one-giant-ai-generated-pull-request-to-a-reviewable-stack/
- 原始链接：https://github.blog/wp-content/uploads/2026/08/pr-size-counter.gif
- 作者：Julia Muiruri（来源文章作者）。
- 是否带水印：否。
- 处理说明：正文使用原 GIF 最后一帧的等比例静态 PNG，未裁剪、未去水印；原始 120 帧 GIF 同时保留。
- 处理状态：待人工审阅（官方博客图片的公众号转载授权需人工确认）。

## IMAGE-02｜Stacked sessions 的依赖关系

- 文章位置：GitHub stacked sessions 案例之后、四层 stacked PR 文本图之前。
- 用途：展示一次前端现代化任务被拆成前后依赖 session 的实际界面关系。
- 文件：`assets/source-images/github-stacked-sessions.png`
- 来源平台：GitHub Blog。
- 来源页面：https://github.blog/ai-and-ml/github-copilot/stacked-sessions-and-pull-requests-in-the-github-copilot-app/
- 原始链接：https://github.blog/wp-content/uploads/2026/07/608818417-096042e4-9ace-4575-877d-a18926371bc2.png
- 作者：Cassidy Williams（来源文章作者）。
- 是否带水印：否。
- 处理说明：保持原图比例和全部界面内容，不裁剪。
- 处理状态：待人工审阅（官方博客图片的公众号转载授权需人工确认）。

## IMAGE-03｜确定性程序与 LLM Agent 分工

- 文章位置：OpenCodeReview 分工表之后。
- 用途：把表格中的职责边界压缩成手机端易读的两栏信息图，并补出人工最终批准这一责任门。
- 文件：`assets/generated-images/review-division.png`
- 来源平台：原创信息图。
- 来源页面：本文 `final.md` 与 `sources.md` 中的 OpenCodeReview 架构事实。
- 原始链接：不适用。
- 作者：Gstack。
- 是否带水印：否。
- 处理状态：正常。

## IMAGE-04｜Agent 时代 PR 四原则

- 文章位置：“Agent 时代，PR 至少要守住四条原则”小节末尾、职责分离引用之前。
- 用途：汇总单一关注点、依赖显式、逐层验证、责任不外包，并突出高风险变更的人类责任门。
- 文件：`assets/generated-images/pr-four-principles.png`
- 来源平台：原创信息图。
- 来源页面：本文 `final.md`。
- 原始链接：不适用。
- 作者：Gstack。
- 是否带水印：否。
- 处理状态：正常。

## 未采用候选

- `assets/source-images/opencodereview-highlights-zh.png`：官方图主要展示用户数、采纳率、任务量、Token 成本和 benchmark 等项目方自报指标，与终稿主动弱化营销数字的事实边界冲突，因此不插入正文。

## 人工发布前检查

- 确认 IMAGE-01、IMAGE-02 的公众号转载权限；若不采用，可用正文已有文字图与原创依赖图替换，不影响文章结论。
- 微信编辑器上传时使用本地文件，不依赖网页热链。
- 封面上传后检查两行标题在列表缩略图中的可读性。
- 正文图片保持原比例，不拉伸；图片说明保留来源平台。
