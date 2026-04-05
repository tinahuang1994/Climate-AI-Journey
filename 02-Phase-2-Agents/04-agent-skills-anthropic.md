# Key Learnings: Agent Skills with Anthropic

*Created: March 2026 | Source: [Agent Skills with Anthropic](https://www.deeplearning.ai/short-courses/agent-skills-with-anthropic/) — DeepLearning.AI*

**1. The Problem with Basic AI Agents**

Many AI agents today rely heavily on **prompts** (instructions written in text).

But prompts have several problems:

-   You have to repeat the same instructions many times

-   Long prompts make AI slower and less reliable

-   Complex workflows are hard to manage

For example:

If you want an AI to analyze a spreadsheet, you might have to explain every step each time.

Instead of repeating instructions, the course introduces the concept of **Agent Skills**.

**2. What an Agent Skill Is**

An **Agent Skill** is a reusable package of instructions that teaches an AI how to perform a specific task.

You can think of a skill as a **playbook** for AI.

Example:

Instead of telling AI every time how to analyze a dataset, you create a skill called:

"Time Series Analysis"

Whenever the AI needs that capability, it simply loads that skill.

Skills allow AI agents to **learn reusable workflows instead of repeating prompts**.

**3. Skills Turn General AI into Specialists**

Large language models like Claude or GPT are **generalists**.

They know a little about many topics.

Skills help transform them into **specialists when needed**.

Example:

A single AI model could temporarily become:

-   a **data analyst**

-   a **coding assistant**

-   a **researcher**

-   a **marketing analyst**

Each role is activated through the appropriate skill.

This makes the agent behave more like a **trained professional following a process**.

**4. Skills Are Reusable Workflows**

One major idea from the course is:

If you solve a workflow once, you should reuse it.

Skills let you package workflows such as:

-   code review

-   research reports

-   data analysis

-   generating practice questions from notes

Once built, the same skill can be reused many times across different projects.

This improves:

-   efficiency

-   consistency

-   reliability

**5. The Structure of a Skill**

Skills are usually stored as **structured folders of instructions**.

A typical skill includes:

**SKILL.md**

This file explains:

-   what the skill does

-   when to use it

-   what steps to follow

Additional files may contain:

-   templates

-   examples

-   instructions

-   code snippets

This structure allows the agent to **load only the information it needs** instead of reading everything at once.

**6. Progressive Disclosure (Managing Context)**

One challenge with AI systems is the **context window** (how much information the AI can process at once).

Skills solve this using something called **progressive disclosure**.

Instead of loading everything immediately:

1.  The AI sees a short description of the skill

2.  If the skill is relevant, it loads the detailed instructions

3.  It may load additional files if needed

This keeps the AI's context **clean and efficient**.

**7. Skills vs Tools vs Subagents**

The course explains how skills differ from other components in agent systems.

**Tools**

Tools allow agents to **take actions**.

Examples:

-   web search

-   database queries

-   running code

-   accessing files

**Skills**

Skills define **how to perform a workflow**.

They are more like:

-   procedures

-   playbooks

-   operating manuals

**Subagents**

Subagents are **separate AI workers** that handle specific tasks.

Example:

-   a research subagent

-   a coding subagent

-   a testing subagent

Skills can be used **inside subagents** to guide how they work.

**8. Pre-Built Skills**

The course also introduces several **ready-to-use skills**.

Examples include workflows for:

-   spreadsheet analysis

-   presentation generation

-   skill creation itself

These pre-built skills help developers quickly build **larger automated workflows**.

**9. Creating Custom Skills**

A major part of the course is learning how to build your own skills.

Examples demonstrated include:

-   generating practice questions from lecture notes

-   analyzing time-series data

-   performing code reviews

-   conducting research on documentation and repositories

These skills allow agents to **follow structured methods rather than improvising answers**.

**10. Using Skills Across Different Systems**

Skills can be used across multiple environments including:

-   AI chat interfaces

-   APIs

-   coding assistants

-   agent development frameworks

Because skills follow an **open format**, they can be reused across different agent systems.

This makes them similar to **software modules**.

**11. Skills Enable More Advanced Agent Systems**

Skills become even more powerful when combined with other agent technologies such as:

-   external tools

-   APIs

-   subagents

-   data sources

Together, these components allow developers to build **complex AI workflows that resemble real business processes**.

**12. Best Practices for Designing Skills**

The course highlights several guidelines:

**Keep skills focused**

Each skill should do one thing well.

**Make skills reusable**

Design them so they can work in many scenarios.

**Use clear instructions**

Skills should include structured steps that guide the AI.

**Load skills only when needed**

This keeps context efficient and improves performance.

**13. Key Takeaways**

-   **Agent Skills are reusable workflows for AI agents.**

-   They reduce the need for repeated prompting.

-   Skills turn general AI models into **task specialists**.

-   They help organize complex AI systems.

-   Skills make AI workflows **more consistent, scalable, and reliable**.

**Overall Insight**

The key shift introduced in this course is moving from:

**"Prompting AI each time"**

to

**"Building reusable capabilities for AI agents."**

Just as human teams rely on **playbooks, procedures, and training**, AI agents can rely on **skills** to perform tasks more effectively and consistently.
