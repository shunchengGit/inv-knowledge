---
url: https://mp.weixin.qq.com/s/sCmRKJjTpdB4k3145OzZMg
imported: 2026-06-01
category: programming
---

# 深入解析Chromium的 AI Coding 开发体系

---
url: https://mp.weixin.qq.com/s/sCmRKJjTpdB4k3145OzZMg
imported: 2026-06-01
category: programming
---

# 深入解析Chromium的 AI Coding 开发体系

## 摘要
Chromium 是全球最大的开源 C++ 项目之一（3500万+ 行代码），在源码仓库中构建了一整套 AI Agent 基础设施。本文深入解析其 AI Policy、Prompts（四层分层提示词体系）、Skills（18+ 个可复用技能）、Knowledge Base（三层 Agentic RAG）、Eval（评估测试框架）和 Projects（大规模代码改造）六大核心机制，以及三者（Prompts + Knowledge + Skills）在实际开发中的协同工作方式。

## 关键要点

### 1. AI Policy：人类始终是最终责任人
- 作者必须在发送 Review 前自行审查并理解所有代码
- 无论是否使用 AI，作者必须声明代码为自己的原创作品
- 如果 AI Agent 创建的 CL 或 Bug 收到了人类的反馈，必须由人类操作者亲自回复
- 违规后果：提交不理解的代码 → 剥夺 Committer 权限，再犯 → 封禁账号

### 2. Prompts：四层分层提示词体系
```
┌─────────────────────────────────────────────────┐
│  第四层：Task Prompts（任务提示词）                 │
│  一次性任务指令，如 /cr:gerrit/cl-description       │
├─────────────────────────────────────────────────┤
│  第三层：Templates（平台模板）                      │
│  desktop.md / android.md / ios.md / rust.md     │
├─────────────────────────────────────────────────┤
│  第二层：common.md（完整工作流）                    │
│  8 步标准编辑流程 + 知识库引用                      │
├─────────────────────────────────────────────────┤
│  第一层：common.minimal.md（核心指令）              │
│  构建、测试、编码、JNI 等基础规范                    │
└─────────────────────────────────────────────────┘
```
- 8 步标准工作流：深度理解 → 编写代码 → 编写测试 → 构建 → 修复编译错误 → 运行测试 → 修复测试错误 → 迭代
- 维护机制：源文件是 `.tmpl.md`，通过 `process_prompts.py` 脚本自动生成 `.md`

### 3. Skills：18+ 个按需激活的专业技能
- Skills 是专家模块，与 Prompts（始终加载的通用指令）不同，Skills 是按需激活的
- 包括：feature-flag-removal、fuzzing、histograms、cl-description、git-cl-helper、chromium-docs 等
- 每个 Skill 包含完整的 checklist、代码模板、验证流程

### 4. Knowledge Base：三层 Agentic RAG
**核心理念：Consult, then Answer**
- **第一层**：knowledge_base.md — 静态路由表（任务关键词 → 文档路径的 if-then 规则引擎）
- **第二层**：chromium-docs Skill — 本地文档检索工具（2000+ md 文件索引，Python 脚本辅助 AI 定位文档）
- **第三层**：MCP 扩展 — 外部知识源（blink-spec、build-information、depot-tools 等）

**与传统 RAG 的对比**：
| 维度 | 传统 RAG | Chromium 的 Agentic RAG |
|:---|:---|:---|
| 检索方式 | 用户 query → 向量检索 → 返回 chunks | AI 自主判断 → 按规则读取文件 → 按需搜索 |
| 知识来源 | 预构建的向量数据库 | 源码树中的原始文档（实时读取） |
| 路由机制 | 纯语义相似度 | 静态规则表 + 动态搜索 + MCP 外部查询 |
| 更新方式 | 需要重新 embedding | 文档随代码同步更新，索引按需重建 |

### 5. Eval：评估测试套件
- 15+ 个评估用例（构建配置、测试生成、重构、修复测试、Fuzz 测试等）
- Pass@K 机制：一个用例运行 N 次，只要 K 次通过就算成功
- 隔离执行：每个测试在独立的 WorkDir 中运行（btrfs 快照）
- CI 级基础设施：Swarming 分片并行、Docker 沙箱隔离、ResultDB 上报

### 6. Projects：AI 驱动的大规模代码改造
- **bedrock/modularize-chrome-browser**：将 `chrome/browser/` 拆分为独立模块（6 阶段流程，SKILL.md 长达 344 行）
- **code-health/**：代码健康自动化治理框架（histogram-cleanup、lint-sync 等）
- **modernization/**：代码现代化自动修复（AutoFixer 框架，最多 3 轮循环）

### 三大机制的协同关系
```
                    ┌─────────────┐
                    │  开发者需求   │
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │   Prompts   │  ← 定义"怎么做"（8 步工作流）
                    │ (工作流引擎) │
                    └──────┬──────┘
                           │
              ┌────────────┼────────────┐
              │            │            │
       ┌──────▼──────┐ ┌──▼───┐ ┌──────▼──────┐
       │  Knowledge  │ │Skills│ │    Task     │
       │  (知识增强)  │ │(专业 │ │   Prompts   │
       │             │ │ 技能)│ │  (快捷命令)  │
       │ 告诉 AI     │ │告诉AI│ │  加速关键    │
       │"去哪找信息" │ │"如何 │ │   环节执行   │
       │             │ │做特定│ │             │
       │             │ │任务" │ │             │
       └─────────────┘ └──────┘ └─────────────┘
```

## 文档积累历史
- Chromium 的文档从 **2015 年**开始积累，跨越 **11 年**，总计 **6445 次提交**
- `agents/` 目录于 **2025 年 7 月 10 日**创建
- `chromium-docs` 核心 Skill 于 **2026 年 1 月**由一位微软工程师提交
