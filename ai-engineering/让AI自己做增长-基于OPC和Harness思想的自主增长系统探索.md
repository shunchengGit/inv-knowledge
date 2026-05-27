---
url: https://mp.weixin.qq.com/s/sZm-KDM7NoITchuhpbJkJQ
imported: 2026-05-27
category: ai-engineering
---

# 让AI自己做增长：基于OPC和Harness思想的自主增长系统探索

# 让 AI 自己做增长：基于OPC和Harness思想的自主增长系统探索

## 摘要
高德地图PC站团队借鉴OPC（一人公司）理念和Harness Engineering思想，构建了多Agent自主增长系统。系统从发现增长机会、生成提案、编写PRD到代码实现、部署上线全流程零人工干预。以"路书"功能验证，连续运行4小时实现完整应用，主流程无P0 Bug。文章详细阐述了多Agent架构设计、长任务状态机、上下文污染解决方案、独立评估体系、Benchmark构建及三轮优化闭环。

## 关键要点

### 核心理念
- OPC（一人公司）：AI Agent独立自主完成从需求到上线的全流程，一人监护多个并行任务
- Harness Engineering：围绕AI Agent设计约束机制、反馈回路、工作流控制和持续改进循环
- Anthropic实践参考：Planner→Generator→Evaluator三层架构，Evaluator配备Playwright MCP

### 多Agent架构
- Orchestrator：总控调度，监听和派发任务状态
- Planner拆分：product_agent（PRD）、design_agent（UI/UX）、arch_agent（技术架构）
- Builder拆分：testcase_agent（测试用例）、builder_agent（功能实现）
- Memory系统：文件形式记录日志和流转，上游产出自动成为下游输入
- 每次任务启动新SubAgent：避免上下文污染

### 长任务保障
- 状态机：DISPATCHED → ACKED → RUNNING → SUCCEEDED/FAILED
- 心跳监控+超时恢复+条件门禁+失败分类处理

### 评估独立性
- 评审与生成分离、零信任验证、零Broken Feature
- 6个独立评审Agent覆盖提案/PRD/契约/测试/实现/前端设计

### Benchmark与评分
- 元评估：评Evaluator评得准不准
- 两层：code snippets + full_runtime
- 三层评审：代码质量→静态质量→动态运行质量（快速失败优先）
- 三轮优化：64.5→67.5→83.4，精确匹配25%→42%→78%

### 踩坑经验
- 环境/SDK/组件面向AI工具化，skill接入后成功率从10-20%→接近100%
- 端到端自动化工程量被严重低估
- 线上部署保留人工确认，小步快跑每次只解决一个点
- 长链路1-3次循环修P0

### 未来方向
- 数据集覆盖更多Agent的元评估，自建bad/good case+标准答案
