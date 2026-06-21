---
type: Article
title: 深度解析LLM Wiki - Obsidian-Wiki - GBrain：Agent时代知识的“自组织”与“自进化”
description: 本文是「项目深度解析」系列的第4篇，系列文章为《深度解析OpenClaw》、《深度解析Claude Code》、《深度解析Hermes Agent》。（文章内容基于作者个人技术实践与独立思考，旨在分享经验，仅代表个人观点。）
timestamp: 2026-05-16T00:00:00+08:00
resource: https://mp.weixin.qq.com/s/48XpgAMHeaKYj26PrJK-hw
---

# 深度解析LLM Wiki - Obsidian-Wiki - GBrain：Agent时代知识的“自组织”与“自进化”

## 摘要
<!-- AI 待填充 -->

## 关键要点
<!-- AI 待填充 -->

## 原文内容

阿里妹导读




本文是「项目深度解析」系列的第4篇，系列文章为《深度解析OpenClaw》、《深度解析Claude Code》、《深度解析Hermes Agent》。（文章内容基于作者个人技术实践与独立思考，旨在分享经验，仅代表个人观点。）

背景

不知不觉，本文已经是深度解析系列的第四篇了。上一篇解析文章《深度解析 Hermes Agent 如何实现“自进化”及其 Prompt / Context / Harness 的设计实践》在发布后，引发了许多同学的讨论和关注。大家关注的焦点非常集中，主要围绕在“自进化”这个概念，包括“Skill 的自动沉淀”以及“RL（强化学习）训练”这两个核心维度上。

其实，关于RL训练这一块，我在之前的文章里有提到，官方也明确说过，这更多是面向AI研究人员或者算法同学所设计的。如果你的目标是在某个特定领域的垂直任务，或者在特定的 Benchmark 上追求极致的性能效果，那么通过 RL 进行深度训练，确实是让模型突破瓶颈、获得更好效果的有效路径。但对于大多数工程落地场景而言，这种方式的门槛和成本都相对较高。因此，除了RL这条“重资产”路线外，另一种更轻量、更具普适性的方式，就是通过“Skill”的机制来实现 Agent 的自进化。

然而，仅仅是通过Skill自动更新来解决 Agent 的“自进化”，其实还是有点不够的，也有很多人反映真正在用 Hermes Agent 的时候，也没感觉到明显的变聪明，或者看到自动沉淀的比较好的 Skill。这是因为，自动沉淀 Skill 的机制很多时候还是取决于模型自己的判断和决策，这种判断和决策的触发时机和可控性相对就比较低了。因此，通过人给予Agent更多的“知识”来提升 Agent 的能力，甚至存放知识的这个“知识库”如果能“自动梳理”、“自动组织”、“自动更新”甚至“自动进化”，那就更好了，从而就能推动 Agent 的不断“自进化”。

所以，今天的这个深度解析文章就特殊一点，我不按照之前的结构去分析Prompt、Context、Harness这些维度了，我将会从 Knowledge Engineering（知识工程）的角度展开，但知识的效果也是影响Prompt、Context、Harness 非常重要的一部分，并且也是我们的主线话题“如何构建一个好的Agent”中非常重要但提及较少的一个部分。

从“知识堆积”到“结构化记忆”

前段时间，Andrej Karpathy（OpenAI联合创始人）开源了一个名为“LLM-Wiki”的项目[1]，核心其是就一个 Markdown文件，目标是指导大模型Agent进行知识的更新与结构化，整个过程如下图所示[2]。这个项目的本质，其实是解决了一个长期困扰我们的痛点：如何让 Agent 自动将非结构化的资料转化为 “AI能理解”、“有结构”的知识库。另外，今天还会介绍一个项目叫做“Gbrain”[3]，它是由 Y Combinator 总裁兼 CEO Garry Tan 构建的，一个思想和 LLM-Wiki 类似但更工程化一点的知识库项目。

