# Advanced Claude Code Guide: Harness Engineering for Non-Engineers

*A practical, operationalized playbook for building AI products with structure, proof, and discipline.*

> ⚠️ **Decay disclaimer:** Claude Code ships updates frequently. Specific commands, flags, and features described here may have changed. Use this as a conceptual foundation and verify current details at [claude.ai/code](https://claude.ai/code).

---

## What This Guide Is For

You've been using Claude Code for a month. You know how to vibe code. You've shipped things. But you've probably also noticed that on bigger or more complex projects, the results get messier — Claude drifts, you lose track of decisions, things break in ways you didn't expect, and it feels like you're managing chaos rather than building a product.

This guide is about changing that. The core shift is moving from **reactive prompting** (ask Claude to do stuff, fix what breaks) to **structured orchestration** (define the system upfront, constrain Claude's environment, require proof of correctness, and keep context clean).

The concept borrowed from software engineering is called **harness engineering** — and despite the jargon, it's simple: before you build the thing, you build the scaffolding that proves the thing is working correctly. Think of it like the safety harness and checklists that surgeons use before an operation. The harness doesn't do the surgery. It makes sure the surgery is done right.

You don't need a software background to apply this. You need discipline and a clear process. This guide gives you both.

---

## Part 1: The Mental Model — Why Harness Engineering Matters

### The Problem With Unstructured Claude Code Sessions

Without structure, here's what typically happens on a complex project:

1. You describe a vague goal. Claude starts building.
2. Two hours in, you realize Claude made architecture decisions you didn't want.
3. You ask Claude to fix it. Claude fixes the symptom, not the root cause.
4. The context window fills up. Claude starts "forgetting" earlier constraints.
5. You start a new session. Claude has no memory of anything you agreed on before.
6. You're debugging something that was working yesterday and you don't know why it broke.

None of this is Claude's fault. Claude is an extremely capable agent — but it needs a well-defined environment to perform at its best. Without that environment, it optimizes for what seems plausible, not what you actually want.

### What Harness Engineering Actually Is

Harness engineering means: **before you write any feature code, you build the infrastructure that can tell you whether the feature works correctly**.

In software engineering, this means automated tests. For your purposes as a non-engineer product builder, this means:

- Clear documents that define what "correct" looks like (PRD, specs)
- Test cases or example inputs/outputs Claude can run against
- Checkpoints that force Claude to verify before continuing
- Structured file layouts that persist between sessions

The analogy: when a chef develops a new dish, they don't just cook it once and call it done. They test it with the same ingredients multiple times, write down the recipe precisely so another cook can reproduce it, and taste it at each stage. The recipe is the harness. The tasting checkpoints are the tests.

### The Four Principles Behind This Guide

1. **Context is expensive.** Claude Code has a finite context window. Every unnecessary token in that window is crowding out something useful. Discipline about what lives in context vs. in docs is one of the highest-leverage skills.

2. **Proof beats plausibility.** A Claude response can look correct but be wrong. The only way to know is to test it against something specific. "It looks right" is not enough.

3. **Decisions need a home.** Every time you start a new Claude Code session, it starts fresh. If important architectural decisions live only in chat history, they will be re-made — randomly — in the next session. Write decisions down in permanent files.

4. **Small slices beat big leaps.** The more you ask Claude to do in one step, the harder it is to verify the output and trace failures. Short implementation loops with verification at each step are dramatically more reliable.

---

## Part 2: Project Setup — Building the Foundation

*Do this before you write a single line of feature code. This is the most important phase.*

### Your Project Folder Structure

Every serious project should have this structure from day one:

```
my-project/
├── CLAUDE.md           ← Claude reads this at the start of every session
├── PRD.md              ← What the product is and what success looks like
├── architecture.md     ← Technical decisions and system structure
├── data-model.md       ← Shape of your data (what fields, what types)
├── ui-spec.md          ← How the UI should look and behave
├── test-plan.md        ← What needs to be verified and how
├── .claude/
│   └── settings.json   ← Permission and safety rules for Claude
└── src/                ← Actual code lives here
```

You don't need all of these from day one — but you need PRD.md and CLAUDE.md before Claude writes any code. The others get added as decisions get made.

**Why this matters:** These files are your project's memory. Claude Code will read them at the start of every session. This means every session starts with context — not from a blank slate.

### How to Write PRD.md (Product Requirements Document)

The PRD is the most important document in your project. It answers: *what are we building and why?*

Write it in plain English. No jargon. No technical architecture. Just:

```markdown
# PRD: [Product Name]

## What This Is
One paragraph describing what the product does in plain terms.

## Who It's For
Describe the specific user. Not "anyone who..." — describe a real person.

## What Success Looks Like
List 3-5 concrete things. Not "users find it valuable." Something like:
- A user can complete X task in under 2 minutes
- The output is always in format Y
- The product handles edge case Z without crashing

## What Is Out of Scope
Explicitly list what this does NOT do. This is crucial — it prevents Claude
from solving a different problem than the one you have.

## Non-Negotiable Constraints
Things that cannot change no matter what:
- Must work without login
- Must handle inputs in Chinese and English
- Must cost less than $X to run per month
```

**Why you write it this way:** Without a PRD, Claude invents the product requirements in real time based on vague cues from your prompts. It will optimize for technical elegance or completeness rather than your actual goal. The PRD is the anchor.

Don't worry about having every answer upfront. An incomplete PRD with honest "TBD" markers is far better than no PRD. You'll fill it in as you make decisions.

### How to Write CLAUDE.md

CLAUDE.md is a set of operating rules Claude reads at the start of every session. Think of it as the briefing you give a contractor before they start work each day.

Keep it short (under 400 words) and specific. Here's a template:

```markdown
# Project Rules

## Always Do This First
- Read PRD.md before proposing any features or changes
- Read architecture.md before writing any code
- If a decision isn't in the docs, ask before inventing an answer

## Code Rules
- Prefer small, reviewable changes over large rewrites
- Write or update tests before implementing features
- If you change the data model, update data-model.md first

## What Not To Do
- Do not invent data or hardcode fake values
- Do not add features not in the PRD without asking
- Do not refactor unrelated code during a feature implementation

## When You're Uncertain
- State your uncertainty explicitly
- Propose two options with tradeoffs instead of picking one silently
- Ask one focused question rather than barreling forward

## Verification
- After implementing anything, describe how to verify it works
- Run tests after every change
- If tests don't pass, fix the root cause — don't suppress the error
```

**Why this works:** CLAUDE.md creates consistent behavior across sessions. Without it, Claude's behavior depends on whatever mood of prompts you start the session with. With it, you get a Claude that operates the same disciplined way every time.

**Warning:** Don't make CLAUDE.md too long. The docs explicitly note that overly long memory files reduce adherence. If a rule is too vague or abstract to be actionable, cut it.

### Setting Up .claude/settings.json

This file controls what Claude Code is allowed to do. You don't need to understand JSON syntax deeply — just know that you can use it to prevent Claude from accidentally touching files it shouldn't.

A basic version:

```json
{
  "permissions": {
    "deny": [
      "Bash(rm -rf *)",
      "Write(.env)",
      "Write(secrets.*)"
    ]
  }
}
```

This prevents Claude from deleting everything, writing to your environment variables file, or touching any secrets file. Add rules as you discover things you want to protect.

---

## Part 3: Plan Mode — Think Before You Build

*Use this every time you start working on something non-trivial.*

### What Plan Mode Is

Plan Mode is a setting in Claude Code where Claude can read files and think, but cannot write files or execute commands. It forces exploration before action.

You enter it two ways:
- In the REPL: press `Shift+Tab` to toggle
- From the terminal: `claude --permission-mode plan`

**Why this matters:** The single most expensive mistake in any project is starting to build before you've thought through the structure. It's easy to spend 3 hours building something only to realize it needs to be completely restructured. Plan Mode forces the thinking to happen first, when changing your mind is free.

### The Planning Prompt

When you start Plan Mode on a new feature, use this structure:

```
Read PRD.md, architecture.md, and the current project structure.

Create a plan for [feature name] with these sections:

1. SCOPE SUMMARY
   What exactly will be built. What won't be.

2. FILES THAT WILL CHANGE
   Which existing files get modified. Which new files get created.

3. DATA MODEL
   What data does this feature need? What shape is it?
   If it changes the existing data model, describe how.

4. UI FLOW
   If there's UI: what does the user see and do, step by step.

5. TEST CASES
   What are the 3-5 specific things we'll verify to know this works?
   Include: valid input, invalid input, edge cases.

6. RISKS AND QUESTIONS
   What could go wrong? What do you need to know that's unclear?

Do NOT write any implementation code yet.
```

**Why this format:** Each section has a specific job. "Files that will change" forces Claude to understand the existing codebase before touching it. "Test cases" forces you to define success before building. "Risks and questions" surfaces problems before they become expensive.

### Reviewing the Plan

When Claude returns the plan, don't just approve it. Read each section and ask:

- Does the scope match what I actually want?
- Do the test cases actually prove the thing works?
- Are there questions Claude flagged that I need to answer?

Answer Claude's questions directly in the chat. Then say: *"Update the plan with these answers and flag any remaining uncertainties."*

Only once the plan feels solid should you move to implementation.

### Saving the Plan as a Living Document

Once the plan is approved, ask Claude to save it:

```
Save this plan to PLAN-[feature-name].md in the project root.
We'll use this as the reference document during implementation.
```

This document becomes the source of truth for this feature. If implementation drifts from the plan, you'll notice.

---

## Part 4: The Harness — Building Proof Before Code

*This is the section most beginners skip. It's also the highest-leverage section.*

### What "Building the Harness" Means in Practice

Before implementing a feature, you create a set of specific, verifiable checks that will tell you whether the feature is working. In software engineering this is called "test-driven development" — but you don't need to think of it that way. Just think: *what exactly would prove this works?*

For different types of features, the harness looks different:

**For a feature that processes data:**
- Define 3-5 specific inputs and their expected outputs
- Define 2-3 inputs that should fail and what failure should look like
- Ask Claude to write a test script that runs these checks automatically

**For a UI feature:**
- Define exactly what a user should see and be able to do
- Define what error states look like
- Ask Claude to create a visual checklist that you manually verify

**For an API integration:**
- Define the exact request format and expected response structure
- Define what happens when the API returns an error
- Ask Claude to write a test that calls a mock version of the API

**For a data model change:**
- Define what valid data looks like (what fields are required, what types)
- Define what should be rejected (missing required field, wrong type)
- Ask Claude to write validation tests before touching the actual data

### The Harness Prompt

Use this prompt to build the harness before implementation:

```
Before writing the main feature code, create the test harness.

Based on [feature name], define tests that will fail if the feature
is broken. Include:

1. HAPPY PATH: Valid inputs with their expected outputs. Be specific —
   use real example values, not "some valid input."

2. FAILURE CASES: Inputs that should be rejected, and what the error
   should say.

3. EDGE CASES: Unusual but valid inputs. Empty strings, very long inputs,
   special characters, etc.

4. HOW TO RUN: A simple command or steps I can follow to run these checks.

Do not implement the actual feature yet. Just the tests.
```

### Why You Build Tests First

This feels counterintuitive. Why write tests for something that doesn't exist?

Because **writing the tests forces you to define success precisely**. If you can't write a test for something, it means you don't actually know what "correct" means for that thing. That ambiguity will haunt you during implementation.

Also: once the tests exist, Claude has a concrete goal. Instead of "make it work" (which is vague), Claude is now trying to make specific tests pass. This dramatically reduces the chance of Claude building something plausible but wrong.

Think of it like commissioning custom furniture. If you just say "build me a table," you'll get something table-shaped but probably not what you wanted. If you say "build a table that fits in this 120cm × 80cm space, holds at least 50kg, and matches this wood sample" — now you have a spec the carpenter can be held to.

### A Simple Harness for Non-Engineers

You don't need to write automated tests in code. A harness can be as simple as a document:

```markdown
# Test Plan: [Feature Name]

## Test 1: Basic valid input
Input: [exact value]
Expected output: [exact value]
Status: [ ] PASS [ ] FAIL

## Test 2: Invalid input — missing required field
Input: [exact value with field missing]
Expected behavior: Error message saying "[exact message]"
Status: [ ] PASS [ ] FAIL

## Test 3: Edge case — empty input
Input: ""
Expected behavior: [describe]
Status: [ ] PASS [ ] FAIL
```

Ask Claude to populate this template for your feature, then use it as a checklist after implementation.

---

## Part 5: Implementation — Building in Small Slices

*Now you actually build. But with discipline.*

### The Core Rule: One Slice at a Time

Never ask Claude to implement an entire feature in one prompt. Break it into the smallest meaningful pieces, verify each piece works, then move to the next.

What's a "slice"? It's the smallest change that:
- Is complete in itself (not halfway implemented)
- Can be tested or verified independently
- Doesn't depend on something that isn't built yet

For a feature that has a UI, a backend function, and a database interaction, those are three separate slices — not one thing.

### The Implementation Prompt

```
Implement only the first slice: [describe it specifically].

Rules:
- Make the smallest safe change
- Don't touch files outside the plan's "files that will change" list
- After implementing, tell me exactly what to do to verify it works
- Run the relevant tests from the test plan
- If a test fails, fix the actual root cause — don't suppress the error or
  work around it
- Do not start the next slice until this one passes verification
```

**Why "don't touch files outside the plan":** This prevents scope creep. When Claude encounters related code while implementing, it often wants to refactor or "improve" it. That's usually fine in isolation, but it pollutes your diff, makes verification harder, and can introduce bugs in things that were working. Keep slices clean.

### Verifying Before Continuing

After each slice, verify before asking for the next one. If Claude says "I've implemented X, to verify run Y" — actually run Y. Don't skip this step.

If verification fails:
```
The test for [X] is failing with this error: [paste exact error]

Diagnose the root cause. Don't fix symptoms.
Explain what's actually wrong before proposing a fix.
```

**Why "diagnose before fixing":** Claude's instinct when something fails is to try the first plausible fix. That fix often works in the specific case but leaves the underlying bug intact. Forcing diagnosis first produces better fixes.

### When Claude Goes Off Track

It will happen. Claude will start implementing something that's drifting from the plan, or propose a change to the architecture that you didn't agree to, or "helpfully" refactor something that was working.

When this happens, stop and reorient:

```
Stop. This is drifting from the plan in PLAN-[feature-name].md.
Re-read that document and describe: what were we supposed to be building?
What did you just implement instead? What's the difference?
```

This surfaces the drift explicitly so you can consciously decide whether to follow Claude's direction or course-correct.

---

## Part 6: Context Management — Keeping Claude Sharp

*The single most underrated skill in Claude Code.*

### Why Context Matters

Claude Code's context window fills up over the course of a session. As it fills:
- Claude becomes slower
- Claude starts making subtle errors that it wouldn't make with fresh context
- Claude "forgets" earlier instructions and constraints
- The quality of plans and analysis degrades

Managing context is like managing working memory. You want to keep only what's actively relevant in the window, and offload everything else to documents.

### The Three Context Commands

**`/clear`** — Wipes the context completely. Use when:
- You're switching to a completely different task
- The current session has gone significantly off track
- You've just finished a feature and are starting a new one
- Something is deeply broken and you want a fresh start

**`/compact`** — Summarizes the context instead of wiping it. Use when:
- You're continuing the same task but the session is getting long
- You want to preserve the narrative of what happened without all the detail
- You're about to tackle the next slice of the same feature

When you use `/compact`, give it focus instructions:

```
/compact Focus on: architectural decisions made, tests that are passing or failing,
files that were modified, and any open questions flagged.
```

**`/rewind`** — Goes back to a previous state. Use when:
- Claude went down a wrong path and made changes you want to undo
- Something that was working stopped working and you want to recover
- You need to try a different approach from a checkpoint

### The Context Hygiene Rule

Every time you start a new session, start with this prompt:

```
Read CLAUDE.md, PRD.md, and architecture.md.
Summarize in 3 sentences: what this project is, what we're currently building,
and what the current state of implementation is.
```

This forces Claude to orient itself from documents (permanent) rather than from chat history (ephemeral). If the summary is wrong, your docs need updating — which is useful information.

### What Belongs in Documents vs. Context

**In documents (permanent):**
- All architectural decisions
- The data model
- Test plans
- Feature specs
- Any decision you'd be annoyed to lose tomorrow

**In context (temporary):**
- The current implementation conversation
- Debugging a specific error
- Reviewing the output of the current slice

**Rule of thumb:** If you'd need the information in the next session, write it down. If it's only relevant to the current debugging conversation, it's fine to let it live in context and disappear.

---

## Part 7: Advanced Techniques — Subagents and Research Mode

### Using Subagents for Investigation

Claude Code can delegate investigation tasks to a separate context — this is called using subagents. The practical effect is that research and exploration happen without polluting your main implementation context.

Use subagents when you need to:
- Understand how an existing piece of code works before modifying it
- Compare two implementation approaches before committing to one
- Research a library or API without losing your implementation thread
- Debug a complex error that requires extensive investigation

How to invoke this:
```
I need you to investigate [specific thing] in a separate context.
Don't modify anything. Return a summary with:
- What you found
- How it works
- Any implications for what we're building
- Your recommendation if there's a decision to be made
```

### The Pre-Build Audit

Before starting any significant new project (or major feature on an existing one), conduct an audit. This is a structured review of everything relevant to the build, done before writing any code.

The audit covers four areas:

**1. Architecture audit**
```
Review the current project structure and architecture.md.
Identify:
- Parts of the codebase that will be affected by this feature
- Potential conflicts or dependencies we need to handle
- Anything that's unclear or undocumented that we need to settle first
```

**2. Data audit**
```
Review data-model.md and any existing data files or schemas.
Identify:
- Whether the current data model supports the new feature
- What changes, if any, are needed
- What existing data might be affected by those changes
```

**3. UI/UX audit** (for UI work)
```
Review ui-spec.md and any existing UI components.
Identify:
- Which components can be reused
- What new components are needed
- Any inconsistencies in the existing UI that we should resolve
```

**4. Risk audit**
```
Given the plan for [feature], identify:
- The top 3 things most likely to go wrong
- For each: how would we detect it? how would we recover?
- Any external dependencies we're relying on that could fail
```

Running this audit before building catches the problems that would otherwise surface as expensive mid-build surprises.

---

## Part 8: Daily Workflow — Putting It All Together

*This is your repeatable process for every session.*

### Session Start Checklist

Every time you open Claude Code on an existing project:

```
□ Read CLAUDE.md (Claude does this automatically, but verify it's current)
□ Read PRD.md — does it still reflect what you're building?
□ Read architecture.md — does it still reflect the current state?
□ Orient Claude: "Summarize the project and current state in 3 sentences"
□ If something is wrong in the summary, update the docs before proceeding
```

### Starting a New Feature

```
□ Enter Plan Mode (Shift+Tab or --permission-mode plan)
□ Run the planning prompt (see Part 3)
□ Review and refine the plan
□ Save the plan to PLAN-[feature-name].md
□ Exit Plan Mode
□ Run the harness prompt to build tests first (see Part 4)
□ Implement slice by slice with verification at each step
□ Update architecture.md and data-model.md with any decisions made
```

### During Implementation

```
□ One slice at a time
□ Verify before proceeding
□ Diagnose failures at root cause
□ Use /compact when the session gets long
□ Use /clear when switching to a different task
□ Write down any new architectural decisions immediately
```

### Ending a Session

Before you close Claude Code:
```
□ Are all tests passing?
□ Is architecture.md current?
□ Did the data model change? If so, is data-model.md updated?
□ Is CLAUDE.md still accurate?
□ What's the current state of the feature? Write it in a STATUS.md note.
```

---

## Part 9: The Documents That Run Your Project

*A reference for what each file is for and when to update it.*

### CLAUDE.md
**Purpose:** Operating rules for Claude in this project.
**Update when:** You discover a new constraint or rule that needs to be persistent.
**Keep it:** Under 400 words. Specific. Actionable.

### PRD.md
**Purpose:** What the product is and what success looks like.
**Update when:** The product vision or scope changes, or you decide something is out of scope.
**Keep it:** In plain English. No architecture. No technical details.

### architecture.md
**Purpose:** Technical decisions and system structure.
**Update it BEFORE writing code** that changes the architecture.

What belongs here:
- Which framework/language/tools you're using and why
- How the system is structured (what talks to what)
- Major decisions you've made and the reasoning
- What you explicitly decided NOT to do

Template:
```markdown
# Architecture

## Stack
- Frontend: [what and why]
- Backend: [what and why]
- Data: [what and why]

## System Structure
[Describe how components connect]

## Key Decisions
- Decision: [what you decided]
  Rationale: [why]
  Alternatives considered: [what else you thought about]
  Date: [when]

## What We're NOT Doing
- [explicit exclusions]
```

### data-model.md
**Purpose:** The shape and rules of your data.
**Update it BEFORE writing code** that changes data structures.

What belongs here:
- What entities/objects exist
- What fields each has, what type, which are required
- How they relate to each other
- Validation rules

### ui-spec.md
**Purpose:** How the UI should look and behave.
**Update when:** You make decisions about UI patterns or flows.

What belongs here:
- User flows (what a user does step by step)
- Component descriptions
- Error state behavior
- Design decisions (colors, fonts if relevant)

### test-plan.md
**Purpose:** What needs to be verified and how.
**Update when:** You add new features that need new tests.

This is the accumulation of all your test harnesses — one section per feature.

---

## Part 10: Common Failure Modes — And How to Avoid Them

*Based on real patterns that appear in unstructured Claude Code projects.*

### Failure Mode 1: Starting to Build Before Defining Success

**What it looks like:** You ask Claude to build a feature, it builds something, you look at it and realize it's not quite what you wanted, you ask for changes, those changes break something else, the cycle repeats.

**The fix:** You can't verify output without knowing what correct looks like first. Always define test cases before implementation starts.

### Failure Mode 2: Letting Architecture Decisions Live in Chat

**What it looks like:** In session 1, you decide to use Supabase. In session 3, Claude proposes using a different database because it doesn't know about session 1. You now have conflicting architecture.

**The fix:** Any decision about how the system is structured goes into architecture.md immediately. If it matters, write it down.

### Failure Mode 3: Fixing Symptoms Instead of Causes

**What it looks like:** A test fails. Claude changes the test so it passes instead of fixing the code. Or adds a try-catch that swallows the error. The underlying bug is still there.

**The fix:** Explicitly instruct: "diagnose the root cause before proposing a fix." And read the fix before approving it — does it actually solve the problem or just hide it?

### Failure Mode 4: Giant Prompts That Try to Do Everything

**What it looks like:** "Build me the entire authentication system with login, logout, password reset, email verification, and session management." Claude builds something enormous and complicated, nothing is verifiable, it probably has bugs, and fixing one thing breaks another.

**The fix:** One slice at a time. The discipline of slicing is uncomfortable at first because it feels slower. It isn't. One verified slice per hour beats three hours of debugging an all-at-once implementation.

### Failure Mode 5: Letting CLAUDE.md Become Stale

**What it looks like:** CLAUDE.md was written at the start of the project and never updated. It refers to architecture that changed three weeks ago. Claude follows the outdated rules and makes decisions that conflict with current reality.

**The fix:** Review CLAUDE.md at the start of each week. Remove anything that's no longer true. Add any new rules you've discovered.

### Failure Mode 6: Skipping Plan Mode Because You're in a Hurry

**What it looks like:** You know roughly what you want, Plan Mode feels like overhead, you skip it and just start implementing. You make three architectural decisions on the fly that you later regret. Fixing them costs more time than Plan Mode would have taken.

**The fix:** Use Plan Mode for anything that will take more than 30 minutes to build. The planning prompt takes 5 minutes to run and has never once cost more time than it saved.

---

## Appendix: Prompt Library

*Copy-paste prompts for common situations.*

**Session orientation:**
```
Read CLAUDE.md, PRD.md, and architecture.md.
Summarize in 3 sentences: what this project is, what we're currently building,
and what the current state of implementation is.
```

**Planning prompt:**
```
Enter plan mode. Read PRD.md and inspect the project structure.
Create a plan for [feature name] with: scope summary, files that will change,
data model, UI flow, test cases, and risks/questions.
Do NOT write implementation code.
```

**Harness prompt:**
```
Before implementing [feature], create a test harness.
Define: happy path cases with specific inputs/outputs, failure cases with
expected error messages, and edge cases. Include how to run each check.
Do not implement the feature yet.
```

**Implementation prompt:**
```
Implement only [specific slice]. Make the smallest safe change.
Only touch files in the plan. After implementing, tell me exactly how to verify
it works. Run the relevant tests. Fix root causes, not symptoms.
```

**Failure diagnosis prompt:**
```
The test for [X] is failing with: [paste error]
Diagnose the root cause. Explain what's wrong before proposing a fix.
```

**Context compact prompt:**
```
/compact Focus on: architectural decisions made, tests passing or failing,
files modified, and open questions.
```

**Architecture decision prompt:**
```
We need to make a decision about [topic].
Present two options with: what each involves, tradeoffs, recommendation.
Once we decide, update architecture.md with the decision and rationale.
```

**Drift detection prompt:**
```
Stop. Re-read PLAN-[feature-name].md.
What were we supposed to be building? What did you just implement?
What's the difference, and how should we proceed?
```

---

*Last updated: April 2026*
*This guide is a living document — update it as you learn what works for your workflow.*
