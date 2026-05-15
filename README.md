# Climate AI Engineering: My Learning Journey

> **Chinese version below — 中文版本在下方**

---

## What This Is

This is a living repository documenting my ongoing journey into Climate AI Engineering. Rather than just collecting notes, I applied every concept to a specific mission: **How can AI help us navigate complex climate data?**

Each module links to a course or primary source, plus a study note with applied examples from real climate projects I built.

*Started: February 2026 — actively updated*

---

## The Backstory

In February 2026, I started with a simple goal: figure out how to write better prompts. That curiosity turned into a deep dive through courses from **Google, Anthropic, Stanford, MIT, Columbia, CalArts, and DeepLearning.AI** — and more importantly, into a series of real products I shipped while learning.

I realized that to actually move the needle on climate work, I needed more than a chatbot — I needed a system. This roadmap tracks my evolution through five distinct phases.

📖 **New here? Read the [Full Guide](./full%20guide.md) first** — it's the syllabus that explains every module, the key learnings, and how it all connects.

---

## What I Built

The real test of any learning journey is what you ship. Here are the projects I built while going through this curriculum:

👉 **[Full portfolio: tinahuang.vercel.app](https://tinahuang.vercel.app/)**

Highlights:
- **Climate Dossier** — Bilingual RAG knowledge base covering IPCC AR6, SBTi standards, and G20 NDC commitments with full citations and strategic analysis layer
- **Smoke Story** — AI-powered wildfire storytelling tool using geospatial AQI data
- **No Thanks** — Workplace boundary-setting coach using Claude as the reasoning engine
- **Climate Triple Takes** — Digital climate newsletter with 3 distinct editorial lenses

---

## The Learning Path

### [Phase 1: The Communication Shift](./01-Phase-1-Foundations)
I stopped treating AI like a search engine and started treating it like a collaborative partner.
- **Key Breakthrough:** Mastering the 5-Step Formula (Task, Context, Reference, Evaluate, Iterate) and advanced persona patterns.

### [Phase 2: From Chatbots to Agents](./02-Phase-2-Agents)
I moved my workflow off the web and into my terminal to give the AI "hands."
- **Sovereign Systems:** Setting up Claude Code + Obsidian to keep research private and local.
- **Multi-Agent Frameworks:** CrewAI, AutoGen, and Agent Skills.
- **Harness Engineering:** Building structured, testable AI workflows with CLAUDE.md and proof-of-correctness layers.
- **Agentic Engineering:** Moving from reactive prompting to goal-directed orchestration using Claude Code's `/goal` command — defining outcomes upfront, letting Claude run autonomously, and reviewing against acceptance criteria. Case study: Climate Dossier (25 eval test cases, PRD-first build, staging gates).

### [Phase 3: The Reliability Engineering](./03-Phase-3-Reliability)
Curing hallucinations with data architecture. For climate data, "good enough" isn't enough.
- **Audit-Grade AI:** Using RAG and Knowledge Graphs to ensure every claim has a citation.

### [Phase 4: Design as a Science](./04-Phase-4-Design)
Learning at MIT and CalArts that "pretty" is a math problem.
- **Aesthetic Math:** Using the 8-Point Grid System, HSL color theory, and typography rules to build trust.

### [Phase 5: Model Customization](./05-Phase-5-Model-Customization)
Going beyond prompting — learning when to actually change the AI's behavior.
- **Key Breakthrough:** Understanding the RAG vs. Fine-Tuning decision, and when each is the right tool.

---

## A Note on These Materials

The study notes in this repo were created with the help of AI (Claude) as personalized, applied summaries of each course. The learning journey, the climate projects I designed and built, and the decisions behind them are entirely my own. AI was my tutor — not the student.

⚠️ **Decay disclaimer:** AI moves fast. Some specific tools, APIs, or framework details in these notes may be outdated by the time you read them. Treat everything here as a conceptual foundation — always verify against current documentation before building.

---

**Want to chat about Climate AI?** Find me on [LinkedIn](https://www.linkedin.com/in/tinahuang1994/)

---
---

# 气候 AI 工程：我的学习之旅

> **English version above — 英文版本在上方**

---

## 这个仓库是什么

这是一个持续更新的仓库，记录我在气候 AI 工程领域的学习历程。我没有只是收集笔记，而是把每一个概念都应用到一个具体的问题上：**AI 能如何帮助我们理解复杂的气候数据？**

每个模块都链接到课程或一手资料，以及我结合自己构建的真实气候项目写的学习笔记。

*开始时间：2026 年 2 月 — 持续更新中*

---

## 背景

2026 年 2 月，我从一个简单的目标出发：学会写更好的 AI 提示词。这个好奇心把我带入了来自 **Google、Anthropic、Stanford、MIT、Columbia、CalArts 和 DeepLearning.AI** 的系列课程——更重要的是，在学习过程中我实际构建并上线了一系列产品。

我意识到，要真正推动气候领域的工作，我需要的不是聊天机器人，而是一个系统。这份路线图记录了我穿越五个阶段的演化过程。

📖 **第一次来？先读 [完整学习指南](./full%20guide.md)** — 这是课程大纲，解释了每个模块的内容、核心收获，以及它们之间的关联。

---

## 我构建了什么

学习之旅真正的检验标准是你交付了什么。以下是我在学习这套课程时构建的项目：

👉 **[完整作品集：tinahuang.vercel.app](https://tinahuang.vercel.app/)**

主要项目：
- **Climate Dossier** — 双语 RAG 气候知识库，覆盖 IPCC AR6、SBTi 标准和 G20 NDC 承诺，带完整引用和战略解读层
- **Smoke Story** — 基于地理空间 AQI 数据的 AI 野火叙事工具
- **No Thanks** — 职场边界设定教练，以 Claude 作为推理引擎
- **Climate Triple Takes** — 拥有三种不同编辑视角的数字气候通讯

---

## 学习路径

### [第一阶段：沟通方式的转变](./01-Phase-1-Foundations)
我开始把 AI 当作协作伙伴，而不是搜索引擎。
- **核心突破：** 掌握五步提示词框架（任务、上下文、参考、评估、迭代）和高级角色模式。

### [第二阶段：从聊天机器人到 Agent](./02-Phase-2-Agents)
我把工作流从网页端迁移到终端，给 AI 装上了"手"。
- **主权系统：** 搭建 Claude Code + Obsidian，让研究保持私有和本地化。
- **多智能体框架：** CrewAI、AutoGen 和 Agent Skills。
- **Harness Engineering：** 用 CLAUDE.md 和正确性证明层构建有结构、可验证的 AI 工作流。
- **Agentic Engineering：** 从反应式提示升级到目标导向编排——使用 Claude Code 的 `/goal` 命令预先定义完成条件，让 Claude 自主运行，最后对照验收标准评审结果。案例：Climate Dossier（25 个 eval 测试用例，PRD-first 构建流程，staging 门控）。

### [第三阶段：可靠性工程](./03-Phase-3-Reliability)
用数据架构治愈幻觉问题。对于气候数据，"差不多"是不够的。
- **审计级 AI：** 用 RAG 和知识图谱确保每一个论断都有引用来源。

### [第四阶段：设计作为科学](./04-Phase-4-Design)
在 MIT 和 CalArts 学到：视觉"美感"是数学问题。
- **美学数学：** 用 8 点网格系统、HSL 色彩理论和排版规则建立信任感。

### [第五阶段：模型定制](./05-Phase-5-Model-Customization)
超越提示词——学会在真正需要的时候改变 AI 的行为。
- **核心突破：** 理解 RAG 与 Fine-Tuning 的抉择，以及各自适用的场景。

---

## 关于这些材料

这个仓库中的学习笔记借助 AI（Claude）创作，是每门课程的个性化、应用型摘要。学习历程本身、我设计和构建的气候项目，以及背后的决策，完全来自我自己。AI 是我的导师，不是学生。

⚠️ **时效性声明：** AI 发展极快。这些笔记中的部分工具、API 或框架细节，在你读到时可能已经过时。请把这里的内容作为概念基础——在实际构建之前，请务必核对当前文档。

---

**想聊气候 AI 话题？** 在 [LinkedIn](https://www.linkedin.com/in/tinahuang1994/) 上找我