这背后折射出的，是人类在知识管理上的天然短板。人类其实非常擅长“无脑堆积”知识——看到好的文章就收藏，遇到有用的文档就保存（此刻，可以打开看下你的网页收藏夹、各类APP的收藏夹，以及混乱的电脑桌面文件，是不是有很多已经“落灰”很久了，哈哈哈~）。这说明人类很不擅长“组织”知识。要把这些零散的信息梳理成体系化的结构，不仅耗时耗力，更因为缺乏统一的整理标准而变得很困难，容易拖延，拖着拖着就算了。无论是从个人层面看，收藏信息、文件是真的杂乱；还是从企业层面看，以我在阿里云售后做智能客服相关算法多年的经验，企业级知识库的维护成本更是非常之高，这主要体现在两个维度：

时效性与动态维护。知识是有生命周期的，它会随着产品迭代、业务变更而过时或失效。如何精准识别并剔除失效知识，同时无缝接入新知识，本身就是一个巨大的挑战。

组织结构的复杂性。知识该如何分类？以我们阿里云的服务领域来看，是按产品维度？问题场景维度？还是按关键词维度？比如，“镜像”主要集中在ECS、轻量应用服务器这些产品，而OpenClaw的相关知识就可能横跨多个产品线，简单的树状层级结构很难刻画这种复杂的网状关系。这种多维度的交叉关联，使得人工构建和维护一个完美的类似知识图谱之类的方案几乎成为不可能完成的任务。

而在 AI 时代，尤其是对于 Agent 而言，知识的质量直接决定了效果的上限。正如我在前文中说过的，Context 不仅仅包含当前的对话指令和历史记录，更核心的组成部分是外部注入的知识。这里的“知识”是一个广义的概念，它主要包含经验性知识，也就是完成特定任务所需的策略、步骤和隐性经验；事实性知识，比如领域内的客观信息、文档、FAQ 等静态数据。

以 AI Coding 场景为例，当我让 Agent 去写代码时，我期望它遵循的不仅仅是一个语法正确的结果，而是一套完整的“编码习惯”。比如：我喜欢用什么样的命名规范、注释风格？是应该先设计接口再实现细节，还是先跑通 Demo 再重构？优先使用哪些成熟的库或框架？写完代码后，是否自动进行单元测试或静态检查？

这些隐性的、带有个人色彩的经验法则，其实就是典型的经验性知识。在 Hermes Agent 或 OpenClaw 的体系中，我们将这类经验封装为 Skill。Skill 本质上是一种结构化的经验沉淀，它告诉 Agent “在这个特定场景下，应该按照什么步骤、用什么工具、遵循什么标准去行动”。

另一类事实性知识，就比较通俗易懂了。比如：某个概念、术语的定义是什么？某个报错原理背后的机制是怎样的？针对某类常见问题的最佳实践解决方案有哪些？甚至是网上最新的技术博客摘要。这些信息构成了 Agent 回答问题的基础素材。

如果说 Prompt Engineering 是在教模型“完成什么样的任务”，那么 Knowledge Engineering（知识工程）就是在教模型“应该知道什么”以及“如何运用已知信息”。Karpathy 的 LLM-Wiki 思路之所以具有突破性，是因为它突破了传统 RAG “每次查询从头检索”的局限。通过 Schema 文件指导 LLM 主动维护结构化的 Markdown Wiki，它将原始资料“编译”为带有交叉引用、矛盾标注的持久化知识体。

在这种设计下，知识不再是静态的死水，而是随着使用持续累积、增厚的活体，避免了重复推导带来的算力浪费。在这个新范式下，人类的角色发生了转变：我们只需专注于“提问题”和“堆知识”，而将繁琐的维护工作交给大模型。再配合上 Obsidian 这类知识维护的 IDE，Agent 就成为了那个不知疲倦的知识管理助手，可以自动完成知识的清洗、去重与结构化整合。

大家在使用各类 Agent 工具的过程中，尤其是在“养虾🦞”（OpenClaw）的时候，大家会深刻体会到这 Skill 的重要性。但是，这里存在一个明显的痛点：Skill 的编写是有门槛的。 虽然市面上有很多教程教你怎么写出一个高效的 Prompt 或 Skill，但这依然需要开发者对业务逻辑有深刻的理解，并且要花费大量时间去调试和优化指令。对于普通用户而言，手动将隐性经验转化为显性的、机器可执行的 Skill，成本依然很高。

