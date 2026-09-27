---
type: Analysis
title: 台积电CoWoS与先进封装更新：2027-28年产能上修，SoIC 2028年接棒
description: JPMorgan 9月17日深度：上调2027/28年CoWoS行业产能预期4%/6%，TSMC CoWoS 2027/28年底达200K/225K wfpm；SoIC 2028年成为焦点，NVIDIA Feynman预计采用A16-on-A16 3D SoIC；CoWoS供需缺口收窄至10%，领先制程晶圆和基板成为更大瓶颈。
timestamp: 2026-09-17T00:00:00+08:00
resource: res/台积电/2026-09-17-2330.TW-JPMorgan-TSMC CoWoS and Advanced Packaging Updates-124435562.pdf
source_type: pdf
tags: [tsmc, cowos, soic, advanced-packaging, nvidia, ai-accelerator, jpmorgan, 2026-09]
---

## 摘要

JPMorgan Gokul Hariharan 发布 TSMC CoWoS 与先进封装深度更新（17 页）。核心结论：上调 2027/28 年 CoWoS 行业产能预期 4%/6%，TSMC CoWoS 产能 2027/28 年底分别达 200K/225K wfpm；SoIC 2028 年接棒成为主要增长点，NVIDIA Feynman 预计采用 A16-on-A16 3D SoIC 逻辑-逻辑堆叠。CoWoS 供需缺口已收窄至 10% 左右，领先制程晶圆和 ABF 基板取代 CoWoS 成为 AI 客户更大瓶颈。

## 关键要点

1. **CoWoS 产能上修**：TSMC CoWoS 产能 2027/28 年底预计达 200K/225K wfpm（此前预期约 190K/210K），增量主要来自 CoWoS-R（满足 Vera CPU 和 AI ASIC 需求）。OSAT 厂商扩产更快，2027/28 年底合计产能达 60K/95K wfpm，主要聚焦 CPU 和 CoWoS-R 类应用。

2. **CoWoS 供需缺口收窄**：当前 CoWoS 供需缺口约 10%，较此前有所缓解。瓶颈转移：领先制程晶圆（N3/N2）和 ABF 基板成为 AI 客户更大制约，而非 CoWoS 封装产能本身。

3. **SoIC 2028 年爆发**：3D SoIC 路线图逐渐清晰。NVIDIA Feynman（2028 年）预计采用 A16-on-A16 逻辑-逻辑 SoIC 堆叠（4 die 两堆叠配置，每堆叠 2 个 A16 计算 die）。其他采用者：MTIA 600、OpenAI Serrano、Google TPU v10 部分版本。TSMC SoIC 产能 2027/28 年底预计达 35K/70K wfpm，2028 年预估较此前上调。

4. **NVIDIA 需求微调上修**：Rubin/Rubin Ultra 2027 年 CoWoS 需求上调 4%，反映 Neocloud 和 SPCX 需求上行。Rubin→Rubin Ultra 切换可能快于预期（设计规格变化有限）。Feynman 2028 年采用 3D SoIC 限制 2.5D 封装尺寸至 6-7x reticle（CoWoS-L），同时容纳 4 计算 die + 12-16 HBM cube。

5. **Vera CPU 与 ASIC 需求**：Vera CPU 需求强劲，TSMC 扩 CoWoS-R 产能，Amkor（2H26/2027）和 ASE（2027 底）提供额外支持。预计 LP40 2027 年底迁移至 CoWoS-R。ASIC 方面，TPU v8、Trn3 等放量驱动 CoWoS-R 需求。

## 关联

- [[tsmc-jpmorgan-august-sales-20260910]] — 8月营收与N3供需
- [[tsmc-bofa-semicon-taiwan-20260831]] — SEMICON Taiwan 硅光子/SoIC 趋势
- [[tsmc-bofa-benign-competitive-20260716]] — 此前对竞争格局的评估

## 数据验证

- CoWoS 供需缺口：~10%（JPM 估算）
- TSMC CoWoS 产能：2027 年底 200K wfpm，2028 年底 225K wfpm
- SoIC 产能：2027 年底 35K wfpm，2028 年底 70K wfpm
- 10K wfpm SoIC ≈ 支持 100 万加速器（每加速器 2 个 reticle size base die）

## 机构

J.P. Morgan / Gokul Hariharan / Jennifer Hsieh / David Chou / Jason Chen / Subham Singhania
