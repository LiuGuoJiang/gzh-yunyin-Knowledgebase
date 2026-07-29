# V8.0 基于 LangGraph + RAG 实现 AI公众号运营Agent技术方案

## 1. 项目目标

将前面建立的公众号运营体系升级为一个 AI Agent 系统，让 AI 负责信息收集、内容分析、辅助创作和数据复盘，人负责最终判断和个人观点输出。

核心目标：

- 自动发现 AI 行业热点
- 基于公众号定位筛选选题
- 基于历史内容生成文章建议
- 基于数据反馈优化内容策略

---

## 2. 整体架构

```
AI新闻源
  |
  v
采集Agent
  |
  v
热点分析Agent
  |
  v
选题规划Agent
  |
  v
内容创作Agent
  |
  v
人工审核发布
  |
  v
数据分析Agent
  |
  v
RAG知识库更新
```

形成内容运营闭环：

发现 -> 分析 -> 创作 -> 发布 -> 复盘 -> 学习。

---

## 3. LangGraph工作流设计

### State设计

```python
class ContentState:
    news_list: list
    selected_topics: list
    article_outline: dict
    draft_content: str
    review_result: dict
    metrics: dict
```

---

## 4. Agent节点设计

### News Collector Agent

职责：

- 获取OpenAI、Anthropic、GitHub Trending等信息
- 生成标准化新闻数据

输出：新闻素材池。

---

### Topic Analyst Agent

职责：

根据评分模型判断价值：

- 技术影响力40分
- 热度20分
- 稀缺性20分
- 账号匹配度20分

输出优先级排序。

---

### Content Planner Agent

根据账号定位生成不同方向：

AI架构师江小北：

- AI架构
- Agent实践
- 企业落地
- 技术人成长

AI自由圈：

- AI热点
- 工具资讯
- 行业动态

---

### Writing Agent

负责：

- 标题生成
- 大纲设计
- 初稿生成
- 语言优化

注意：

不能替代作者观点，个人经历必须由人工补充。

---

## 5. RAG知识库设计

知识库用于保存长期运营经验。

```
公众号知识库
 |
 |-- 定位文档
 |-- 历史文章
 |-- 标题库
 |-- 爆款案例
 |-- 用户反馈
 |-- 数据复盘
```

检索用途：

- 生成符合账号风格的文章
- 避免重复选题
- 学习历史爆款模式

---

## 6. MCP工具设计

未来可以接入：

- RSS新闻工具
- GitHub搜索工具
- 微信数据工具
- Markdown仓库工具
- 数据分析工具

---

## 7. MVP实现路线

第一阶段：

人工触发 + AI辅助

技术：

- LangGraph
- RAG
- Markdown知识库
- 大模型API

第二阶段：

自动采集新闻。

第三阶段：

多Agent协作运营团队。

---

## 8. 个人IP价值

该项目本身也是AI架构师江小北的重要案例：

《我如何用LangGraph打造自己的AI内容运营团队》。
