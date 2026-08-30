---
type: Reference
title: 腾讯发布并开源Hy4 preview：770B MoE与1M上下文进入国产开源第一梯队
description: 腾讯2026年8月28日发布并开源Hy4 preview：770B总参数、49B激活参数、1M上下文，内部203项工程任务均分2.99/4，并同步接入WorkBuddy、CodeBuddy及腾讯云API。
timestamp: '2026-08-31T00:51:45.521664+08:00'
resource: https://www.tencent.com/tencent-releases-and-open-sources-tencent-hy4-preview/
source_type: url
tags:
- tencent
- hy4-preview
- foundation-model
- ai-productivity
- ai-monetization
- official-source
- 2026-08
---

# 腾讯发布并开源Hy4 preview：770B MoE与1M上下文进入国产开源第一梯队

## 摘要
腾讯于2026年8月28日发布并开源新一代混合专家旗舰模型Hy4 preview，模型总参数量770B、每Token激活49B，上下文长度达到1M Token，并同步提供标准权重与FP8权重。腾讯将模型接入WorkBuddy、CodeBuddy、元宝和ima，并通过腾讯云TokenHub及OpenRouter提供API，表明模型发布已与办公、编程和消费端产品联动。官方内部盲测显示Hy4 preview在203个工程任务上均分2.99/4，略高于GLM 5.3的2.92和Kimi K3的2.94，但这些结果主要来自腾讯官方评测，仍需第三方调用量、留存率及推理毛利率验证商业价值。

## 关键要点

1. **模型规格**：Hy4 preview采用MoE架构，主干总参数770B、每Token激活49B，共78层；其中77层采用256个路由专家和1个共享专家，每Token激活Top-8路由专家及共享专家。
2. **长上下文与推理加速**：上下文长度为1M Token，原生内置1层MTP投机解码层；注意力采用Gated DeepSeek Sparse Attention，并通过IndexCache跨层复用稀疏索引。
3. **全面开源**：腾讯在Hugging Face、ModelScope、GitCode及CNB同步开放Hy4 preview和Hy4 preview-FP8权重，采用Apache 2.0许可证，并提供vLLM、SGLang部署方案和完整微调流程。
4. **产品接入**：模型已接入WorkBuddy、CodeBuddy、元宝和ima，也可通过腾讯云TokenHub及OpenRouter调用；WorkBuddy与CodeBuddy上线后前两周免费提供Hy4 preview。
5. **API定价**：官方价格为每百万输入Token 0.834美元、输出Token 2.501美元、缓存命中Token 0.042美元，定价重点指向大规模生产力与Agent调用。
6. **内部盲测**：腾讯组织163名内部专家评测203个真实工程任务，Hy4 preview均分2.99/4；对GLM 5.3胜/平/负为46.8%/12.8%/40.4%，对Kimi K3为51.2%/7.9%/40.9%。
7. **部分基准**：腾讯披露Hy4 preview在SWE-bench Multilingual、SWE-bench Pro、Terminal-Bench 2.1、OfficeQA Pro及GPQA Diamond上分别取得82.9、65.7、85.4、66.2及92.3，较Hy3均明显改善，但评测环境和部分结果由腾讯自行运行。
8. **自优化尝试**：腾讯称Hy4 preview参与训练方法、数据策略、评测框架及底层算子的自动优化，并通过分析推理系统瓶颈将端到端吞吐量较基线提高31.8%；该数据目前属于公司官方口径。
9. **已知限制**：腾讯明确称Hy4 preview属于早期版本，复杂任务存在思考时间过长和过度自我验证倾向，后续仍将继续进行预训练和后训练迭代。
10. **投资含义**：Hy4如期发布验证腾讯高额AI资本开支已转化为第一梯队模型及实际产品能力，但尚未证明AI投入获得合格资本回报，后续应跟踪Token调用量、免费期后付费留存、腾讯云增速和推理毛利率。

## 关联

- [德银腾讯2Q26业绩分析：AI战略清晰化与Capex激增176%，游戏与广告基本面强劲](tencent-2q26-db-ai-strategy-and-capex-surge.md) — Hy4发布兑现了2Q26财报后管理层提出的模型升级和AI执行加速路径。
- [汇丰腾讯2Q26：AI成本担忧或被高估，WorkBuddy开始变现](tencent-hsbc-2q26-better-ai-outlook.md) — 补充WorkBuddy、MaaS及GPU出租对AI投入形成商业化回报的观察框架。
- [摩根大通中国互联网AI建设成本：阿里股东显性稀释、腾讯组合机会成本、百度子公司权益让渡](jpm-china-internet-who-pays-ai-build-2026-08.md) — JPMorgan将Hy4列为腾讯AI资本开支形成产出的近期验证点。

## 引用

- [Tencent Releases and Open-Sources Tencent Hy4 preview](https://www.tencent.com/tencent-releases-and-open-sources-tencent-hy4-preview/)
- [Tencent-Hunyuan/Hy4-preview GitHub](https://github.com/Tencent-Hunyuan/Hy4-preview)
- [Hy4 preview模型权重](https://huggingface.co/tencent/Hy4-preview)
