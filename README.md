# 投资知识库：阅读与验证入口

## 全量入口
- [知识索引](entries/index.md)：按类型浏览；标签索引位于entries/by-tag/。
- [原始资源索引](res/index.md)：回溯PDF、机构与日期。
- [知识图谱](knowledge-graph.html)：关系导航，不代表因果或观点一致。

## 优先阅读路径
### AI基础设施：先看客户投入，再看供应商兑现
- [云资本开支跟踪](entries/morgan-stanley-global-cloud-capex-tracker-2026-08.md)
- [博通多机构共识与分歧](entries/broadcom-AVGO-FY26Q2-multi-bank-analysis.md)
- [微软FQ3综合](entries/MSFT-FQ3-26-财报速览-Azure加速-Copilot起飞-BNP-Paribas-HSBC-UBS综合.md)
- [Meta资本开支与现金流分歧](entries/Meta-1Q26-Results-Capex-BofA-DB-JPM-20260430.md)

### 电力设备：行业机会→反方观点→官方验证
- [全球燃机供需](entries/ccbi-advanced-manufacturing-gas-turbines-upcycle-202606.md)
- [东方电气麦格理反方观点](entries/macquarie-dec-1q26-performance-downgrade.md)
- [东方电气官方半年报](entries/dongfang-electric-2026-h1-official-report.md)

### 汽车与机器人：区分远期市场和当期利润
- [机器人整机企业比较](entries/Deutsche-Bank-Humanoid-Robot-Comparing-Unitree-UBTECH-DEEP-Dobot-and-Others.md)
- [三花BofA：H股估值警示](entries/BofA-Zhejiang-Sanhua-1Q26-Core-Beat.md)
- [三花UBS：A股盈利与新业务](entries/UBS-Zhejiang-Sanhua-Intelligent-Controls-Q126-Revenue.md)
- [福耀官方半年报](entries/fuyao-glass-2026-h1-official-results.md)
- [福耀实际与预期比较](entries/fuyao-glass-2026-h1-results-expectation-valuation-analysis.md)

### 银行：经营能力→季度兑现
- [宁波银行客群经营](entries/ningbo-bank-client-strategy-zhongtai-analysis.md)
- [宁波银行2Q26业绩](entries/ubs-bank-of-ningbo-2q26-results-beat.md)
- [MS金融高质量发展](entries/Morgan-Stanley中国银行业投资者演示-高质量发展与人民币存款新规.md)

## 引用纪律
1. 每个数字明确机构、报告日期、财年/自然年、币种、单位，区分实际/管理层指引/券商预测。
2. timestamp可能是导入时间，不能替代报告发布日期；报告超过90天标注老化，超过183天默认不作当前依据。
3. Reference用于官方基准，Synthesis用于多源综合；研报不是官方事实。相同PDF被财报基准和复盘共同引用不等于重复条目。
4. 旧估值、目标价、买入区间不是当前建议；manual且标有来源缺口的条目不得充作可验证财报锚点。
5. entry关联必须真实、非自身且有具体理由；无相关证据时写缺口，不机械凑链接。
6. 少数旧文件名为兼容历史入链而保留，例如“日月光投控中介层…”实际主体已更正为世界先进VIS，以title与源PDF为准。
7. 原始PDF只读入口为curator的km_import.py read；不要把目录链接当作来源文件。

## 写入与维护
仅由curator主流程写库。多个会话不要同时导入、修复或提交；开始前核对HEAD与工作区并备份，完成后重建索引/图谱、复检和核对远端HEAD。当前不存在已验证的跨进程写锁，不能仅凭锁文件宣称防住并发。
标签仅合并确定同义词；Q1/Q2、preview/review以及行业/子行业不因字符串相似而合并。低频标签可代表新的研究标的，不应为了告警归零删除。

## 已知缺口
本轮为结构优化与重点源文纠偏，不是所有条目的全篇事实审计。恒瑞缺少足够相关的官方交易材料；东方电气、恒立、双环旧manual估值仍需另行补齐数据来源。URL可达性未全量检查。
