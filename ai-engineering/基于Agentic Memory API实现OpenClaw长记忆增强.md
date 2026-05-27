> 阿里云计算平台AI搜索团队

原文链接：https://mp.weixin.qq.com/s/coDGE7bjC9KyPSLwLKANkw?scene=1&click_id=60

 在2026年 OpenClaw 大行其道的当下，OpenClaw 原生的记忆组件基于本地存储，不支持跨设备同步和跨会话记忆，其痛点显著。阿里云计算平台AI搜索团队通过集成发布的 Agentic Memory API 作为云端智能记忆服务，灵活对接 OpenClaw 提供持久化的长记忆能力、语义检索和技能管理功能。彻底解决 OpenClaw 本地存储记忆不智能的痛点。

 方案简介

 基于 Agentic Memory API 实现 OpenClaw 长记忆增强能力，构建长短记忆、情景、语义的多层记忆体系。通过向量与图谱混合云存储，实现跨会话信息持久化及智能检索巩固，突破上下文限制，赋予 Agent 长期个性化记忆能力，显著提升交互连贯性与用户理解深度。

 01

 快速部署

 1. 在 OpenClaw（或者 JVSClaw 等兼容版 agent）对话框内输入以下指令安装插件：

 请根据https://help.aliyun.com/zh/open-search/search-platform/use-cases/best-practice-agentic-memory-openclaw 文档安装插件

 2. 然后根据提示输入配置信息即可。

 3. 安装完成后，自动重启openclaw gateway，需要等待一分钟左右。

 02

 方案架构

 整体方案架构包含以下核心流程：

 提取（Extract）：Agentic Memory 从用户输入中提取关键信息，识别需要记忆的内容(Facts, Skills)。

 向量化（Embed）：使用文本嵌入模型将提取的信息转换为高维向量。

 存储（Store）：将向量数据和文本信息写入 Elasticsearch。

 检索（Retrieve）：当用户发起新请求时，在 Elasticsearch 中召回相关 Facts, Skills。

 融合（Fuse）：将检索到的记忆与当前上下文融合，增强 LLM 的响应质量。

 03

 方案优势对比

| 维度 | OpenClaw原生方案 | Agentic Memory方案 |
|---|---|---|
| 存储后端 | 本地SQLite/LanceDB | Agentic Memory API云端服务 |
| 数据持久化 | 本地文件 | 云端持久化 |
| 跨设备同步 | 不支持 | 支持 |
| 跨会话记忆 | 不支持 | 支持 |
| 事实提取 | 需本地LLM处理 | 服务端自动提取 |
| 向量化与检索 | 需本地嵌入模型 | 服务端自动完成 |
| 技能管理 | 不支持 | 支持搜索、获取、上传、更新 |
| 异步存储 | 不支持 | 支持异步任务，可查询状态 |
| 本地依赖 | 需要原生依赖 | 仅需Node.js内置fetch |

 04

 实践步骤

 （一）操作流程

 步骤一：开通Agentic Memory API服务并获取连接信息

 登录 AI 搜索开放平台控制台，开通 Agentic Memory API 服务。获取 API服务地址（baseUrl）、API Key、Workspace Name。

 步骤二：安装插件

 ```
 openclaw plugins install @alicloud-ai-search/openclaw-memory
 ```

 步骤三：配置插件参数

 编辑 `~/.openclaw/openclaw.json`，添加配置：

 ```json
 {
   "plugins": {
     "entries": {
       "openclaw-memory": {
         "enabled": true,
         "config": {
           "baseUrl": "http://<workspace-id>.platform-cn-shanghai.opensearch.aliyuncs.com",
           "workspaceName": "default",
           "apiKey": "YOUR_API_KEY_HERE"
         }
       }
     }
   }
 }
 ```

 步骤四：启动或重启Gateway

 ```
 openclaw gateway restart
 ```

 （二）验证记忆功能

 CLI命令：
 ```
 openclaw mem search "项目架构"
 openclaw mem search "项目架构" --limit 10 --skill
 openclaw mem get <memory_id>
 openclaw mem forget <memory_id>
 openclaw mem task <task_id>
 ```

 Agent工具：`memory_recall`、`memory_store`、`memory_update`、`memory_forget`、`memory_get`

 05

 工作原理

 自动召回流程（autoRecallMemory 启用时）：
 1. 获取用户输入作为搜索查询
 2. 向 API 发送搜索请求，检索相关记忆和技能
 3. 以 XML 格式注入到 Agent 上下文前部：
 ```xml
 <relevant-memories>
 Relevant facts from long-term memory:
 - 用户名为小明
 - 用户下周一早上十点有会议
 Relevant skills:
 - skill-name: description of the skill
 </relevant-memories>
 ```

 自动捕获流程（autoCaptureMemory 启用时）：
 1. 提取对话中的用户和助手消息
 2. 过滤短消息、包含 `<relevant-memories>` 的消息、启动提示、临时会话
 3. 发送到 API 进行事实提取和异步存储

 REST API接口：

