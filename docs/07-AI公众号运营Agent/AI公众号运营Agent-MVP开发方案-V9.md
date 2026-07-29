# AI公众号运营Agent MVP开发方案-V9

## 1. 项目目标

基于前面V1-V8运营体系，建设一个服务于「AI架构师江小北」和「AI自由圈」两个公众号的AI运营助手。

目标：

- 降低每天寻找素材的时间
- 提升选题质量
- 保留个人观点和技术深度
- 沉淀长期内容资产

核心理念：

> AI负责信息处理，人负责价值判断。

---

## 2. MVP范围

第一版不追求全自动发布，只实现辅助运营。

包含：

1. AI新闻采集
2. 新闻价值评分
3. 选题推荐
4. 文章大纲生成
5. 知识库检索增强
6. 内容复盘记录

---

## 3. 技术架构

```text
数据源
 |
RSS / GitHub / 官方博客
 |
采集服务
 |
新闻数据库
 |
LangGraph Workflow
 |
 +-- 新闻分析Agent
 +-- 选题Agent
 +-- 写作Agent
 +-- 复盘Agent
 |
RAG知识库
 |
Markdown/Git仓库
```

---

## 4. 技术选型

### Agent框架

LangGraph

原因：

- 支持状态管理
- 支持复杂流程编排
- 支持Human-in-loop

### RAG

推荐：

- LlamaIndex / LangChain
- Chroma / Milvus
- BGE Embedding模型

### 存储

第一阶段：

- Markdown
- Git仓库

后续：

- PostgreSQL
- 向量数据库

---

## 5. Workflow设计

```text
START
 |
新闻采集Node
 |
新闻评分Node
 |
选题决策Node
 |
内容规划Node
 |
AI写作Node
 |
人工审核Node
 |
数据复盘Node
 |
END
```

---

## 6. Agent设计

## News Agent

职责：

- 获取AI行业新闻
- 清洗重复信息
- 生成摘要

输入：

新闻源

输出：

新闻素材池

---

## Topic Agent

职责：

判断是否适合公众号。

依据：

- 技术影响力
- 热度
- 用户匹配度
- 个人IP相关度

---

## Writer Agent

职责：

生成：

- 标题
- 大纲
- 初稿

注意：

必须引用个人素材库，避免生成普通AI文章。

---

## Review Agent

职责：

检查：

- 是否符合公众号定位
- 是否有个人观点
- 是否存在事实错误

---

## 7. RAG知识库设计

知识来源：

```text
公众号定位
 |
历史文章
 |
个人经历
 |
技术学习笔记
 |
项目实践
 |
数据复盘
```

检索目标：

让AI知道：

- 我是谁
- 我的写作风格
- 我的技术方向
- 我的观点偏好

---

## 8. 项目目录建议

```text
ai-gzh-agent

├── agents
│   ├── news_agent
│   ├── topic_agent
│   ├── writer_agent
│   └── review_agent
│
├── workflow
│   └── graph.py
│
├── rag
│   ├── embedding.py
│   └── retriever.py
│
├── knowledge-base
│
├── api
│
└── docker-compose.yml
```

---

## 9. 开发阶段规划

### Phase 1

完成：

- 新闻采集
- Markdown知识库
- 简单Agent流程

周期：1-2周

---

### Phase 2

增加：

- RAG
- 历史文章分析
- 自动评分

周期：2-4周

---

### Phase 3

增加：

- 多Agent协作
- 数据分析
- 自动运营建议

---

## 10. 项目价值

这个项目同时具备三个价值：

1. 自己运营公众号
2. 展示AI架构能力
3. 形成个人IP案例

未来可以输出文章：

《我如何用LangGraph打造自己的AI内容团队》
