# 只改 Prompt 不够了：Coding Agent 开始把测试结果变成训练信号

过去我们讨论 Coding Agent，常常盯着三个地方：模型够不够强、Prompt 写得好不好、工具装得多不多。

8 月 5 日，Hugging Face 社区公开了一条不同的路线：把 TRL、OpenEnv 和 OpenCode 接在一起，让 Coding Agent 在隔离沙箱中运行完整工具循环，再把真实轨迹和隐藏测试奖励送回训练器。

官方用 Qwen3-8B 跑了 32 道 DeepCoder 题目，共训练 10 步，平均奖励从约 0.27 上升到 0.71。曲线有明显波动，实验规模也很小，所以这个数字不能证明模型已经学会真实软件工程。它真正证明的是：Agent 执行、结果验证和模型更新这条链已经能闭合。

## 把 Coding Agent 真正做过的事送回训练器

传统的 Agent 强化学习，往往由训练器自己控制交互：生成一轮，解析工具调用，执行工具，再把结果喂给模型。上线时，模型却运行在另一套 Harness 里，要面对终端、文件系统、命令失败和多轮修复。

训练的是一套近似循环，部署的是另一套真实循环。中间存在结构错位。

这次方案采用的是 loop-owning 模式，循环控制权交给 OpenCode：

1. 每次 rollout 启动一个独立沙箱；
2. OpenCode 自己决定何时读文件、改代码、执行命令和继续修复；
3. 中间的透明代理记录模型实际生成的 token、logprob 和消息轨迹；
4. 隐藏测试检查最终工作区，返回结果奖励；
5. TRL 的 AsyncGRPO 再根据同组结果更新模型。

这里的 Harness，可以理解为包在模型外面的工作系统。它负责组织上下文、调用工具、管理多轮执行。过去它主要决定 Agent 上线后怎么干活；现在，它开始同时生成模型训练时要学习的轨迹。

## 为什么这比再装一个工具更值得关注

给 Agent 新增搜索、终端或代码编辑工具，只改变它运行时能做什么，并不会自动改变模型参数。这次不同，Agent 在真实 Harness 里采取了哪些行动、最后有没有通过验证，会反过来影响模型以后更倾向于怎么行动。

验证器的角色也变了。测试过去主要用来拦截错误，现在还可能成为训练目标的一部分。团队提供什么任务、工具和通过标准，模型就会从什么反馈里学习。

这不是 Hugging Face 的全球首创。7 月公开的 OpenForgeRL 已经展示了用代理层和远程容器训练真实 Harness。Hugging Face 这次的价值，更像是把 OpenCode、OpenEnv 和 TRL 整理成一条具体的开源配方，让更多人能复现和拆解。

如果这个方向继续发展，团队真正难复制的资产，可能不只是基础模型，而是自己的任务分布、工具链、验证器和失败轨迹。这些数据更接近团队每天真实发生的软件工作。

## 奖励上涨，不等于学会软件工程

这条路线现在仍然很早期。

首先，32 道题和 10 个训练步骤只够观察链路能否运行，远远不够判断泛化。DeepCoder-Preview 主要是竞赛编程任务，也不是大型企业代码仓库。

其次，官方还披露了另一次 Qwen3-4B 远程实验。奖励上升几步后发生坍塌，Agent 开始重复调用工具却没有解题。作者没有确认原因，只提出训练太短、异步延迟、沙箱失败和模型较小等可能性。

工具本身也没有生产就绪。相关 TRL 能力还在 `experimental`，OpenEnv 官方仓库明确提示项目处于早期阶段，Bug、功能不完整和接口变化都可能发生。

更需要警惕的是验证器。模型优化的是“验证器能看见的成功”，不一定是真实业务想要的成功。测试覆盖不足时，Agent 可能学会让测试变绿，却忽略权限、安全、性能回退和后续维护。

环境失败也会污染奖励。沙箱没启动、Agent 崩溃、验证超时，如果都被记成解题失败，模型收到的反馈就不准确。因此，失败归因不是附属的运维工作，而是训练质量的一部分。

## 谁适合现在试一试

适合做小规模实验的，是那些能够控制开源模型和推理服务、有重复且可验证的垂直任务，并且已经积累测试、构建脚本和隔离环境的团队。他们可以先选一小类任务，观察奖励提升是否能迁移到未见样本，再决定要不要扩大投入。

对大多数使用托管式 Coding Agent 的程序员，现在没有必要搭一套强化学习集群。更现实的做法是先把手头工作变得可验证：

- 给任务写清楚完成条件和失败条件；
- 补齐单元测试、集成测试和静态检查；
- 让 Agent 在隔离环境中运行，保留命令、日志和补丁轨迹；
- 把失败分成代码、工具、环境和需求问题。

这些工作即使不用于训练，也会立刻改善 Coding Agent 的可靠性。没有稳定的验证器，直接训练模型，很可能只是把原有标准里的漏洞放大。

这次实验没有证明 Coding Agent 已经会持续“自我进化”。它只是把一个方向变得具体：模型在真实工具链里执行任务，系统验证结果，再用这段轨迹更新模型。

对多数团队来说，第一步不是马上跑 GRPO，而是先让“完成”成为一个可以可靠判断、反复复现的工程事实。

## 参考资料

1. Hugging Face：[Training a coding agent using the OpenCode harness in remote HF sandboxes with TRL and OpenEnv](https://huggingface.co/blog/sergiopaniego/trl-openenv-harness-training)
2. Hugging Face TRL Docs：[OpenEnv Integration for Training LLMs with Environments](https://huggingface.co/docs/trl/main/openenv)
3. Hugging Face TRL：[OpenCode HF Sandbox 示例](https://github.com/huggingface/trl/blob/main/examples/scripts/openenv/opencode_hf_sandbox.py)
4. Hugging Face OpenEnv：[OpenCode Environment](https://huggingface.co/docs/openenv/environments/opencode)
5. Hugging Face Datasets：[DeepCoder-Preview-Dataset](https://huggingface.co/datasets/agentica-org/DeepCoder-Preview-Dataset)
6. Yu 等：[OpenForgeRL: Train Harness-native Agents in Any Environment](https://arxiv.org/abs/2607.21557)
7. Luo 等：[Training Long-Context, Multi-Turn Software Engineering Agents with Reinforcement Learning](https://arxiv.org/abs/2508.03501)
