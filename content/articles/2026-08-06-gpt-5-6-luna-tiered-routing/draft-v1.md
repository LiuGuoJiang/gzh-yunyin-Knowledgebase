# GPT-5.6 Luna 降价 80%，真正该改的不是模型，而是 Agent 架构

7 月 30 日，OpenAI 把 GPT-5.6 Luna 的 API 价格下调了 80%。每百万输入 / 输出 Token 的标准价格，从 1 / 6 美元降到 0.20 / 1.20 美元。

Terra 同期降价 20%，新价格是 2 / 12 美元。Sol 标准价格不变，仍为 5 / 30 美元；新增的 Fast mode 最高可达到标准处理的 2.5 倍速度，价格是 2 倍。

以上都是短上下文标准价。超过 272K 输入后会进入长上下文计费，缓存写入、工具调用也可能产生额外费用。

同样的输入、输出 Token 量，Luna 的价格只有 Sol 的 1/25。这个价差已经大到足以改变 Agent 的架构设计。不过，最省钱的做法并不是把默认模型全部换成 Luna。

## 为什么便宜模型不一定带来便宜结果

普通问答可能只调用一次模型，Agent 通常会连续规划、检索、调用工具、执行、验证和总结。每一步都可能再次携带上下文，失败后还会重试。

这意味着模型单价只是成本的一部分。假如规划环节理解错了需求，后续执行再便宜也是浪费；如果低价模型多跑五轮工具、最后还要强模型重做，账单未必更低。涉及发布、付款、删除资源等动作时，一次错误的代价更不能用节省的 Token 抵消。

所以 Agent 应关注的指标是“每个合格结果的总成本”，而不是每百万 Token 的价格。

## 模型选择要下沉到每一个步骤

OpenAI 在公告中给了一个编码工作流示例：先让 Sol 消除不确定性、定义计划，再由 Luna 实现明确修改、编写和运行测试、评估结果。

这个示例很有代表性，但不能机械照抄。OpenAI 同时提醒，不同工作流可能需要不同组合。一个低风险的结构化抽取任务可以直接使用 Luna；日常 RAG 回答和常规业务分析可能更适合 Terra；需求澄清、复杂规划和高风险代码审查则可能需要 Sol。

更实用的路由依据有四个：任务有多大不确定性，错误代价有多高，用户是否在等待，以及结果能否自动验收。

一个最小的分层路由可以这样工作：

```text
任务分类
  ├─ 可预测、可自动验收  → Luna
  ├─ 需要日常综合判断    → Terra
  └─ 高不确定性或高风险  → Sol / Sol Fast
                ↓
              质量门
        通过 / 升级 / 转人工
```

这里的重点不在于接入三个模型，而在于每一步都有验收标准。结构化输出可以校验字段，代码修改可以跑测试，检索回答可以检查引用覆盖。结果没有过线，就升级到更强模型；达到循环上限或触及高风险动作，就转人工。

Fast mode 也应该单独看待。它用更高价格换低延迟，适合用户正在等待的高价值请求。后台批处理为了更快而默认打开 Fast，通常没有必要。

## 账单要从 Token 扩展到完整任务

团队可以用一条简单公式重新记账：

```text
每个合格结果的总成本
=（模型 Token + 工具调用 + 基础设施 + 重试
  + 人工复核 + 失败代价）÷ 通过验收的结果数
```

至少要记录每一步路由到哪个模型，输入、输出和缓存 Token，用了多少次工具，循环、重试和升级了几次，以及自动通过率、人工改写率和 P95 延迟。

缓存也不能只看“命中率”。GPT-5.6 的缓存写入按未缓存输入价格的 1.25 倍收费，只有同一段稳定前缀被后续请求反复读取，才可能形成净节省。

OpenAI 还披露，Sol 参与优化生产 Kernel 后，端到端模型服务成本降低 20%；它设计的推测模型实验让 Token 生成效率提高 15% 以上。这些是 OpenAI 自己的生产结果，不是普通团队可以直接复制的收益。更可借鉴的是它的优化范围：模型之外，请求路由、上下文、缓存、工具输出和重复工作都要一起算。

## 程序员现在可以怎么做

第一步，不要先做一个“万能智能路由器”。选出 3～5 个稳定任务类别，比如结构化抽取、RAG 回答、代码修改和结果总结。

第二步，为每类任务写清验收标准，用同一批真实样本比较 Luna、Terra 和 Sol。除了成功率，也记录总 Token、工具调用、重试和延迟。

第三步，为每类任务选择能够稳定过线的最低成本模型。先用影子模式记录路由建议，不急着切换生产流量。

第四步，加上失败升级、循环上限和人工责任门，再做小流量灰度。便宜模型可以扩大执行规模，但不能扩大权限。

第五步，路由稳定后再优化处理档位和缓存：在线请求看延迟价值，后台任务考虑 Standard，异步或低优先级任务再评估 Batch / Flex。

模型路由会越来越像数据库读写分离。真正有用的能力不是多配置几个模型名称，而是把流量分类、质量门、失败回退和成本观测做成一套稳定机制。

Luna 的 80% 降价，确实让高频、后台和批量型 Agent 更容易算过经济账。它释放出来的更大价值，是让团队有空间把高价智能留给难以判断的部分，把规模交给能够被验证的步骤。

贵模型处理昂贵的不确定性，便宜模型处理可验证的规模。边界画得越清楚，这次降价带来的收益才越真实。

## 参考资料

1. OpenAI：[Advancing the price-performance frontier with GPT-5.6](https://openai.com/index/advancing-the-price-performance-frontier-with-gpt-5-6/)
2. OpenAI Developers：[API Pricing](https://developers.openai.com/api/docs/pricing)
3. OpenAI：[How GPT-5.6 fuses frontier intelligence with frontier efficiency](https://openai.com/index/gpt-5-6-frontier-intelligence-efficiency/)
4. OpenAI Developers：[Fast mode](https://developers.openai.com/api/docs/guides/fast-mode)
5. OpenAI Developers：[Prompt caching](https://developers.openai.com/api/docs/guides/prompt-caching)
6. OpenAI Developers：[Evaluation best practices](https://developers.openai.com/api/docs/guides/evaluation-best-practices)
7. Anthropic：[Building effective agents](https://www.anthropic.com/engineering/building-effective-agents)
8. LMSYS：[RouteLLM: Learning to Route LLMs with Preference Data](https://arxiv.org/abs/2406.18665)