这正是 Hermes Agent 引入“自进化”机制的价值所在——它试图通过自动化生成的方式，降低这一门槛。Agent 不再仅仅被动地接收人类编写的 Skill，而是能够在交互过程中，自动从历史对话、成功/失败的案例中提取模式，自动生成或优化新的 Skill。这种从“人工编写 Skill”到“Agent 自动生成 Skill”的转变，才是实现真正意义上“知识自进化”的关键一步。这个自动化生成 Skill的过程呢，这种其实也是一种也是一种自动化沉淀知识的能力。

Skillify：渐进式披露式的“知识形态”

无论是Andrej Karpathy 的 LLM Wiki，还是Garry Tan 的 GBrain。这两个项目在某种程度上都对 “Skill” 这个概念进行了泛化。

传统意义上的 Skill，往往被固化为一个特定的 SKILL.md 文件或指令集，大模型读取它来掌握某项特定技能。但 LLM Wiki 和 GBrain 的核心创新在于：它们将 Skill 泛化为一种知识组织形态。 在这种范式下，Skill 不再局限于某种固定格式，它可以是任何 Markdown 文件、文档片段甚至是零散的笔记。关键在于，通过定义清晰的元数据（Metadata）或 Schema，描述清楚“在什么场景下应该调用哪些文件”，从而实现知识的渐进式披露（Progressive Disclosure）。

GBrain 的创始人 Garry Tan 甚至使用了一个词叫“Skillify”，也有的论文里使用的词是 “Skillfully”，whatever，这两个词都挺形象的，指的就是去写 Skill 或者像 Skill 一样去组织和加载知识。这种机制允许 各类 Agent 接收各类文件、文本、链接，然后自动将其“编译”并归档到一个统一的个人知识库中。你可以把这个知识库想象成一个巨大的、结构化的 “Skill 包”，它不仅包含事实性知识、经验性知识，还可以容纳你的长期记忆、个人喜好、过往经历等所有碎片化信息。

这就好比拥有一个私人的 AI 助理，它帮你把杂乱无章的桌面文件、散落的笔记，按照 AI 可理解的方式分门别类地管理起来。你无需关心底层的存储细节，只需负责“投喂”资料，Agent 负责整理、索引和持久化。当下次遇到相关问题时，它能直接从“缓存”中提取已内化的知识，而不是重新去搜索。这种理念不仅适用于个人知识管理，对企业级知识库的建设同样具有极高的参考价值。

我回顾一下阿里云智能客服的发展历程，其实知识体系的演进大致也经历了三个阶段，这也折射出当前技术范式的变化。第一个就是“传统智能知识库时代”，从2016~2022年，早期的智能客服基本上就是面向搜索引擎的知识库。知识必须由人工进行严格的分类、打标和归档，形成树状或标签体系。检索时，系统通过关键词匹配召回相关条目。这种方式非常高度依赖人工维护成本，且灵活性比较差，难以应对长尾问题。

到了后面就是2023年，随着大模型的兴起，进入到了“RAG时代”，RAG成为主流技术。核心逻辑就是是“前置小模型检索 + 后置大模型生成”。但是，我在之前的文章《Agent / Skills / Teams架构演进过程及技术选型之道》里提到过，虽然RAG解决了海量知识的存储和召回问题，但存在几个问题：

模型能力断层：前置的检索模型通常比较小，语义理解能力有限，容易漏召或误召关键信息，导致后端大模型“无米之炊”。

搜索独立性：每次交互都是独立的检索过程。即使上一次成功找到了答案，下一次面对相似问题时，仍需重新搜索。这不仅浪费算力，更带来了结果的不确定性，导致“上次搜得准，下次未必准”。