| 方法 | 路径 | 说明 |
|---|---|---|
| GET | {prefix}/health | 健康检查 |
| POST | {prefix}/search | 搜索记忆和技能 |
| POST | {prefix}/memories | 存储记忆（异步） |
| PUT | {prefix}/memories/:id | 更新记忆 |
| GET | {prefix}/:id | 获取记忆或技能 |
| DELETE | {prefix}/:id | 删除记忆或技能 |
| GET | {prefix}/tasks/:task_id | 查询异步任务状态 |
| PUT | {prefix}/skills/:id | 更新技能 |

 06

 常见问题

 插件注册后日志无输出 → 检查 slots.memory 配置和 enabled 状态
 搜索返回空结果 → 确认 API 服务正常、已有记忆存储
 记忆存储后无法立即检索 → 存储是异步的，需用 task_id 查询状态
 自动召回未触发 → 确认 autoRecallMemory=true、非临时会话、输入非空

---

## 深度解析：语义相似度匹配是如何工作的？

### 1. 文本 → 向量（Embedding）

"下周一的会"和"我周一早上十点有个会议"分别送进 embedding 模型，各自输出一串高维向量（如 1536 维浮点数数组）：

```
"下周一的会"       →  [0.12, -0.34, 0.78, ...]
"我周一早上十点有个会议" →  [0.11, -0.31, 0.75, ...]
"今晚吃什么"       →  [-0.89, 0.45, -0.22, ...]
```

在向量空间中，前两个向量方向接近（余弦相似度高），第三个离得远。ES 存储每条记忆的向量，检索时拿查询向量做 top-K 最近邻（kNN），实现语义匹配而非字面匹配。

### 2. 为什么能跨字面匹配？

Embedding 模型在预训练时已学会语言中的同义、上下位、常识关系：
- "下周" ≈ "周一"（未来时间指代）
- "会" ≈ "会议"（同义）
- "十点"是"早上"的下位细节

即使字面完全不同，映射到向量空间后方向仍然接近。

### 3. 完整调用链

```
用户输入 "下周一的会"
       │
       ▼
OpenClaw Gateway 触发 before_agent_start 事件
       │
       ▼
openclaw-memory 插件拦截 [autoRecallMemory=true]
       │
       ▼
POST {baseUrl}/.../memory/agentic-memory/search
  Body: { "query": "下周一的会", "limit": 5 }
  Header: Authorization: Bearer <apiKey>
       │
       ▼
阿里云 Agentic Memory API（服务端完成全部重活）：
  1. 将 "下周一的会" embedding 成向量
  2. 在 ES 中做 kNN 检索
  3. 返回 top-5 相关记忆
       │
       ▼
返回 JSON → 插件包装成 XML 注入到 Agent 上下文前部：
  <relevant-memories>
  Relevant facts from long-term memory:
  - 用户下周一早上十点有会议
  </relevant-memories>
       │
       ▼
LLM 拿到（记忆上下文 + 用户输入），生成回复
```

关键：插件只传原始 query 文本，不做本地 embedding，所有向量化和检索都在阿里云服务端完成。这就是轻量化的核心——Agent 侧零 AI 依赖，仅需 HTTP 调用。
