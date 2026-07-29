# V20 AI个人公司MVP代码工程设计

## 一、目标

将 AI个人公司从架构设计推进到可运行工程。

核心目标：

- 建立Agent运行框架
- 建立个人知识RAG
- 建立工具调用能力
- 支撑内容、技术、商业Agent运行

---

# 二、整体工程架构

```
ai-founder-os
|
├── backend
|   ├── api
|   ├── agents
|   ├── workflow
|   ├── rag
|   ├── memory
|   └── tools
|
├── knowledge-base
|
├── prompts
|
├── configs
|
└── docker-compose.yml
```

---

# 三、技术选型

## 服务层

FastAPI

负责：

- Agent接口
- 任务管理
- 状态查询

## Agent编排

LangGraph

负责：

- State管理
- Workflow执行
- 多Agent协作

## 知识库

RAG：

- Markdown知识库
- Embedding
- 向量检索

## 工具层

MCP：

- GitHub
- 文件系统
- 数据接口

---

# 四、核心模块设计

## Agent模块

```
agents
├── ceo_agent
├── content_agent
├── tech_agent
├── business_agent
└── data_agent
```

---

## Workflow模块

示例：内容生产流程

```
新闻采集
 ↓
选题分析
 ↓
大纲生成
 ↓
文章生成
 ↓
人工审核
```

---

# 五、MVP开发优先级

## Sprint1

完成：

- FastAPI项目
- LangGraph基础流程
- RAG检索

## Sprint2

完成：

- 内容Agent
- 技术Agent

## Sprint3

完成：

- MCP工具接入
- Paperclip任务管理

---

# 六、工程原则

不要追求一次完成AI公司。

先打造：

> 一个每天真正帮助自己的AI员工。

然后逐步扩展为AI团队。
