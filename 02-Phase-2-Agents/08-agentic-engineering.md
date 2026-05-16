# From Vibe Coding to Agentic Engineering: A Practical Field Guide

*Module 2.7 — 2C: Advanced Agentic Engineering*

> **Chinese version below — 中文版本在下方**
>
> **Prerequisites:** This guide is a continuation of [Module 2.6 Harness Engineering](./07-claude-code-advanced-guide.md). Complete Module 2.6 first.
>
> ⚠️ **Decay disclaimer:** Claude Code iterates fast. Specific commands and features may have changed. The conceptual framework here is durable; verify operational details against [claude.ai/code](https://claude.ai/code) current documentation.

---

## Who This Is For

You already use Claude Code. You have a global CLAUDE.md, project conventions, and you've built verified products with Harness Engineering.

But you may still feel this: **Claude interrupts you every five minutes.** You're managing it, not directing it. Every back-and-forth drains your attention instead of advancing the project.

This guide solves exactly that.

The core upgrade in one sentence: **move from reactive prompting to goal-directed orchestration.** Define the goal, constraints, and acceptance criteria upfront — then let Claude run autonomously and review the output when it's done.

---

## Part 1: Why Vibe Coding Has a Ceiling

### 1.1 The Structural Problem with Vibe Coding

"Vibe Coding" means: you sense what you want, tell the AI, it gives you something, you say "that's not right, try again," and the loop continues.

The problem isn't inefficiency — it's **structural**:

1. **No definition of done:** If you haven't said what "finished" looks like, the loop never ends.
2. **AI is driving you:** Every turn, you're responding to its output instead of directing the work.
3. **Original intent erodes:** Each "no, do it differently" quietly drifts the goal from where you started.
4. **No way to verify it's actually correct:** You "feel" like it's right, but there's no objective check.

This works on small projects. On anything with real complexity, it spirals.

### 1.2 What Agentic Engineering Is

The core shift in Agentic Engineering: **you're the director, AI is the entire crew.**

A director doesn't walk behind the camera mid-shoot to tell the cinematographer how to frame each shot. The director clarifies everything before the cameras roll — what the story is, what the style is, what the non-negotiable red lines are — then trusts the crew to execute.

Applied to Claude Code:

- **Before the cameras roll:** Define Goal, Constraints, and Done When
- **During the shoot:** Claude runs autonomously; only genuine ambiguity warrants a pause
- **After the wrap:** You review and accept — you don't proofread line by line

### 1.3 Two Modes Side by Side

| | Vibe Coding | Agentic Engineering |
|---|---|---|
| **Interaction frequency** | Every 5 minutes | Define at start, review at end |
| **Your input** | Continuous instruction + instant feedback | Goal + Constraints + Done When |
| **Claude's behavior** | Waits for your next instruction | Runs autonomously, pauses only on blockers |
| **Definition of done** | You "feel" like it's close | Predefined acceptance checklist passes |
| **Best for** | Prototypes, one-off tasks | Production features, full modules |
| **Failure mode** | Goal drift, infinite loops | Poorly defined goal runs in the wrong direction |

---

## Part 2: Three-Layer Work Structure

### Layer 1: Global Environment (Already in Place)

Your `~/.claude/CLAUDE.md` defines your working style, design principles, and trigger conditions. This layer doesn't need to change — but you can add one new agentic trigger rule:

> **Important:** CLAUDE.md is **context, not enforced configuration.** Claude treats it as background reference, not hard rules. When instructions are ambiguous or conflicting, Claude may not follow them exactly. The more specific and clear you write, the more likely it will comply.

```markdown
## Agentic Mode Rules
- When given a goal-oriented task (structured with Goal/Constraints/Done When):
  run autonomously without asking for confirmation on intermediate steps.
  Only pause if: (1) two or more valid interpretations exist and the choice changes the outcome,
  (2) a destructive operation is needed that was not mentioned upfront,
  (3) a hard technical blocker prevents progress.
```

### Layer 2: Task Definition (The Critical Upgrade)

This is the biggest divide between Agentic Engineering and Vibe Coding.

**The three-element structure:**

```
Goal:        What you want (description of the end state)
Constraints: What can't be touched, what must stay, technical limits
Done When:   Acceptance criteria (objectively verifiable conditions)
```

**How to use the `/goal` command:**

`/goal` is a Claude Code built-in command for triggering autonomous runs. You follow it with a **verifiable completion condition**. Claude runs until that condition is met, judging for itself at the end of each turn whether the condition is satisfied.

Pattern: give Claude full context first (Goal + Constraints), then use `/goal` to specify the completion condition.

**Wrong vs. right:**

❌ Vibe Coding style (will get interrupted 5 times):
```
Help me add a new feature to the Climate Dossier NDC module,
something like a country filter, and make the results look better.
```

✅ Agentic Engineering style (runs to completion):
```
# Context
Climate Dossier NDC module. React frontend, FastAPI backend.

# Goal
Add a country filter to the NDC query interface.
When a country is selected, retrieval returns only that country's NDC content.
"All countries" is the default (no filter applied).

# Constraints
- Do not modify /brief endpoint logic — only change frontend + retrieval layer
- Country list must be extracted from existing metadata country field, not hardcoded
- UI style must match the existing sector selector (reference: frontend/src/components/ContextCard.tsx)
- Do not modify eval test cases

/goal filter renders correctly, selecting a country returns citations only from that country, npm run build passes with no errors
```

The last line is the completion condition — an objectively verifiable sentence. Claude runs until it's true.

### Layer 3: Autonomous Run + Gate Review

"Gates" are checkpoints you set — Claude can only proceed when a condition is met, otherwise it stops and waits for your confirmation. Once the task is defined, set two things:

**Interrupt policy (put in task header or project CLAUDE.md):**
```
Interrupt only if:
1. Two valid interpretations exist and the choice materially changes the output
2. A destructive operation (delete, overwrite, schema change) was not mentioned in the task
3. A hard blocker prevents any further progress
```

**Review framework (what you do when it's done):**

Don't read the code line by line. Check against your `Done When` list:
- Does every acceptance criterion pass?
- Any unexpected side effects (broken tests, style changes)?
- Review the git diff — did Claude touch anything outside its scope?

---

## Part 3: Step-by-Step Workflow

### Step 1: Task Decomposition (Before Writing Any Code)

Break a large goal into 2–4 independently runnable task blocks. Each block should:
- Have a clear start state and end state
- Complete in 20–40 minutes
- Not depend on the intermediate state of another block

**Example — adding a new module to Climate Dossier:**

❌ Wrong decomposition (sequential dependencies, can't run independently):
```
Task 1: Download documents
Task 2: Ingestion (depends on Task 1)
Task 3: Write eval cases (depends on Task 2)
Task 4: Adjust UI (depends on Task 3)
```

✅ Right decomposition (each block independently definable and verifiable):
```
Task A: Prepare corpus — finalize document list, write source metadata schema
Task B: Ingestion — run ingest.py per module-onboarding.md, verify chunk count
Task C: Eval — write 8 golden test cases, run them, confirm pass rate
Task D: UI — add module entry to landing page, npm run build passes
```

### Step 2: Write Context, Trigger with `/goal`

**Template:**

```
# Context
[Current state, relevant file paths]

# Goal
[One sentence describing the end state — subject is "user" or "system," verb is observable]

# Constraints
- [Specific files/features/logic: do not modify]
- [Technical limits: framework, API, format]
- [Preserved behavior: existing tests must pass]

# Reference Files
- @[relevant file path]

/goal [one sentence completion condition, objectively verifiable]
```

**Phrasing that causes Claude to keep interrupting (avoid list):**

| Avoid | Why | Replace with |
|---|---|---|
| "make it look better" | No objective standard | "match the style of ContextCard.tsx" |
| "optimize it" | Scope unclear | Specify what to optimize and target metric |
| "something like X" | Forces Claude to guess | Point to a specific file: `@X.tsx` |
| "if possible" | Gives Claude decision power | Say explicitly: yes or no |
| "good enough" | No acceptance criterion | Write a Done When entry |

### Step 3: Set the Interrupt Policy

Declare in the task header or project CLAUDE.md:

```markdown
## Interrupt Policy
Pause and ask only if:
1. Ambiguity: two interpretations exist, each produces materially different output
2. Destructive: action requires deleting/overwriting something not listed in Constraints
3. Blocker: technical issue prevents further progress
Otherwise, make a decision, document it in your summary, and keep running.
```

### Step 4: Run, Then Walk Away

Literally walk away: get a glass of water, do something else.

Why? Because if you sit and watch, you'll inevitably intervene before it finishes — which breaks its run flow and pulls you back into the vibe coding loop.

**Long-task tip:** If the task is expected to run for a long time, type `/compact` before the session fills up. Claude will compress its context, free up space, and keep running through the remaining work.

Your role in Agentic Engineering is **gatekeeper**, not monitor.

### Step 5: Review and Close

When you get the result, check in this order:

```
1. Verify each Done When item, one by one
2. Run tests (if there's an eval harness: run it directly)
3. Check git diff — what files did Claude touch? Anything outside scope?
4. If there's a problem: fix the Goal/Constraints definition, restart — don't patch code line by line
```

---

## Part 4: Case Study — Climate Dossier

### Project Background

Climate Dossier is a bilingual RAG climate knowledge base supporting natural language queries across three modules: IPCC AR6 (all three working groups), SBTi Science-Based Targets standards, and G20 NDC national climate commitments — with full citations and a "So What" strategic interpretation layer.

Backend: FastAPI + LlamaIndex + ChromaDB. Frontend: React.
Eval layer: 25 golden test cases, 25/25 passing.

Every major feature was built using Agentic Engineering.

---

### Case A: PRD-First, Not Code-First

Climate Dossier's first step wasn't writing code — it was writing `PRD.md`. The PRD defined:
- What the product is (What)
- Two user types (Who)
- Four Must-Haves (the precursor to Done When)
- Technology choices and constraints (Constraints)

With a PRD, Claude knows where to run. Starting to code without one is like a director calling "action" without a script.

**How key decisions were recorded:**

Every significant decision was written into `CLAUDE.md` in real time:
```markdown
# Climate Dossier — Project CLAUDE.md

## Decided
- No Vercel (blocked in mainland China)
- No Google Fonts (blocked in mainland China, self-hosting woff2 instead)
- LLM: DeepSeek API (with 503 fallback to Anthropic)
- Eval architecture: write eval cases first, then build the module — test cases define "done"
```

This isn't note-taking. It's **making Claude inherit these decisions at every future session startup** — no need to re-explain.

---

### Case B: The Eval Layer Is the Acceptance Criteria

In Climate Dossier, the workflow for every new module is fixed:

```
Write eval cases (define Done When) → Build module → Run eval → Pass → Done
```

IPCC module: 7 eval cases, 7/7 pass before shipping.
SBTi module: 10 eval cases, 10/10 pass before shipping.
NDC module: 8 eval cases, 8/8 pass before shipping.
Total: 25 golden test cases, all passing.

This is what a `/goal` completion condition looks like in practice — a machine-executable acceptance checklist.

```bash
# Run the full acceptance suite in one command
backend/venv/bin/python eval/run_eval.py --module ndc
# Output: 8/8 passing — done
```

When "done" becomes a runnable command, Agentic Engineering gets very clear: Claude runs until that command passes.

---

### Case C: Staging Workflow as a Gate System

Climate Dossier implements gates at the database layer:

```
ingest to dev DB → run eval → pass → promote to prod
                              ↓
                           fail → diagnose, re-run
```

This isn't just technical safety — it's a **structured gate**: Claude can experiment freely in the dev environment, but the prod environment has a concrete entry condition (all evals pass).

Applied to your own projects: in any project with a production environment, **define the gate in the task definition upfront** — don't decide it ad hoc during review.

---

### Case D: Modular Onboarding Protocol

Climate Dossier has a `module-onboarding.md` that defines the complete steps for adding any new module: define document list → configure metadata schema → write eval → run ingestion → verify chunk count → run eval → update CLAUDE.md on pass.

This is a **reusable `/goal` task template**. When adding a new module, you don't reinvent the process — you fill in the new module's parameters and let Claude run the protocol.

This is one of the highest expressions of Agentic Engineering: **the process itself is your most valuable engineering output**, not just the code it produces.

---

## Part 5: Choosing a Tool

**Tools change. Engineering thinking doesn't.** Goal + Constraints + Done When + gate review works on any agentic tool. This guide uses Claude Code, but switching to OpenAI Codex or another tool doesn't change the core method.

Does tool choice matter? Yes — but the deciding factor isn't a feature comparison table; it's your working style.

### How to Decide

**Use Claude Code if:**
- You develop locally (need to read/write local files, run local servers)
- You have complex project conventions that need to persist across sessions (CLAUDE.md is designed for this)
- You need custom workflows (skills, hooks)

**Use OpenAI Codex if:**
- Your code lives entirely on GitHub, not locally
- You need to run multiple independent tasks in parallel (cloud sandbox)
- You don't have or don't want to maintain a local dev environment

Both tools are evolving fast. The feature gap will keep shifting. Base today's decision on your working style, not a feature list.

---

## Part 6: FAQ

**Q: How does this relate to Harness Engineering?**

Harness Engineering (Module 2.6) is the **infrastructure layer**: it teaches Claude how to prove that code is correct (CLAUDE.md, proof of correctness, context hygiene).

Agentic Engineering is the **workflow layer**: it tells Claude where to run, how far to run, and when to stop.

You need both. Without Harness Engineering, Agentic Engineering produces fast but incorrect output. Without Agentic Engineering, Harness Engineering builds correctly but slowly.

**Q: What if Claude runs for 30 minutes and goes completely off course?**

This almost always means the Goal was underspecified, or a critical constraint was missing. Don't patch the wrong output — instead:

1. Find which phrase in the Goal caused the drift
2. Fix Goal/Constraints
3. Restart

One complete re-run is faster than dozens of incremental patches.

**Q: Is `/goal` a built-in Claude Code command?**

Yes, `/goal` is a Claude Code built-in — you don't need to create it. Usage: `/goal` followed by an objectively verifiable completion condition (e.g., `/goal all tests pass and npm run build succeeds with no errors`). Claude runs autonomously and judges for itself at the end of each turn whether the condition is met.

**Q: Is this necessary for small projects?**

For one-off scripts or prototypes, vibe coding is fine. Agentic Engineering earns its investment **after a complexity threshold**: when a task touches multiple files, carries side-effect risk, or needs to be repeated, the upfront cost of structured definition pays back on the first run.

---

## Progression Path

| Stage | Capability | Tool |
|---|---|---|
| Stage 1 | Single-task agentic runs | `/goal` command + structured context + interrupt policy |
| Stage 2 | Project-level convention | Project CLAUDE.md — inheriting decisions across sessions |
| Stage 3 | Repeatable modular process | Onboarding protocol + eval layer |
| Stage 4 | Automated closed loop | CI/CD integration (eval must pass before merge) |

---

## Appendix: Template Library

### `/goal` Launch Template

```
# Context
[Current state description]

# Goal
[One sentence end state]

# Constraints
- [Files or features: do not touch]
- [Technical limits]
- [Behavior that must be preserved]

# Reference Files
- @[relevant file path]

/goal [one sentence completion condition, objectively verifiable]
```

### Interrupt Policy Template (for CLAUDE.md)

```markdown
## Interrupt Policy
Pause and ask only if:
1. Two valid interpretations exist and the choice materially changes the output
2. A destructive operation is required that was not mentioned in the task definition
3. A hard technical blocker prevents further progress
Otherwise: decide, document your reasoning, and keep running.
```

### Review Checklist Template

```markdown
## Review Checklist
- [ ] Done When item 1: pass / fail
- [ ] Done When item 2: pass / fail
- [ ] Done When item 3: pass / fail
- [ ] git diff scope is reasonable, nothing outside Constraints
- [ ] Tests pass (or eval layer pass)
- [ ] No new dependencies or architectural changes introduced
```

---
---

# 从氛围编程到 Agentic Engineering：工程化 AI 的实战指南

*Module 2.7 — 2C：Advanced Agentic Engineering 进阶篇*

> **English version above — 英文版本在上方**
>
> **前置条件：** 本文是 [Module 2.6 Harness Engineering](./07-claude-code-advanced-guide.md) 的续篇。请先完成 Module 2.6，再读这份指南。
>
> ⚠️ **Decay disclaimer:** Claude Code 持续迭代，具体命令和功能可能已更新。本文的概念框架长期有效；操作细节以 [claude.ai/code](https://claude.ai/code) 当前文档为准。

---

## 这份指南是为谁写的

你已经会用 Claude Code 了。你有全局 CLAUDE.md，有项目规范，也用 Harness Engineering 构建过有验证的产品。

但你可能还是有这种感觉：**Claude 每隔五分钟来问你一次。** 你在管理它，不是在指挥它。每一个 back-and-forth 都在消耗你的注意力，而不是推进项目。

这份指南要解决的，正是这件事。

核心升级只有一句话：**从"反应式提示"升级到"目标导向编排"。** 你先定义好目标、约束和验收标准，让 Claude 自主运行，半小时后来看结果。

---

## Part 1：为什么氛围编程到顶了

### 1.1 氛围编程的本质问题

"氛围编程"（Vibe Coding）的意思是：你感觉到想要什么，告诉 AI，它给你一些东西，你再说"这不对，改一下"，如此循环。

这种方式的问题不是效率低，而是**结构性的**：

1. **没有终点定义**：如果你没有说清楚"完成"是什么样的，这个循环就永远不会结束。
2. **AI 在驱动你**：每一轮对话，你都在响应 AI 给你的输出，而不是你在主导方向。
3. **原始意图一点一点被稀释**：每次你说"不对，换一种方式"，原始目标都在偷偷漂移。
4. **没有办法验证它是不是真的对了**：你"感觉"对了，但没有客观标准来检验。

这在小项目上可以用，在任何有复杂度的项目上都会失控。

### 1.2 Agentic Engineering 是什么

Agentic Engineering 的核心转变是：**你是导演，AI 是整个剧组。**

导演不会在拍摄途中走进摄影机后面告诉摄影师每一帧怎么拍。导演在开机之前把所有事情说清楚——故事是什么、风格是什么、哪些场景是不能妥协的红线——然后相信团队执行。

对应到 Claude Code：

- **开机前**：写清楚目标（Goal）、约束（Constraints）、验收标准（Done When）
- **拍摄中**：Claude 自主运行，只有遇到真正的歧义才来问你
- **杀青后**：你做的是评审和验收，不是逐行检查

### 1.3 两种工作方式的对比

| | 氛围编程 | Agentic Engineering |
|---|---|---|
| **交互频率** | 每 5 分钟一次 | 启动时定义，完成时评审 |
| **你的输入** | 持续指令 + 即时反馈 | 目标 + 约束 + 验收标准 |
| **Claude 的行为** | 等你告诉它下一步 | 自主执行，阻断时才暂停 |
| **完成标准** | 你"感觉"差不多了 | 预定义的验收清单通过 |
| **适合场景** | 原型探索、一次性任务 | 生产级功能、完整模块 |
| **失败模式** | 目标漂移，无限循环 | 目标定义不清，跑错方向 |

---

## Part 2：三层工作结构

Agentic Engineering 的工作结构分三层，你在 Module 2.6 已经建好了第一层，本文主要讲第二层和第三层的升级。

### 第一层：全局环境（已有）

你的 `~/.claude/CLAUDE.md` 定义了你的工作风格、设计原则、触发条件。这一层不需要改变，但可以加一行新的 agentic 触发规则。

> **重要说明：** CLAUDE.md 是**上下文，不是强制配置**。Claude 把它当作背景信息来参考，而不是必须遵守的硬性规则——指令模糊或有冲突时，Claude 可能不会按你写的来。写得越具体、越清晰，它遵守的可能性就越高。

```markdown
## Agentic Mode Rules
- When given a goal-oriented task (structured with Goal/Constraints/Done When):
  run autonomously without asking for confirmation on intermediate steps.
  Only pause if: (1) two or more valid interpretations exist and the choice changes the outcome,
  (2) a destructive operation is needed that was not mentioned upfront,
  (3) a hard technical blocker prevents progress.
```

### 第二层：任务定义（最关键的升级）

这是 Agentic Engineering 和氛围编程最大的分水岭。

**三要素结构：**

```
Goal:        你想要什么（终态描述）
Constraints: 不能碰什么、必须保留什么、技术限制
Done When:   验收标准（可以客观核查的条件）
```

**`/goal` 命令的使用方式：**

`/goal` 是 Claude Code 的内置命令，专门用于触发自主运行。你在命令后面跟一个**可验证的完成条件**，Claude 就会在每轮执行结束后自行判断条件是否达成，不满足就继续跑，直到条件成立为止。

使用模式：先给 Claude 完整的上下文（Goal + Constraints），然后用 `/goal` 指定完成条件。

**错误写法 vs 正确写法：**

❌ 氛围编程的写法（会被打断 5 次）：
```
帮我给 Climate Dossier 的 NDC 模块加一个新功能，
就是可以按国家筛选，让结果看起来更好。
```

✅ Agentic Engineering 的写法（一次跑完）：
```
# 背景
Climate Dossier NDC 模块，React 前端，FastAPI 后端。

# 目标
在 NDC 查询界面新增国家筛选器。
用户选择国家后，检索结果只返回该国的 NDC 内容。
"全部国家"作为默认选项（不筛选）。

# 约束
- 不改动 /brief endpoint 的逻辑，只改前端 + 检索层
- 国家列表从现有 metadata 的 country 字段提取，不新增 hardcoded 列表
- UI 风格与现有 sector selector 一致（参考 frontend/src/components/ContextCard.tsx）
- 不修改 eval 测试用例

/goal 筛选器渲染正确，选中某国后 citations 全属于该国，npm run build 无报错
```

注意最后一行：`/goal` 后面跟的是完成条件——一个可以客观核查的句子。Claude 会一直运行，直到这个条件成立。

### 第三层：自主运行 + 门控检查

"门控"就是你设定的关卡——Claude 只有在满足条件时才能推进到下一步，否则就停下来等你确认。定义好任务后，设置两件事：

**门控规则（写在任务开头或项目 CLAUDE.md）：**
```
Interrupt only if:
1. Two valid interpretations exist and the choice materially changes the output
2. A destructive operation (delete, overwrite, schema change) was not mentioned in the task
3. A hard blocker prevents any further progress
```

**评审框架（完成后你做的事）：**

拿到结果时，不要逐行看代码。对着你写的 `Done When` 清单核查：
- 每一条验收标准是否通过？
- 有没有意外的副作用（测试 break、样式变化）？
- 对比 git diff，确认 Claude 没有动它不该动的地方

---

## Part 3：Step-by-Step 操作流程

### Step 1：任务分解（写代码之前）

把一个大目标拆成 2-4 个可以独立运行的任务块。每个任务块的标准：
- 有明确的开始状态和结束状态
- 可以在 20-40 分钟内完成
- 不依赖另一个任务块的中间状态

**例子 — Climate Dossier 添加新模块：**

❌ 错误拆法（顺序依赖，无法独立运行）：
```
任务 1：下载文档
任务 2：ingestion（依赖任务 1）
任务 3：写 eval 用例（依赖任务 2）
任务 4：调整 UI（依赖任务 3）
```

✅ 正确拆法（每块可以独立定义和验收）：
```
任务 A：准备语料 — 确定文档列表，写下 source metadata schema
任务 B：Ingestion — 根据 module-onboarding.md 跑 ingest.py，验证 chunk 数量正确
任务 C：Eval — 写 8 个 golden test cases，跑通，确认 pass 率
任务 D：UI — 在 landing page 新增模块入口，通过 npm run build
```

### Step 2：写好上下文，用 `/goal` 触发自主运行

**模板：**

```
# 背景
[当前状态，相关文件路径]

# 目标
[一句话描述终态，主语是"用户"或"系统"，动词是可观察的行为]

# 约束
- [具体文件/功能/逻辑：不能改]
- [技术限制：框架、API、格式]
- [保留的行为：现有测试必须通过]

# 参考文件
- @[相关文件路径]

/goal [完成条件的一句话描述，可以客观核查]
```

说明：`/goal` 之前的部分是给 Claude 的上下文，`/goal` 后面是触发自主运行的完成条件。Claude 会一直运行，直到完成条件被满足。

**会导致 Claude 反复来问你的措辞（避坑清单）：**

| 避免用这些词 | 原因 | 替换为 |
|---|---|---|
| "让它看起来更好" | 没有客观标准 | "与 ContextCard.tsx 样式一致" |
| "优化一下" | 范围不明确 | 具体说优化什么，目标是什么 |
| "类似于 X" | 需要 Claude 猜测 | 指向具体文件：`@X.tsx` |
| "如果可以的话" | 给了 Claude 决策权 | 明确说要还是不要 |
| "差不多就行" | 无验收标准 | 写 Done When 条目 |

### Step 3：设置门控规则

在任务头部或项目 CLAUDE.md 里声明：

```markdown
## Interrupt Policy
Pause and ask only if:
1. Ambiguity: two interpretations exist, each produces materially different output
2. Destructive: action requires deleting/overwriting something not listed in Constraints
3. Blocker: technical issue prevents further progress
Otherwise, make a decision, document it in your summary, and keep running.
```

### Step 4：运行，然后离开

字面意义上离开：去喝杯水，做点别的事。

为什么这一步重要？因为如果你坐在旁边盯着它跑，你会忍不住在它跑完之前就插手。这会打断它的运行流，也会让你陷回氛围编程的循环里。

**长任务提示：** 如果任务预计跑很长时间，可以在会话快满之前输入 `/compact`，让 Claude 压缩上下文、腾出空间，继续跑完剩余任务。

你在 Agentic Engineering 里扮演的角色是**门控点**，不是监控员。

### Step 5：评审与收尾

拿到结果时，按这个顺序检查：

```
1. 对照 Done When 清单，逐条验证
2. 跑测试（如果有评估层（eval harness）：直接跑）
3. 看 git diff — Claude 动了哪些文件？有没有超出范围？
4. 如果有问题：修正 Goal/Constraints 定义，重新启动一次 — 不是逐行改代码
```

---

## Part 4：案例——Climate Dossier 的 Agentic Engineering 实践

### 项目背景

Climate Dossier 是一个双语 RAG 气候知识库，支持 IPCC AR6 全三卷、SBTi 科学碳目标标准、G20 NDC 国家气候承诺三个模块的自然语言问答，带完整引用和"So What"战略解读层。

后端：FastAPI + LlamaIndex + ChromaDB。前端：React。
评估层：25 个 golden test cases，25/25 passing。

这个项目的每一个主要功能，都是用 Agentic Engineering 方式构建的。下面是具体案例。

---

### 案例 A：PRD-first 定义目标（不是 code-first）

Climate Dossier 的第一步不是写代码，而是写 `PRD.md`。PRD 定义了：
- 这个产品是什么（What）
- 两类用户是谁（Who）
- 四个 Must-Have（Done When 的前身）
- 技术选型和限制（Constraints）

有了 PRD，Claude 才知道往哪里跑。没有 PRD 就开始 coding，等价于导演没有剧本就叫"开机"。

**关键决策记录方式：**

每一个重大决定，都实时写进 `CLAUDE.md`：
```markdown
# Climate Dossier — Project CLAUDE.md

## 已决定
- 不用 Vercel（大陆被封）
- 不用 Google Fonts（大陆被封，已自托管 woff2）
- LLM：DeepSeek API（有 503 备用降级到 Anthropic）
- 评估架构：先写 eval 用例，再构建模块——测试用例定义"完成"
```

这不是记笔记，这是**让 Claude 在未来每次启动都能继承这些决定**，不需要你重新解释。

---

### 案例 B：评估层即验收标准

在 Climate Dossier，每个新模块的工作流是固定的：

```
写 eval 用例（定义 Done When）→ 构建模块 → 跑 eval → 结果 pass → 完成
```

IPCC 模块：7 个 eval 用例，7/7 pass 后上线。
SBTi 模块：10 个 eval 用例，10/10 pass 后上线。
NDC 模块：8 个 eval 用例，8/8 pass 后上线。
三个模块合计 25 个 golden test cases，全部 passing。

这就是 `/goal` 完成条件的真实形态——一个可以机器执行的验收清单。

```bash
# eval harness 用一行命令跑完验收
backend/venv/bin/python eval/run_eval.py --module ndc
# 输出：8/8 passing — done
```

当你把"完成"变成一个可执行的命令，Agentic Engineering 就变得非常清晰：Claude 跑到这个命令通过为止。

---

### 案例 C：Staging Workflow 即门控系统

Climate Dossier 在数据库层实现了门控：

```
ingest to dev DB → 跑 eval → pass → promote to prod
                              ↓
                           fail → 诊断，重跑
```

这个 workflow 的意义不只是技术安全，它是一个**结构化的门控**——Claude 可以在 dev 环境里自由实验，但 prod 环境有明确的进入条件（eval 全部通过）。

类比到你自己的项目：在任何有生产环境的项目里，**门控点要在任务定义里写清楚**，不要靠你在评审时临时决定。

---

### 案例 D：模块化 Onboarding 协议

Climate Dossier 有一份 `module-onboarding.md`，定义了添加任何新模块的完整步骤：定义文档列表 → 配置 metadata schema → 写 eval → 运行 ingestion → 验证 chunk 数量 → 跑 eval → 通过后更新 CLAUDE.md。

这就是一个**可重复的 `/goal` 任务模板**。每次添加新模块，你不需要重新发明流程，只需要填入新模块的参数，然后让 Claude 按协议运行。

这是 Agentic Engineering 的最高境界之一：**流程本身就是你最有价值的工程产出**，而不只是你写出来的代码。

---

## Part 5：选哪个工具？

**工具会变，工程思维不会。** Goal + Constraints + Done When + 门控评审这套方法，可以在任何 agentic 工具上运行。本指南用 Claude Code，但如果你换成 OpenAI Codex 或者其他工具，核心方法完全不变。

那工具选择有没有意义？有——但判断标准不是功能表，而是你的工作方式。

### 怎么选

**用 Claude Code，如果：**
- 你在本地开发（需要读写本地文件、跑本地服务器）
- 你有复杂的项目规范需要跨会话持久化（CLAUDE.md 是为此设计的）
- 你需要自定义工作流（skills、hooks）

**用 OpenAI Codex，如果：**
- 你的代码全在 GitHub，不在本地
- 你需要同时跑多个独立任务（云端并行沙箱）
- 你没有或不想维护本地开发环境

两个工具都在快速演进，功能差距会不断变化。今天的决策依据应该是工作方式，不是功能清单。

---

## Part 6：常见问题

**Q：这和 Harness Engineering 是什么关系？**

Harness Engineering（Module 2.6）是**基础设施层**：它让 Claude 知道怎么证明代码是正确的（CLAUDE.md、proof of correctness、context hygiene）。

Agentic Engineering 是**工作流层**：它让 Claude 知道往哪里跑、跑多久、遇到什么情况停下来。

两者叠加才是完整体系。没有 Harness Engineering，Agentic Engineering 会产生快速但错误的输出。没有 Agentic Engineering，Harness Engineering 会让你构建得正确但效率没有提升。

**Q：如果 Claude 跑了半小时但方向完全错了怎么办？**

这几乎总是因为 Goal 定义不清，或者 Constraints 里遗漏了关键限制。不要在错误的输出上继续修改，而是：

1. 找到 Goal 里哪句话导致了偏差
2. 修正 Goal/Constraints
3. 重新启动一次

一次完整的重新运行比无数次零碎修改更快。

**Q：`/goal` 是 Claude Code 的内置命令吗？**

是的，`/goal` 是 Claude Code 的内置命令，不需要自己创建。使用方式：`/goal` 后面跟一个可以客观验证的完成条件（例如：`/goal all tests pass and npm run build succeeds`）。Claude 会自主运行，在每轮结束后自行判断条件是否达成，直到满足为止。

**Q：如果项目很小，有必要这样做吗？**

对于一次性小脚本或原型，氛围编程完全没问题。Agentic Engineering 的价值在**复杂度临界点之后**：当一个任务涉及多个文件、有副作用风险、或者需要反复执行时，结构化定义的投入会在第一次运行就回收。

---

## 升级路径

| 阶段 | 能力 | 对应工具 |
|---|---|---|
| 阶段 1 | 单任务 agentic 运行 | `/goal` 命令 + 结构化上下文 + 门控规则 |
| 阶段 2 | 项目级规范沉淀 | 项目 CLAUDE.md — 让每次会话继承决策 |
| 阶段 3 | 可重复模块化流程 | Onboarding 协议 + 评估层 |
| 阶段 4 | 自动化闭环 | CI/CD 集成（eval 跑通才允许 merge） |

---

## 附录：模板库

### `/goal` 启动模板（可直接复制）

```
# 背景
[当前状态描述]

# 目标
[一句话终态描述]

# 约束
- [不能动的文件或功能]
- [技术限制]
- [必须保留的行为]

# 参考文件
- @[相关文件路径]

/goal [完成条件的一句话，可以客观核查]
```

### 门控规则模板（放入 CLAUDE.md）

```markdown
## Interrupt Policy
Pause and ask only if:
1. Two valid interpretations exist and the choice materially changes the output
2. A destructive operation is required that was not mentioned in the task definition
3. A hard technical blocker prevents further progress
Otherwise: decide, document your reasoning, and keep running.
```

### 评审清单模板

```markdown
## Review Checklist
- [ ] Done When 条目 1：通过 / 失败
- [ ] Done When 条目 2：通过 / 失败
- [ ] Done When 条目 3：通过 / 失败
- [ ] git diff 范围合理，没有超出 Constraints
- [ ] 测试通过（或评估层 pass）
- [ ] 没有新引入的依赖或架构变化
```
