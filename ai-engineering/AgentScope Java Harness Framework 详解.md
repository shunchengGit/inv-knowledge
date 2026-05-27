# AgentScope Java 1.1.0 Harness Framework 详解

## 背景

OpenClaw、Hermes、Claude Code 带火了 Harness Engineering 理念，但搬到企业级场景有五个障碍：

1. 多用户多副本 — 本地目录工作区无法共享
2. 工具执行安全 — 用户命令不能在宿主机直接跑
3. 文件系统不可移植 — Agent 逻辑和基础设施耦合
4. Multi-Agent 编排 — 子任务分发/超时/回收全要自己拼
5. 上下文压缩和分层记忆 — 框架只给抽象接口，实现靠自己

根源：个人助手和企业级 Agent 是两种工程形态。

## 两大核心支柱

### Workspace（唯一事实来源）

```
workspace/
├── AGENTS.md          ← Agent 人格，每次注入 system prompt
├── MEMORY.md          ← 精炼长期记忆，后台自动维护
├── knowledge/         ← 领域知识
├── skills/            ← 可复用技能
├── subagents/         ← 子 Agent 规格声明
└── agents/<agentId>/
    ├── context/       ← 会话状态快照
    ├── sessions/      ← JSONL 对话日志（永不压缩）
    └── memory/        ← 每日记忆流水账
```

### AbstractFilesystem（可插拔文件系统）

Agent 调用统一接口（read/write/ls/grep），底层可适配本地磁盘、远端KV、沙箱。三种模式切换只改一行配置。

## 六个核心概念

- HarnessAgent: ReActAgent 的工程封装
- Workspace: Agent 的"大脑外化"
- Filesystem: 解耦逻辑与存储
- RuntimeContext: 身份上下文（sessionId/userId）
- Sandbox: 隔离执行 + 状态可恢复
- Memory: 双层记忆系统

## 记忆管理（双层分离）

- 第一层每日流水账: 每次对话后 LLM 提炼新事实 → memory/YYYY-MM-DD.md，只追加
- 第二层长期记忆: MemoryConsolidator 周期性合并 → MEMORY.md，去重精炼

compaction 在 memory flush 之后执行，先沉底再压缩。遇 context overflow 自动捕获、强制压缩、重试。

## 子 Agent 编排

四种声明方式（推荐工作区文件驱动），支持同步/异步。子 Agent 默认叶子节点，防递归。

## 三种部署模式

| 模式 | 场景 | Shell | 数据落点 |
|------|------|-------|---------|
| 本机 + Shell | 个人助手 | 可执行 | 本地磁盘 |
| 远端共享存储 | 多副本在线服务 | 默认关闭 | 远端KV |
| 沙箱执行 | DataAgent/Coding Agent | 隔离执行 | 沙箱内 |

## 要点

AgentScope Java 1.1 把 Harness Engineering 收敛成 HarnessAgent + Workspace + 可插拔 Filesystem + Hook 管线。个人场景当加强版 ReAct Agent，企业场景开启隔离和多租户。参考链接:

- https://github.com/agentscope-ai/agentscope-java/blob/main/docs/zh/harness/overview.md
- https://github.com/agentscope-ai/agentscope-java/blob/main/docs/zh/harness/filesystem.md
- https://java.agentscope.io
