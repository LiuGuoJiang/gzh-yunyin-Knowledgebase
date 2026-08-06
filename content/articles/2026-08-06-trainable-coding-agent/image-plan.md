# 配图计划：Coding Agent 开始把测试结果变成训练信号

> 目标公众号：AI自由圈  
> 正文长度：约 1835 个可见字符（不含参考资料）  
> 规划：封面 1 张；正文 4 张  
> 视觉策略：2 张 Hugging Face 官方事实图 + 2 张原创信息图。网络图片保持原貌，转载权限不明确时按规则标记人工审阅。

## COVER｜公众号封面

- 文章位置：公众号封面，不插入正文。
- 用途：用“代码工作区—终端—验证—训练更新”的闭环视觉表达 Coding Agent 在真实 Harness 中执行、验证并学习。
- 文件：`assets/generated-images/cover.png`
- 无文字底图：`assets/generated-images/cover-art.png`
- 确定性排版稿：`assets/generated-images/cover.svg`
- 尺寸：1080×1440，3:4。
- 生成方式：内置 `image_gen` 生成无文字底图；中文标题、栏目标签和主题关键词采用本地 SVG 确定性排版，再导出 PNG。
- 封面文字：
  - 栏目：`AI自由圈｜技术前沿`
  - 引导语：`只改 Prompt 不够了`
  - 主标题：`Coding Agent / 开始“边做边学”`
  - 主题关键词：`真实 Harness × 强化学习`
- 最终提示词：

```text
Use case: stylized-concept
Asset type: portrait WeChat public-account cover background, exact 3:4 composition
Primary request: an original minimalist editorial technology visual for a Coding Agent learning from real tool use and test feedback; show a clean feedback loop made of four connected abstract modules: code workspace, terminal actions, verification check, and training update, with one continuous cobalt-blue signal line returning to the start
Scene/backdrop: very light warm gray to white background, no physical environment, no people
Style/medium: refined flat editorial illustration with subtle paper texture, information-card aesthetic, crisp architectural linework, modern open-source engineering mood
Composition/framing: strict portrait 3:4; reserve the upper-left and center-left 58% as calm negative space for a two-line Chinese title to be added later; concentrate the feedback-loop visual in the lower-right and bottom third; clear mobile thumbnail silhouette; generous safe margins
Lighting/mood: bright, calm, analytical, trustworthy
Color palette: warm white, very light gray, charcoal, and one single cobalt-blue accent; no other saturated colors
Materials/textures: matte paper, thin technical grid, precise nodes, restrained code-bracket and checkmark motifs
Constraints: no text, no letters, no numbers, no pseudo-text, no logos, no watermark; no recognizable product UI; no human figure; no robot; no AI brain; no neon; no cyberpunk city; no glowing sci-fi effects
Avoid: marketing poster look, circuit-board cliché, busy background, excessive 3D, gradients with strong saturation
```

- 是否带水印：否。
- 处理状态：正常。

## IMAGE-01｜Qwen3-8B 奖励曲线

- 文章位置：开头实验数字与边界说明之后。
- 用途：展示官方短实验中平均奖励约从 0.27 升至 0.71，同时保留明显波动，帮助读者理解“链路闭合”与“能力泛化”之间的边界。
- 文件：`assets/source-images/hf-qwen3-8b-reward-curve.png`
- 来源平台：Hugging Face Community Blog。
- 来源页面：https://huggingface.co/blog/sergiopaniego/trl-openenv-harness-training
- 原始链接：https://cdn-uploads.huggingface.co/production/uploads/61929226ded356549e20c5da/uMe3VteaTOlfsJGNTLrFV.png
- 作者：Sergio Paniego（来源文章作者）。
- 是否带水印：否；图例含官方实验运行标识。
- 处理说明：保持原图全部内容与比例，不裁剪、不改色。
- 处理状态：待人工审阅（官方博客图片的公众号转载授权需人工确认）。

## IMAGE-02｜真实 Harness 训练链路

- 文章位置：loop-owning 五步流程之后。
- 用途：直观展示 vLLM policy、OpenCode、透明代理、验证器和 TRL AsyncGRPO 之间的模型调用、轨迹、奖励与权重同步关系。
- 文件：`assets/source-images/hf-real-harness-training-pipeline.png`
- 来源平台：Hugging Face Community Blog。
- 来源页面：https://huggingface.co/blog/sergiopaniego/trl-openenv-harness-training
- 原始链接：https://cdn-uploads.huggingface.co/production/uploads/61929226ded356549e20c5da/V-2Ggmf_RLKwT8z2gUB5J.png
- 作者：Sergio Paniego（来源文章作者）。
- 是否带水印：否；图中保留 TRL、OpenEnv、OpenCode 和 vLLM 标识。
- 处理说明：保持原图全部内容与比例，不裁剪、不覆盖产品标识。
- 处理状态：待人工审阅（官方博客图片的公众号转载授权需人工确认）。

## IMAGE-03｜验证器边界

- 文章位置：“奖励上涨，不等于学会了软件工程”小节中，验证器说明之后。
- 用途：对比验证器通常能观察的测试、运行和静态检查，与它可能漏掉的安全、性能、隐性需求和维护成本。
- 文件：`assets/generated-images/verifier-boundary.png`
- 可编辑源文件：`assets/generated-images/verifier-boundary.svg`
- 来源平台：原创信息图。
- 来源页面：本文 `final.md` 与 `sources.md`。
- 原始链接：不适用。
- 作者：Gstack。
- 是否带水印：否。
- 处理状态：正常。

## IMAGE-04｜谁值得训练自己的 Coding Agent

- 文章位置：“谁值得现在试一试”小节的行动清单之后。
- 用途：把读者分为“适合小规模实验的团队”和“应先提高可控性的大多数开发者”，给出清晰的行动分流。
- 文件：`assets/generated-images/who-should-train.png`
- 可编辑源文件：`assets/generated-images/who-should-train.svg`
- 来源平台：原创信息图。
- 来源页面：本文 `final.md`。
- 原始链接：不适用。
- 作者：Gstack。
- 是否带水印：否。
- 处理状态：正常。

## 人工发布前检查

- 确认 IMAGE-01、IMAGE-02 的公众号转载权限；若不采用，可用本文已有文字说明与原创图替换，不影响文章结论。
- 微信编辑器上传时使用本地文件，不依赖网页热链。
- 封面上传后检查两行主标题在列表缩略图中的可读性。
- 正文图片保持原比例，不拉伸；官方图的来源说明与实验边界图注不得删除。