知识未沉淀：为了解决这些问题，在 Agent 时代出现了Agentic RAG，虽然可以通过让大模型反复优化搜索关键词来提升召回率，但这本质上是在用昂贵的推理成本去弥补检索能力的不足，并且且依然无法解决“知识未沉淀”的问题。

在第三个阶段“Agent时代”，知识的组织再次发生变化。相比于RAG，LLM Wiki 和 GBrain 的核心优势就在于“一次学习，永久可用”：

消除重复搜索：当新知识被录入并结构化后，它就成为了 Agent 内部知识库的一部分。下次遇到类似问题，Agent 直接读取已整理的知识，无需再次触发外部检索，极大地提升了稳定性和响应速度。

全链路大模型参与：从知识的解析、结构化到最终的调用，主要由大模型主导。大模型像阅读一本书的目录一样，根据上下文动态决定加载哪部分知识（就是渐进式披露），避免了小模型检索带来的语义偏差。

知识的累积效应：每一次交互都在丰富知识库，Agent 越用越聪明，形成了真正的“飞轮效应”。

简而言之，如果说 RAG 是让大模型“带着书本进考场”，那么 Skillify 则是让大模型“把书读透并记成整理后的笔记”。前者依赖临场发挥、现找资料，后者依赖深厚积累、精准定位。对于追求高稳定性、高准确率的复杂 Agent 场景而言，构建这种基于渐进式披露的持久化知识库，或许是现阶段比单纯优化 RAG 检索策略更本质的解法。

LLM Wiki：三层架构的知识闭环

核心思路捋清楚账号，接下来，我们先深入看一下 Karpathy 提出的 LLM Wiki。他本身就是一个 llm-wiki.md 文件，具体内容我放进来，大家可以仔细看一下：

llm-wiki.md

# LLM Wiki


A pattern for building personal knowledge bases using LLMs.


This is an idea file, it is designed to be copy pasted to your own LLM Agent (e.g. OpenAI Codex, Claude Code, OpenCode / Pi, or etc.). Its goal is to communicate the high level idea, but your agent will build out the specifics in collaboration with you.


## The core idea


Most people's experience with LLMs and documents looks like RAG: you upload a collection of files, the LLM retrieves relevant chunks at query time, and generates an answer. This works, but the LLM is rediscovering knowledge from scratch on every question. There's no accumulation. Ask a subtle question that requires synthesizing five documents, and the LLM has to find and piece together the relevant fragments every time. Nothing is built up. NotebookLM, ChatGPT file uploads, and most RAG systems work this way.


The idea here is different. Instead of just retrieving from raw documents at query time, the LLM **incrementally builds and maintains a persistent wiki** — a structured, interlinked collection of markdown files that sits between you and the raw sources. When you add a new source, the LLM doesn't just index it for later retrieval. It reads it, extracts the key information, and integrates it into the existing wiki — updating entity pages, revising topic summaries, noting where new data contradicts old claims, strengthening or challenging the evolving synthesis. The knowledge is compiled once and then *kept current*, not re-derived on every query.


This is the key difference: **the wiki is a persistent, compounding artifact.** The cross-references are already there. The contradictions have already been flagged. The synthesis already reflects everything you've read. The wiki keeps getting richer with every source you add and every question you ask.


You never (or rarely) write the wiki yourself — the LLM writes and maintains all of it. You're in charge of sourcing, exploration, and asking the right questions. The LLM does all the grunt work — the summarizing, cross-referencing, filing, and bookkeeping that makes a knowledge base actually useful over time. In practice, I have the LLM agent open on one side and Obsidian open on the other. The LLM makes edits based on our conversation, and I browse the results in real time — following links, checking the graph view, reading the updated pages. Obsidian is the IDE; the LLM is the programmer; the wiki is the codebase.


This can apply to a lot of different contexts. A few examples:


- **Personal**: tracking your own goals, health, psychology, self-improvement — filing journal entries, articles, podcast notes, and building up a structured picture of your


_（原文过长，仅显示前8000字。完整内容见 .claw/raw/深度解析LLM Wiki - Obsidian-Wiki - GBrain：Agent时代知识的“自组织”与“自进化”/content.raw.txt）_