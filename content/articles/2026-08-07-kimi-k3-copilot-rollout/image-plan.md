# 配图计划：Kimi K3 进 Copilot，当天暂停又恢复

> 目标公众号：AI自由圈  
> 正文长度：约 1520 个汉字（不含参考资料）  
> 规划：封面 1 张；正文 3 张  
> 视觉策略：1 张 GitHub 官方公告图 + 2 张原创信息图。网络图片保持原貌，转载权限不明确时按规则标记人工审阅。

## COVER｜公众号封面

- 文章位置：公众号封面，不插入正文。
- 用途：用五层系统卡片、连续信号线和一个短暂停顿节点，表达 Kimi K3 接入 Copilot 后仍依赖托管、编排和执行链路。
- 文件：`assets/generated-images/cover.png`
- 无文字底图：`assets/generated-images/cover-art.png`
- 确定性排版稿：`assets/generated-images/cover.svg`
- 尺寸：1080×1440，3:4。
- 生成方式：内置 `image_gen` 生成无文字底图；中文标题、栏目标签和主题关键词采用本地 SVG 确定性排版，再导出 PNG。
- 封面文字：
  - 栏目：`AI自由圈｜模型观察`
  - 引导语：`上线・暂停・恢复`
  - 主标题：`Kimi K3 进 Copilot / AI 编程拼整条链路`
  - 主题关键词：`模型 × 托管 × Actions`
- 最终提示词：

```text
Use case: stylized-concept
Asset type: portrait WeChat public-account cover background, exact 3:4 composition
Primary request: create an original minimalist editorial technology visual about an AI coding model entering a developer platform while the execution chain briefly pauses and resumes; show five stacked abstract system layers connected by one cobalt-blue signal path, with a single small amber interruption node that reconnects downstream, expressing model, inference hosting, orchestration, automation execution, and developer client without words
Scene/backdrop: warm white to very light gray background, no physical environment, no people
Style/medium: refined flat editorial illustration, subtle matte paper texture, information-card aesthetic, crisp architectural linework
Composition/framing: strict portrait 3:4; reserve the upper-left and center-left 60% as calm negative space for a two-line Chinese title to be added later; concentrate the layered system visual in the lower-right and bottom third; generous safe margins; strong mobile thumbnail silhouette
Lighting/mood: bright, calm, analytical, trustworthy
Color palette: warm white, very light gray, charcoal, one cobalt-blue accent #1F5EFF, and only one tiny muted amber status dot
Materials/textures: matte paper, faint technical grid, precise nodes, restrained code-bracket and workflow motifs
Constraints: no text, no letters, no numbers, no pseudo-text, no logos, no watermark; no recognizable product UI; no human figure; no robot; no AI brain; no neon; no cyberpunk city; no glowing sci-fi effects
Avoid: marketing poster look, circuit-board cliché, busy background, excessive 3D, strong saturated gradients
```

- 是否带水印：否。
- 处理状态：正常。

## IMAGE-01｜Kimi K3 进入 GitHub Copilot 官方公告图

- 文章位置：开头说明 rollout 已恢复、且不能把事故归因于 Kimi 之后。
- 用途：确认事件主体是 Kimi K3 进入 Copilot 的 model picker，并为开场提供官方视觉证据。
- 文件：`assets/source-images/github-copilot-kimi-k3-social-card.png`
- 来源平台：GitHub Changelog。
- 来源页面：https://github.blog/changelog/2026-08-06-kimi-k3-is-now-available-in-github-copilot/
- 原始链接：https://github.blog/wp-content/uploads/2026/08/github-copilot-social-card-8.png
- 作者：GitHub。
- 是否带水印：否；保留 GitHub、Kimi K3 和 Copilot 界面标识。
- 处理说明：保持原图全部内容与比例，不裁剪、不改色。
- 处理状态：待人工审阅（官方公告图片的公众号转载授权需人工确认）。

## IMAGE-02｜一次 Copilot 调用的五层链路

- 文章位置：“模型选型正在变成一份运行时合同”小节的五层文字链路之后。
- 用途：解释 Kimi K3 权重、Fireworks AI 托管、Copilot 编排、Actions/Agent 执行和开发入口之间的依赖关系。
- 文件：`assets/generated-images/copilot-runtime-chain.png`
- 可编辑源文件：`assets/generated-images/copilot-runtime-chain.svg`
- 来源平台：原创信息图。
- 来源页面：本文 `final.md` 与 `sources.md`。
- 原始链接：不适用。
- 作者：Gstack。
- 是否带水印：否。
- 处理状态：正常。

## IMAGE-03｜分层降级路径

- 文章位置：多模型与整条链路高可用的区别之后。
- 用途：把模型、平台编排、Actions 执行和事件重放四类故障映射到不同的降级动作。
- 文件：`assets/generated-images/layered-fallback.png`
- 可编辑源文件：`assets/generated-images/layered-fallback.svg`
- 来源平台：原创信息图。
- 来源页面：本文 `final.md`、GitHub Changelog 与 GitHub Status。
- 原始链接：不适用。
- 作者：Gstack。
- 是否带水印：否。
- 处理状态：正常。

## ALT-01｜Kimi K3 官方 Logo（备选，未插入正文）

- 用途：若发布时需要替换 IMAGE-01，可用于制作简化模型信息卡；当前不插入正文。
- 文件：`assets/source-images/kimi-k3-logo.png`
- 来源平台：Moonshot AI 官方 GitHub。
- 来源页面：https://github.com/MoonshotAI/Kimi-K3
- 原始链接：https://raw.githubusercontent.com/MoonshotAI/Kimi-K3/main/assets/kimi-logo.png
- 作者：Moonshot AI。
- 是否带水印：否；包含 Kimi 品牌标识。
- 处理说明：保持原图，不修改品牌图形。
- 处理状态：待人工审阅（品牌图形的公众号使用范围需人工确认）。

## 人工发布前检查

- 确认 IMAGE-01 的公众号转载权限；若不采用，可直接从正文删除该图，不影响文章结论。
- 微信编辑器上传时使用本地文件，不依赖网页热链。
- 封面上传后检查两行主标题在列表缩略图中的可读性。
- 正文图片保持原比例；官方图来源图注、事故归因边界和原创图中的分层关系不得删除。
