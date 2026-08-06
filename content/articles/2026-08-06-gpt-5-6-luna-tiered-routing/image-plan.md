# 配图计划：GPT-5.6 Luna 降价与 Agent 分层路由

> 目标公众号：AI自由圈
>
> 正文长度：1389 个汉字（不含标题和参考资料）
>
> 规划：封面 1 张；正文 3 张
> 视觉策略：浅色背景、单一钴蓝强调色、信息卡片感。正文全部使用原创信息图，避免过期网页截图和第三方转载风险。

## 图片搜索与选择结论

- 已使用中英文关键词搜索 OpenAI 官方页面和公开图片，未找到能准确同时呈现 7 月 30 日新价格、步骤级路由与“合格结果总成本”的可直接复用图片。
- OpenAI 官方公告可作为价格事实来源，但页面截图会混入导航、引述和与正文无关的信息，手机端信息效率较低。
- 因此不下载网络图片；正文三张图均由 Gstack 根据已核验事实和终稿观点制作。`assets/source-images/` 保留为空目录。
- 本篇没有需要标记为“待人工审阅”的网络图片。

## COVER｜公众号封面

- 文章位置：公众号封面，不插入正文。
- 用途：用三档算力卡片、路由线和质量门表达“便宜模型处理规模，强模型处理不确定性”。
- 文件：`assets/generated-images/cover.png`
- 固定模板：`content/templates/ai-free-circle-cover.svg`
- 尺寸：1080×1440，3:4。
- 生成方式：内置 `image_gen` 生成无文字底图；栏目、主题关键词、两行标题和页脚使用本地 SVG 确定性排版。
- 封面标题：`Luna 降价 80%` / `Agent 要改分层路由`
- 主题关键词：`GPT-5.6 · 成本优化`
- 最终提示词：

```text
Use case: stylized-concept
Asset type: portrait WeChat public-account cover background, strict 3:4 composition
Primary request: create an original minimalist editorial technology illustration for an article about GPT-5.6 Luna price reduction and tiered model routing in AI agents
Scene/backdrop: clean warm-white to very light cool-gray background, no physical room and no people
Subject: three abstract processing cards or compute layers of different visual weight, connected by one precise routing line into a validation gate; the lightest low-cost layer handles many small repeated task tiles, while a compact premium layer handles one ambiguous branching node
Style/medium: restrained modern editorial illustration, information-card aesthetic, crisp geometric forms, subtle paper texture, flat 2.5D at most
Composition/framing: portrait 3:4; reserve the upper 48% as generous quiet negative space for Chinese headline to be added later; place the routing visual primarily in the lower half; strong mobile thumbnail silhouette; safe margins on all sides
Lighting/mood: bright, clear, analytical, trustworthy
Color palette: warm white, pale gray, charcoal text-like marks, one cobalt-blue accent only
Materials/textures: matte paper cards, fine technical grid, precise thin routing lines and small validation check nodes
Constraints: no text, no letters, no numbers, no logos, no watermark; no recognizable brand UI; no robot; no human; no neon; no dark cyberpunk environment; no generic AI brain; no glowing sci-fi effects
Avoid: marketing poster look, busy background, excessive 3D, gradients with saturated colors, illegible pseudo-text
```

- 来源平台：原创生成。
- 来源页面：本文终稿和 `content/style/ai-free-circle-image-style.md`。
- 原始链接：不适用。
- 作者：Gstack。
- 是否带水印：否。
- 处理状态：正常。

## IMAGE-01｜GPT-5.6 新价格对比

- 文章位置：开头价格事实之后、“单价低，不等于任务成本低”之前。
- 用途：直观展示 Luna、Terra、Sol 的当前标准输入 / 输出价和降幅，突出 1/25 的价格杠杆。
- 文件：`assets/generated-images/price-comparison.png`
- 可编辑源文件：`assets/generated-images/price-comparison.svg`
- 来源平台：原创信息图。
- 来源页面：https://openai.com/index/advancing-the-price-performance-frontier-with-gpt-5-6/
- 原始链接：不适用；图中数据根据官方公告重新排版。
- 作者：Gstack。
- 是否带水印：否。
- 处理状态：正常。

## IMAGE-02｜步骤级分层路由

- 文章位置：正文路由文本图之后、质量门说明之前。
- 用途：解释任务分类、三档模型、质量门、升级与人工接管之间的关系，并提醒路由不是固定选型表。
- 文件：`assets/generated-images/tiered-routing.png`
- 可编辑源文件：`assets/generated-images/tiered-routing.svg`
- 来源平台：原创信息图。
- 来源页面：本文 `final.md`；事实依据映射见 `sources.md`。
- 原始链接：不适用。
- 作者：Gstack。
- 是否带水印：否。
- 处理状态：正常。

## IMAGE-03｜合格结果总成本

- 文章位置：“别只盯着 Token 账单”小节末尾、“先用五步做一次小改造”之前。
- 用途：把模型、工具、重试、人工复核、失败代价、质量和时延放进同一成本账本。
- 文件：`assets/generated-images/qualified-result-cost.png`
- 可编辑源文件：`assets/generated-images/qualified-result-cost.svg`
- 来源平台：原创信息图。
- 来源页面：本文 `final.md`。
- 原始链接：不适用。
- 作者：Gstack。
- 是否带水印：否。
- 处理状态：正常。

## 人工发布前检查

- 微信编辑器上传时使用本地文件，不依赖网页热链。
- 封面上传后检查两行标题在会话列表缩略图中的可读性。
- 正文图片保持原比例，不拉伸；价格变动后发布时应重新核对 IMAGE-01。
- 所有图片无水印、无第三方素材，不需要转载授权审阅。
