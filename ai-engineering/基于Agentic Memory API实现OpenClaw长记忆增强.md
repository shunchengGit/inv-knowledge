---
url: 
imported: 2026-05-27
category: ai-engineering
---

# 

## 摘要
<!-- AI 待填充 -->

## 关键要点
<!-- AI 待填充 -->

## 原文内容

深度解析：语义相似度匹配是如何工作的？

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
