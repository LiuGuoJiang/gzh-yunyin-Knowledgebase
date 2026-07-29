# V22 AI个人公司MVP技术详细设计

## 一、目标

将AI个人公司OS从架构设计推进到可运行工程。

第一阶段目标：

构建一个基于 FastAPI + LangGraph + RAG + MCP 的个人AI助手。

## 二、整体架构

```
用户
 |
FastAPI API层
 |
LangGraph Workflow
 |
Agent节点
 |
RAG知识库 + MCP工具
 |
外部系统
```

## 三、项目结构

```
ai-founder-os
├── api
├── agents
├── workflow
├── rag
├── memory
├── tools
├── prompts
├── configs
├── knowledge-base
└── docker-compose.yml
```

## 四、Agent设计

### Agent基类

统一能力：

- 输入处理
- Prompt加载
- 工具调用
- 状态更新
- 结果输出

### Content Agent

负责：

- AI热点分析
- 选题生成
- 文章大纲

### Tech Agent

负责：

- 技术研究
- 架构分析
- 代码辅助

## 五、LangGraph设计

核心State：

```
TaskState
├── user_input
├── context
├── plan
├── tool_result
├── output
└── review
```

流程：

```
START
 ↓
任务分析
 ↓
Agent执行
 ↓
工具调用
 ↓
结果审核
 ↓
END
```

## 六、RAG设计

知识来源：

- Markdown笔记
- 公众号文章
- 项目文档
- 技术方案

Pipeline：

```
文档
 ↓
解析
 ↓
切片
 ↓
Embedding
 ↓
向量库
 ↓
Retriever
 ↓
LLM
```

## 七、MCP设计

第一批工具：

- GitHub工具
- 文件系统工具
- 知识库工具
- 数据统计工具

## 八、部署方案

开发环境：

Docker Compose

服务：

- backend
- vector-db
- redis

## 九、验收标准

MVP完成后：

1. 可以检索个人知识库
2. 可以生成公众号选题
3. 可以辅助技术方案设计
4. 可以保存执行记录
