# Stanford CS146S: The Modern Software Developer

*Created: March 2026 | Source: Stanford CS146S — The Modern Software Developer*

Welcome to **Week 1 of CS146S: The Modern Software Developer**. Since you've already been using Claude Code and built an MCP, you are actually ahead of most students.

In this session, we are going to bridge the gap between "Vibe Coding" (prompting and hoping) and **Agentic Engineering** (systematic, repeatable production).

**The Case Study:** Throughout the course, I asked AI to teach me concepts through a case study. In this scenario, imagine we are using AI as an **NDC Analyst**. A Nationally Determined Contribution (NDC) is a country's official plan to reduce emissions. AI's job is to read these reports and score them according to a "Policy Rubric" (a set of rules) to see how well the country is doing.

Week 1 Core Concept: The "Junior Developer" Mental Model
----------------------------------------------------------

The foundational shift of Week 1 is moving away from seeing AI as a "search engine" and starting to see it as a **Junior Developer (JD)** sitting next to you.

**1. The 2026 Shift: Intent vs. Implementation**

In the old world (2023), you wrote code. In the modern world (2026), you **manage intent**.

-   **Traditional Dev:** You write every line of Python.

-   **Modern Dev:** You define the **Spec** (the "What") and the **Constraint** (the "How"), and the Agent (Claude Code) handles the **Implementation**.

**2. Why "Vibe Coding" is Dangerous**

Week 1 warns against "Vibe Coding"---where you just say "make it better" or "fix this." Without a structured workflow, vibes lead to **"AI Slop"** (unnecessary code bloat) and **"Hallucination Drift"** (the agent slowly changing your rubric without you noticing).

**The Material: The 5-Stage Agentic Workflow**

Week 1 introduces the framework that separates pros from amateurs. When you use Claude Code for your Climate Watch project, you must force it to follow these five stages:

  **Stage**               **What happens?**                                                                 **Claude Code Command**
  ----------------------- --------------------------------------------------------------------------------- ----------------------------------------
  **1. Research**         The agent explores the codebase or files to understand the context.               claude "Summarize \@brazil_ndc.pdf"
  **2. Planning**         **Critical.** The agent must write out its logic before touching a single file.   /plan "How will you audit this?"
  **3. Implementation**   The agent writes the code or the report.                                          claude "Now generate the audit."
  **4. Testing**          The agent runs a script or a "Self-Audit" to check for errors.                  /test "Does this follow the rubric?"
  **5. Review**           You (the Human) inspect the "diff" and approve or reject.                       (Manual Review in Terminal)

**3. Synthesized Takeaways for Your Climate Project**

-   **Specs are the new Source Code:** Your **Policy_Rubric.md** is actually more important than the Python code. If the rubric is vague, the audit will be trash. Week 1 teaches that you should spend 80% of your time on the **Spec** (the Rubric) and 20% on the **Code**.

-   **The "Fresh Context" Rule:** One major Week 1 lesson is to avoid **Context Poisoning**. If you just audited Brazil, don't audit Kenya in the same session. Use **/clear** (which you have in your Guide!) to wipe the AI's "working memory" so it doesn't accidentally apply Brazilian laws to Kenyan data.

**Your Week 1 Lab Exercise (In Claude Code)**

Since you are a "实战" (practical) learner, here is your assignment to apply Week 1's "Junior Developer" mindset:

1.  **Open Claude Code.**

2.  **Assign a Role:** Tell Claude: *"You are my Junior Policy Analyst. I am the Senior Architect. Your job is to research \@brazil_ndc.pdf and tell me if it mentions 'Methane' anywhere."*

3.  **Enforce the Plan:** Before it answers, say: *"Use /plan to tell me how you will search the document and what you will do if the word 'Methane' is used in different units (e.g., tons vs. percentages)."*

4.  **Execute & Test:** Have it find the data, then use /test to verify that the page number it cited actually exists.

**By doing this, you aren't just "chatting"---you are practicing "Agent Orchestration," which is the core skill of a 2026 Software Engineer.**

Welcome to **Week 2 of CS146S: The Anatomy of Coding Agents**.

In Week 1, we treated the AI as a single "Junior Developer." This week, we go deeper. We aren't just giving the AI a task; we are looking at the **internal architecture** that makes an agent "Agentic."

Week 2 Core Concept: The "Thinking" Architecture
--------------------------------------------------

Week 2 moves from "Simple Prompting" to **Cognitive Architectures**. Instead of a straight line (Prompt -\> Response), we build a **Loop** (Reason -\> Act -\> Observe).

**1. The ReAct Pattern (Reason + Act)**

This is the "DNA" of Claude Code and the multi-agent systems you learned in CrewAI.

-   **Reasoning:** Before doing anything, the agent must generate a "Thought" trace. This is why you see Claude Code saying *"I will now read the file to find the rubric\..."*

-   **Acting:** The agent chooses a **Tool** (like ls, grep, or cat).

-   **Observing:** The agent looks at what the tool returned. If the tool says "File not found," the agent doesn't give up; it **reasons** again: *"Ah, I looked in the wrong folder, let me try /docs instead."*

**2. Reflection: The Self-Correction Engine**

Week 2 emphasizes **Reflection**. A "Modern Software Developer" doesn't just trust the first output. You build a system where:

-   **Drafting Agent** creates the code.

-   **Reflecting Agent** looks at the code and says, *"Wait, you missed the edge case where the carbon tax is zero."*

-   **Finalizing Agent** fixes it.

**The "2026 SOTA" Lesson: The "System Prompt" is the OS**

In Week 2, Mihail Eric teaches that the **System Prompt** for an agent is effectively its "Operating System."

-   **Bad System Prompt:** "You are a helpful assistant." (The AI has no guardrails).

-   **Agentic System Prompt:** "You are an NDC Auditor. You have access to a terminal. You must verify every claim against the \@Policy_Rubric. If a number is missing, you must flag it as 'Insufficient Data'."

**3. Synthesized Takeaways for Your Climate Project**

-   **Agentic Drift:** Week 2 warns that the longer an agent works, the more likely it is to "drift" or forget the original mission.

    -   *Correction Strategy:* Use **"Checkpointing."** Every time Claude Code finishes an audit section, have it write a summary to a CHECKPOINT.md file. This acts as "External Memory."

-   **Tool-Use Integrity:** Don't just give Claude "Full Disk Access." Week 2 teaches **Principle of Least Privilege**. Only point Claude to the specific climate folders it needs. This protects your \$2.00 from "hallucinated deletions."

**Your Week 2 Lab Exercise (In Claude Code)**

Let's practice the **Reflection Pattern** we discussed. We are going to make Claude "fight" with itself to get a more accurate result.

1.  **Open Claude Code.**

2.  **Step 1 (Draft):** claude "Read \@brazil_ndc.pdf and write a 1-paragraph summary of their 2030 methane goal."

3.  **Step 2 (Reflect):** Once it finishes, say: claude "Now, act as a Skeptical Auditor. Review your own summary. Did you miss any footnotes or conditional statements that make this goal less ambitious than it sounds?"

4.  **Step 3 (Finalize):** claude "Based on that critique, rewrite the summary to be 100% accurate and cautious."

**Why this matters:** You'll notice that in Step 2, Claude almost always finds a "catch" it ignored in Step 1. This is the **Multi-Agent mindset** applied to a single interface.

**Summary of the Week 2 "Shift"**

-   **Week 1:** AI is a **Person** (Junior Dev).

-   **Week 2:** AI is a **System** (A loop of Thinking, Acting, and Critiquing).

**Next up in Week 3, we explore "The AI IDE" (Cursor, VS Code + MCP) and how to turn your MacBook into a professional-grade AI Factory. Ready for the next level?**

Welcome to **Week 3 of CS146S: The AI IDE & Professional Workflows**.

In Week 2, we mastered the "Thinking" loop (ReAct). This week, we move from the terminal-only view to the **Integrated Environment**. We are turning your MacBook from a personal computer into a **Professional AI Factory**. We shift from "Prompting" to **Context Engineering**.

Week 3 Core Concept: Context Engineering (The Memory Tiering)
-------------------------------------------------------------

Week 3 introduces the most important technical shift of 2026: **Context is a managed resource, not a passive input.** In a professional workflow, we don't just "talk" to Claude; we curate exactly what it "remembers" using a hierarchical system.

**1. The Three-Tier Memory Hierarchy**

Claude Code and modern IDEs (like Cursor) use a structured memory system so you don't have to repeat yourself.

-   **User-Level (\~/.claude/CLAUDE.md):** Your "Global Identity." This is where you store things like *"I am a Climate Researcher"* or *"Always use Python 3.12."* It follows you into every folder.

-   **Project-Level (./CLAUDE.md):** The "Team Standards." This is what /init creates. It defines the specific tech stack for your **Climate Watch** project (e.g., *"Use \@Policy_Rubric.md for every audit"*).

-   **Dynamic/Folder-Level Memory:** You can place a CLAUDE.md inside a subfolder (like /Audits/Brazil/). When Claude enters that folder, it "boots up" specific knowledge for that country, keeping the memory lean and accurate.

**2. MCP (Model Context Protocol): The "USB-C" for AI**

If the memory hierarchy is the "Brain," **MCP** is the "Central Nervous System."

-   **The Problem:** Normally, Claude can't "see" your Google Drive, your SQL database, or a live Climate API.

-   **The Solution:** MCP is a standardized protocol that lets you "plug in" external tools. Instead of downloading a PDF, you connect an **MCP Google Drive Server**, and Claude can "reach out" and grab the file itself.

**The "2026 SOTA" Lesson: Specs are the New Source Code**

In Week 3, we teach the **"Spec-First" Workflow**. Professional developers in 2026 almost never write raw code first.

-   **Vibe Coding vs. Engineering:** Vibe coding is saying "Make a climate app." Engineering is writing a Spec.md that defines the input, output, and constraints.

-   **The Workflow:** You write the **Intent** (the Spec) \$\\rightarrow\$ The Agent generates the **Implementation** (the Code) \$\\rightarrow\$ You verify the **Diff**. If there is an error, you **never** fix the code; you fix the **Spec** and have the Agent regenerate. This prevents "Spaghetti Logic."

**3. Synthesized Takeaways for Your Climate Project**

-   **Context Poisoning:** If you are auditing Brazil, do not let Kenya's files stay in the "Active Context." Week 3 teaches you to use the **/compact** command to prune old thoughts and keep the "Signal-to-Noise" ratio high.

-   **The MCP Advantage:** For your Climate Watch project, you should eventually build or use an **MCP Brave Search Server**. This allows Claude to search the live web for the *latest* climate updates without you having to manually find and download the PDFs.

**Your Week 3 Lab Exercise (The AI Factory Setup)**

We are going to move your Climate Watch project from a "messy folder" to a "Professional AI Factory."

**Part 1: The Global Identity**

1.  Open your terminal.

2.  Create your global identity: nano \~/.claude/CLAUDE.md

3.  Add this:

> *"I am a Senior Climate Policy Auditor. My audits must be skeptical, data-driven, and cite specific page numbers from source PDFs."*

4.  Save and exit. Now, Claude will *always* know your "vibe" without you typing it.

**Part 2: The Project Spec**

1.  Navigate to your Climate project folder.

2.  Create a file called Scraper_Spec.md.

3.  Write:

> *"Task: Create a tool that takes a country name and searches for their 'NDC 2025 update' PDF on Google. Tools: Use the Brave Search MCP."*

4.  Run Claude: claude "Read \@Scraper_Spec.md and use the Brave Search tool to find the PDF link for Brazil."

**Why this matters:** You aren't just "chatting." You are using **Memory (Global Identity)** + **Intent (Spec)** + **Tools (MCP)** to automate a complex research task.

**Summary of the Week 3 "Shift"**

-   **Week 1:** AI is a **Person** (Junior Dev).

-   **Week 2:** AI is a **System** (The Thinking Loop).

-   **Week 3:** AI is an **Environment** (The Memory Hierarchy & Tooling).

Week 4 Preview: Subagent Orchestration (The "Agent Factory")

Ready to move to Week 4? We will learn how to make one Claude instance "hire" five other Claude instances to work in parallel on your Climate audits. **Shall we continue to the deep-dive for Week 4?**

Welcome to **Week 4 of CS146S: Subagent Orchestration (The "Agent Factory")**.

In Week 3, we turned your MacBook into a factory by setting up the environment. This week, we learn how to manage the **"Workers"** inside that factory. We are moving from a single conversation to a **Distributed System**.

Week 4 Core Concept: Delegation & Parallelism
---------------------------------------------

Week 4 is about the transition from "Doing" to **"Delegating."** In 2026, a high-level developer doesn't ask an agent to do everything in one go; they ask the agent to **Orchestrate Subagents**.

**1. The Manager-Worker Pattern**

This is the internal architecture of Claude Code when it handles complex tasks.

-   **The Manager (Parent Agent):** Holds the "Global State" and the ultimate goal (e.g., "Audit all G20 countries"). It does not read the files itself.

-   **The Workers (Subagents):** These are temporary, stateless instances spawned to do one thing: "Read Brazil's NDC," "Extract Methane Data," or "Check Page 42 for a signature."

-   **The Hand-off:** The most critical point of failure. If the Manager doesn't give the Worker a clear **Context Snippet**, the Worker will hallucinate.

**2. Parallel Processing (The "Speed-up")**

Unlike a human, Claude Code can "think" in parallel.

-   **Sequential:** Audit Brazil → Finish → Audit Kenya → Finish. (Slow, high risk of "Context Drift").

-   **Parallel:** Spawn Subagent A (Brazil) + Subagent B (Kenya) + Subagent C (USA). (Fast, zero cross-contamination).

**The "2026 SOTA" Lesson: Orchestration vs. Execution**

Mihail Eric argues that in 2026, **Execution is a commodity; Orchestration is the skill.** \* Any AI can write a Python script. Very few humans can design a "System of Agents" that doesn't get stuck in a recursive loop or blow the budget.

-   **The "Hand-off" Protocol:** SOTA developers spend their time writing the **Interface** between agents. You define exactly what a Worker must return to the Manager (e.g., "Return only a JSON object with three keys: country, goal_year, methane_reduction").

**3. Synthesized Takeaways for Your Climate Project**

-   **Avoid "Giant" Tasks:** If you tell Claude Code to "Audit these 10 PDFs," it will likely fail or get "lazy" by the 4th one.

-   **The Parallel Strategy:** Instead, tell it: *"I want you to spawn a sub-task for each PDF in the /Inbox folder. Each sub-task should use \@Policy_Rubric and output a unique .md file."*

-   **Budget Guardrail:** Parallelism is a **Token Monster**. Each subagent "boots up" with its own system prompt. In 2026, we use **"Context Stripping"**---only giving the subagent the specific pages it needs, not the whole 200-page document.

**Your Week 4 Lab Exercise (The Multi-Agent Parallel Audit)**

We are going to force Claude Code to act as a Manager and hire "Workers" to handle your climate data.

1.  **Open Claude Code** in your project folder.

2.  **The Command:** \> claude "I need to audit \@brazil_ndc.pdf and \@kenya_ndc.pdf. Please spawn two separate sub-tasks to analyze them in parallel using \@Policy_Rubric. Do not merge the contexts. Give me two separate status reports."

3.  **Observe the "Hand-off":** Watch the terminal. You will see lines like:

    -   \> Starting sub-task for Brazil\...

    -   \> Starting sub-task for Kenya\...

4.  **Verify the Output:** Check if it created two distinct "thought traces."

**Why this matters:** This is the only way to scale your Climate Watch project to 195 countries. If you try to do it in one big chat, the AI will eventually "hallucinate" Kenya's data into Brazil's report.

**Summary of the Week 4 "Shift"**

-   **Week 1:** AI is a **Person** (Junior Dev).

-   **Week 2:** AI is a **System** (The Thinking Loop).

-   **Week 3:** AI is an **Environment** (Memory & Tools).

-   **Week 4:** AI is a **Team** (Manager & Subagents).

**Week 5 Preview: Shell Intelligence & Safety Guardrails**

Next week, we give the agents "Hands." We explore how to let Claude run bash scripts, manage your Git commits, and why you should **never** use the -y flag until you've mastered Week 5.

**Ready to move to Week 5, or do you want to try spawning some subagents first?**

Welcome to **Week 5 of CS146S: The Modern Terminal & Shell Intelligence**.

In Week 4, we learned how to "manage" subagents as workers. This week, we give those workers **"Hands"** via the terminal. We are shifting from treating the terminal as a place to "type commands" to treating it as a **Natural Language Command Center** where you manage **Intent** rather than **Syntax**.

Week 5 Core Concept: Predictive & Intent-Based Shell
----------------------------------------------------

Week 5 moves the terminal from a "Passive Tool" to an **"Active Partner."** Instead of you memorizing complex grep or sed flags, you describe the *state* you want the file system to be in, and the agent translates that into a shell-level "plan."

**1. The Command Composition Pattern**

This is how Claude Code translates your natural language into a functional shell script.

-   **Contextual Prediction:** Unlike a standard terminal, an AI-powered terminal sees your project structure. If you say "Run the audit," it doesn't just guess; it checks for a Makefile, a requirements.txt, or a main.py and builds the command accordingly.

-   **Complex Piping:** The agent can compose multi-stage pipelines (e.g., find -\> grep -\> awk -\> sort) in milliseconds---tasks that usually take a senior dev minutes to write and debug.

**2. The Permission Handshake (Safety Guardrails)**

This is the most critical mechanism for your MacBook's safety.

-   **The Dry Run:** Before any execution, the agent generates a "Plan." This plan is an intermediate representation of the shell commands.

-   **Approval Gating:** In 2026, we never use the "Auto-approve" (-y) flag for shell commands. The agent must show you the exact command (e.g., mv ./Inbox/\*.pdf ./Audits/) and wait for your /approve. This is your "Firewall" against accidental file deletion.

**The "2026 SOTA" Lesson: The Terminal is an API for your OS**

In Week 5, Mihail Eric teaches that the command line is no longer just for developers---it is the **API for the AI**.

-   **The "Black Box" Problem:** Traditional terminals are black boxes to AI.

-   **The Modern Solution:** Tools like **Warp** or **Claude Code** provide "Structured Output." The terminal isn't just printing text; it's passing structured data back to the AI brain so it can "Observe" and "Correct" if a command fails.

**3. Synthesized Takeaways for Your Climate Project**

-   **Automated Data Filing:** You can now automate your "Climate Watch" housekeeping. Instead of dragging and dropping, tell Claude: *"Every Monday, find any new PDF in /Downloads that mentions 'NDC' and move it to my /Climate_Audit/Inbox."*

-   **Shell-Level Verification:** Use the shell to check for "Empty Audits." You can ask: *"Scan the /Audits folder. If any .md file is less than 1KB, it's probably a failed audit---delete it and prepare a list of countries I need to re-run."*

**Your Week 5 Lab Exercise (The Automated Pipeline)**

We are going to use the Shell to perform "Housekeeping" on your climate files---a task that would be tedious by hand.

1.  **Open Claude Code.**

2.  **Step 1 (The Search):** \> claude "Search my current directory for all PDF files. For each file, check if it contains the word 'Methane'. Create a new folder called /Methane_Focus and move the matching files there."

3.  **Step 2 (The Plan):** Before you approve, read the /plan. Does it use grep -i (case-insensitive)? Does it use mkdir -p? This is you "Reviewing the Junior Dev."

4.  **Step 3 (The Clean-up):** Once the files are moved, run:

> claude "Now, generate a text file inside /Methane_Focus called 'index.txt' that lists the original filenames and their sizes."

**Why this matters:** You've just performed a complex data-engineering task without knowing the specific shell commands for finding strings inside PDFs. You managed the **Intent**, and Claude handled the **Plumbing**.

**Summary of the Week 5 "Shift"**

-   **Week 1-4:** AI is a **Person**, a **System**, an **Environment**, and a **Team**.

-   **Week 5:** AI is your **Operator** (It has hands in your OS).

**Week 6 Preview: AI Testing & Security**

Ready for Week 6? We dive into **"Adversarial Verification."** We will learn how to make one AI try to "break" the audit of another AI to ensure 100% accuracy. **Shall we proceed?**

Welcome to **Week 6 of CS146S: AI Testing & Security**.

In Week 5, we gave the agent "Hands" to operate your terminal. This week, we learn how to **Restrain** those hands and **Verify** the brain. We shift from "Productivity" to **"Assurance."** \-\--

Week 6 Core Concept: Adversarial Verification (The "Critic" Pattern)
----------------------------------------------------------------------

Week 6 introduces the most vital engineering pattern of 2026: **Adversarial Verification**. Because LLMs are probabilistic, you can never trust a single output 100%. In a professional pipeline, we use a "Double-Agent" architecture.

**1. The Worker vs. The Critic**

Instead of a human manually checking every line of an audit, we deploy a second, independent agent whose **only objective** is to find flaws in the first agent's work.

-   **The Worker (Primary Agent):** Focused on completion and "The Vibe" (e.g., summarizing the NDC).

-   **The Critic (Adversarial Agent):** Focused on **falsification**. It searches for "hallucination triggers"---numbers that don't exist, mismatched units (metric tons vs. kg), or broken logic.

**2. Deterministic vs. Probabilistic Testing**

-   **Traditional Testing (Deterministic):** You write a test where 2+2 must equal 4.

-   **AI-Native Testing (Probabilistic):** You use **"Decision Receipts."** You don't just check the final answer; you force the AI to log its **Chain of Thought (CoT)**. Week 6 teaches that if the "Reasoning" is flawed, the "Answer" is invalid, even if it looks correct.

**The "2026 SOTA" Lesson: Agentic Sandbox & Least Privilege**

Mihail Eric's key lecture this week is on **The Sandbox**. In 2026, we never run agent-generated code on our "bare metal" MacBook.

-   **Agentic Isolation:** Professionals use **Docker-based MCPs**. When Claude Code writes a script to analyze your climate data, it should run inside a restricted container that has **no network access** and **no access to your private files**.

-   **Context Rot:** We address the "10,000-token fatigue." As a session gets longer, the AI's "Security Guardrails" weaken (this is known as *Context Rot*). SOTA devs use the /clear command every 30 minutes to "re-harden" the agent's logic.

**3. Synthesized Takeaways for Your Climate Project**

-   **The "Hallucination Hack":** When auditing an NDC, always ask for **"Page-Level Citations."** If the AI can't point to a specific page number, mark the data as "High Risk."

-   **Multi-Model Voting:** For critical data (like a country's Methane target), use two different models (e.g., Claude 3.5 and Gemini 1.5). If they disagree on the number, **flag it for a human.**

**Your Week 6 Lab Exercise (The Adversarial Audit)**

We are going to perform an "Adversarial Stress Test" on your Brazil NDC audit to see if we can catch a hallucination.

1.  **Open Claude Code.**

2.  **Phase 1 (The Worker):**

> claude "Read \@brazil_ndc.pdf and find their 2030 carbon reduction percentage. Provide a 1-sentence answer."

3.  **Phase 2 (The Critic - The Attack):** Once it answers, type:

> claude "Now, act as a Skeptical Auditor. Your goal is to prove that the previous answer is a hallucination. Check page numbers, check if the percentage is 'conditional' vs 'unconditional', and look for conflicting numbers in the appendices."

4.  **Phase 3 (The Synthesis):** \> claude "Based on the Critic's findings, rewrite the final data point with 100% confidence and include the citation."

**Why this matters:** You'll often find that the Critic discovers the percentage was "Conditional on international funding"---a detail the Worker agent initially ignored to provide a "clean" answer.

**Summary of the Week 6 "Shift"**

-   **Week 1-5:** Learning to **Build** faster.

-   **Week 6:** Learning to **Trust** slower.

**Week 7 Preview: Modern Software Support & Maintenance**

Ready for Week 7? We tackle **"Technical Debt."** We'll learn how to use AI to clean up the messy code and inconsistent folders you've created over the last 6 weeks. **Shall we move on?**

Welcome to **Week 7 of CS146S: Modern Software Support & Maintenance**.

In Week 6, we learned how to "distrust" the AI and build adversarial firewalls. This week, we deal with the inevitable reality of any long-term project: **Entropy**. Your "Climate Watch" project is now seven weeks old. You likely have inconsistent naming conventions, old versions of prompts, and a tools/ folder that looks like a junk drawer.

Week 7 Core Concept: AI-Native Refactoring & Schema Alignment
-------------------------------------------------------------

Week 7 introduces the concept of **"Continuous Refactoring."** In 2026, we don't wait for "Refactor Month." We treat the codebase as a living organism that the AI constantly prunes.

**1. Intent-Preserving Transformations**

Traditional refactoring is manual and error-prone. AI-native refactoring uses the AI to rewrite code to be more efficient while strictly preserving the **Intent** (your original Spec).

-   **The Transformation:** Moving from a script that "just works" to a modular system that can be scaled.

-   **Schema Drift:** As you've audited more countries, you've probably changed your mind on how the data should look. Week 7 teaches how to use an agent to "back-migrate" old data to match your new, improved rubric.

**2. Living Documentation (The "Self-Explaining" Repo)**

Documentation is usually the first thing to die in a project.

-   **Agentic Documentation:** In 2026, we don't write README.md files; we let the AI generate them based on the current state of the code.

-   **The "Context-Aware" Guide:** We teach the agent to create "Onboarding Guides" for *other* agents so that if you spawn a new Subagent, it immediately knows the project's history.

**The "2026 SOTA" Lesson: Code is a Liability, Intent is the Asset**

Mihail Eric's core thesis this week is radical: **Source code is increasingly disposable.**

-   If your Audit_Spec.md is perfect, it doesn't matter if the Python code is messy. You can simply ask Claude Code to *"Delete all the Python and rewrite it from scratch using a faster library."* \* SOTA developers in 2026 focus 90% of their maintenance on the **Specs** and **Tests**. They treat the actual .py or .js files as temporary artifacts generated by the AI to fulfill the Spec.

**3. Synthesized Takeaways for Your Climate Project**

-   **Standardize the Vault:** Your Obsidian notes might be inconsistent. Use Week 7's logic to tell Claude: *"Read all notes in /Obsidian/Brazil and /Obsidian/Kenya. Make sure they use the exact same header structure. If a section is missing, mark it as \[TODO\]."*

-   **The "Fresh Start" Command:** If your script for scraping PDFs has become too complex, use the "Disposable Code" mindset. Say: *"Claude, this script is messy. Read the original \@Audit_Spec.md and rewrite the script from scratch to be 50% shorter."*

**Your Week 7 Lab Exercise (The Project Cleanup)**

We are going to perform "Technical Debt" collection on your Climate Watch project.

1.  **Open Claude Code.**

2.  **Step 1 (Audit the Repo):**

> claude "Scan my project directory. Find all scripts that are over 100 lines long and identify any redundant functions. Create a 'Cleanup Plan' in cleanup.md."

3.  **Step 2 (The Unified Schema):**

> claude "I have changed the \@Policy_Rubric.md to include a new 'Social Equity' score. Read my previous 3 audits and update them to include this new section, even if you have to leave it blank for now."

4.  **Step 3 (Living Docs):**

> claude "Generate a professional README.md that explains how this project works, including the tools in /scripts and the data structure in /Audits. Use my global identity in \~/.claude/CLAUDE.md to set the tone."

**Why this matters:** You are preventing your project from becoming "AI Spaghetti." By forcing the agent to clean up after itself, you ensure the context window remains small and efficient (saving your **\$2.00 budget**).

**Summary of the Week 7 "Shift"**

-   **Weeks 1-6:** Adding **Features** and **Accuracy**.

-   **Week 7:** Adding **Sustainability** and **Cleanliness**.

**Week 8 Preview: Automated UI & App Building**

Ready to move to Week 8? We move from the terminal to the **Browser**. We will learn how to use "Intent-to-UI" to build a beautiful dashboard for your Climate Watch results so you can actually *see* the data you've been auditing.

Welcome to **Week 8 of CS146S: Automated UI & App Building**.

In Week 7, we focused on "The Cleanup"---ensuring our code was sustainable. This week, we make the jump from the terminal to the browser. We are moving from "Logic" to **"Presentation."**

Week 8 Core Concept: Intent-to-Interface (GenUI)
------------------------------------------------

The most radical shift in 2026 is the death of the "Static Frontend." In a professional AI workflow, we no longer spend weeks hand-coding CSS or aligning divs. Instead, we use **Generative UI (GenUI)**.

**1. The "Vibe Coding" Stack**

Mihail Eric defines the 2026 SOTA stack as a combination of specialized tools:

-   **v0 (by Vercel):** The gold standard for **Component Generation**. You describe a UI (e.g., *"A dashboard for tracking carbon offsets with real-time charts"*), and it generates high-quality React code using shadcn/ui and Tailwind.

-   **Lovable & Bolt.new:** These are **Full-Stack Visionaries**. They don't just give you code; they provision a database (Supabase), set up authentication, and deploy the app to a live URL in minutes.

-   **The Orchestrator's Role:** Your job is no longer to "write" the UI, but to provide the **"Design Intent"** and ensure the data from your Week 4/5 agents flows correctly into these visual components.

**2. Liquid Design Systems**

In 2026, we don't build "pages"; we build **Rules**.

-   **Traditional UI:** A fixed layout that looks the same for everyone.

-   **Liquid UI:** An interface that restructures itself based on the user's current goal. If a user is looking for "Methane leaks," the UI automatically promotes the Methane charts to the top and dims the irrelevant data.

**The "2026 SOTA" Lesson: From "How it Looks" to "How it Behaves"**

The core lecture this week is: **"UX is a Living System."**

-   **Zero UI:** For your Climate project, sometimes the "best UI" is no UI. It might be a push notification to a policymaker's phone that says: *"Brazil just updated their NDC---click here to see the 3% change in Methane targets."*

-   **Ghost Actions:** We use "lightly shaded" UI elements to show what the AI *plans* to do next, allowing the human to "steer" the system with simple gestures rather than complex menus.

**3. Synthesized Takeaways for Your Climate Project**

-   **The Climate Dashboard:** You have weeks of audit data sitting in Markdown files. This week, you will use **v0** to generate a "Climate Watch Leaderboard."

-   **Intent-Based Navigation:** Instead of building a complex "Search" page, you'll build a single prompt bar: *"Show me all countries that are failing their 2030 targets."* The UI will generate the necessary table on the fly.

**Your Week 8 Lab Exercise (The Instant Dashboard)**

We are going to take your "Climate Watch" project and give it a face.

1.  **Open v0.dev or Lovable.dev.**

2.  **The Prompt:** \> *"Build a professional climate policy dashboard. It should have a sidebar for 'Country Selection' and a main area with three cards: 'Target vs. Reality', 'Methane Progress', and 'Policy Skepticism Score'. Use a dark-mode 'Sustainability' aesthetic (deep greens and slate grays)."*

3.  **Iterate via "Vibes":** Don't like the charts? Don't touch the code. Tell the AI:

> *"Make the charts 'Glassmorphic' and add a real-time pulse animation to the Skepticism Score if it's over 80%."*

4.  **Connect the Data:** Use **Claude Code** to write a simple "bridge" script that takes your JSON audits from Week 4 and feeds them into this new UI.

**Why this matters:** You just built a dashboard in 20 minutes that would have taken a frontend team two weeks in 2023. You are focusing on the **Value** (the climate insights) rather than the **Vessel** (the React code).

**Summary of the Week 8 "Shift"**

-   **Week 1-7:** Building the **Brain** and **Hands**.

-   **Week 8:** Building the **Eyes** (Visualization and User Interaction).

**Week 9 Preview: Agents Post-Deployment & Observability**

Ready for Week 9? Once your app is live, how do you know if the AI is still "thinking" correctly? We explore **Agentic Monitoring**---making sure your climate factory doesn't start "hallucinating" once you stop watching it.

**Shall we move to Week 9?**

Welcome to **Week 9 of CS146S: AgentOps & Observability**.

In Week 8, we gave your Climate Watch project a "Face" (The UI). This week, we learn how to monitor its **"Heartbeat."** Now that your agents are running autonomously, how do you know if they are still making sense, staying on budget, or getting stuck in a logic loop while you sleep?

Week 9 Core Concept: Agentic Observability (The MELT+R Framework)
-----------------------------------------------------------------

In 2026, standard "Monitoring" (checking if a server is up) is dead. We use **AgentOps**. We move from tracking *errors* to tracking **Reasoning Traces**.

**1. The MELT+R Framework**

Professional agent operators monitor five key signals:

-   **M (Metrics):** Token usage, latency, and cost per audit.

-   **E (Events):** When a subagent starts, fails, or hands off to another.

-   **L (Logs):** Raw text outputs from the LLM.

-   **T (Traces):** The end-to-end "breadcrumb trail" of a request across multiple agents.

-   **R (Reasoning):** **New for 2026.** We monitor the "Chain of Thought." If an agent's reasoning becomes repetitive, it's a sign of a **Logic Loop**.

**2. Token Velocity & Loop Detection**

One of the most dangerous (and expensive) failures in an agentic system is the **Recursive Loop**.

-   **Example:** Agent A asks for a file \$\\rightarrow\$ Tool returns "Error" \$\\rightarrow\$ Agent A asks again \$\\rightarrow\$ Tool returns "Error."

-   **The Fix:** We implement **Budget Guardrails**. If an agent consumes more than **\$0.50** on a single task, or its "Token Velocity" spikes without progress, the system automatically kills the process and alerts you.

**The "2026 SOTA" Lesson: The "Black Box" is an Audit Risk**

Mihail Eric's lecture this week focuses on **Governance**.

-   In 2026, if an AI agent makes a decision (like rejecting a climate credit), you must provide a **"Decision Receipt."** \* **SOTA tools (like AgentOps.io or LangSmith)** allow you to "Time Travel." You can rewind an agent's memory to the exact second it made a mistake, fix the prompt, and "Replay" the session to see if it improves.

**3. Synthesized Takeaways for Your Climate Project**

-   **Cost Attribution:** Use tags in your code so you know exactly which country is costing you the most. *"Is Brazil's NDC 10x more expensive to audit than Kenya's because the PDF is messier?"*

-   **The "Vibe Check" Monitor:** Set up a simple automated test that runs every 24 hours. It asks: *"Did any of yesterday's audits result in a '0' score?"* If yes, it flags it for human review, as a '0' is usually a sign of a tool failure, not a perfect climate policy.

**Your Week 9 Lab Exercise (The Operational Dashboard)**

We are going to instrument your Climate Watch factory so you can see under the hood.

1.  **Open Claude Code.**

2.  **Step 1 (Install the Monitor):**

> claude "Install the AgentOps SDK and wrap my main audit script. I want to track every tool call to the PDF parser."

3.  **Step 2 (The Loop Test):** Purposely give Claude a broken file path.

> claude "Try to audit \@non_existent_file.pdf and show me how you handle the error. Do you retry? How many times?"

4.  **Step 3 (The Cost Report):** \> claude "Analyze my session logs. How many tokens did we use for the last 5 audits? Estimate the total cost in USD based on Claude 3.5 Sonnet pricing."

**Why this matters:** You are moving from a "Hobbyist" who hopes it works to an "Operator" who **knows** it works. This is what separates a student project from a production-grade climate intelligence platform.

**Summary of the Week 9 "Shift"**

-   **Weeks 1-8:** Building the **Machine**.

-   **Week 9:** Building the **Dashboard** to manage the machine.

**Week 10 Preview: The Sovereign Developer & Beyond**

Ready for the **Grand Finale**? In Week 10, we look at the future of the industry. We discuss the "Sovereign Developer" (one human, a thousand agents) and how you will use these skills to stay relevant as AI continues to evolve.

**Shall we move to the final week?**

Welcome to **Week 10 of CS146S: The Sovereign Developer & The Final Synthesis**.

You have spent nine weeks evolving from a "Prompter" to an "Orchestrator." In this final week, Mihail Eric brings everything together. We move from building a factory to being the **Sovereign** of your own technological empire.

**Week 10 Core Concept: The Sovereign Developer**

In 2026, we define the "Sovereign Developer" as a single human who possesses the **agency, choice, and infrastructure** to operate at the scale of a traditional 50-person engineering firm.

**1. The AI-Native Lifecycle**

The traditional Software Development Lifecycle (SDLC) is dead. In the Sovereign model, the cycles of *Plan -\> Code -\> Test -\> Deploy* collapse into a single continuous loop managed by agents.

-   **Problem Decomposition:** You don't "code" features; you "decompose" problems into agent-sized chunks.

-   **The Agent-Friendly Codebase:** You've learned to write code that isn't just readable for humans, but **optimized for machines**. This means consistent interfaces, strict typing, and comprehensive "Agent-Readmes."

**2. Strategic Interdependence**

Sovereignty doesn't mean doing everything yourself---it means **controlling the key points of your stack.**

-   **Infrastructure Sovereignty:** You aren't just a tenant on a cloud; you understand how to use MCPs and local containers to ensure your "Climate Watch" project stays alive even if a specific vendor goes down.

-   **The Shift from Execution to Vision:** As AI handles 90% of the implementation, your value as an engineer shifts to **Judgment**. You are the "Validator of Reality" in a world of plausible-looking AI hallucinations.

**The "2026 SOTA" Lesson: The Human-in-the-Loop is the CEO**

The final lecture's takeaway is profound: **You are no longer the "Worker Bee"; you are the "Chief Engineering Officer."**

-   **Managing "Interns":** Treat every agent instance like an incredibly fast, perfectly obedient, but literal-minded intern.

-   **Economic Advantage:** Junior developers today have a "Startup Superpower." By being "AI-native," you can build systems that senior developers---resistant to changing their 20-year habits---deem "impossible" or "too risky."

**3. Final Synthesis for Your Climate Project**

Your **Climate Watch** project is now a **Sovereign System**:

1.  **Memory:** It knows your identity and policy rubric via CLAUDE.md.

2.  **Hands:** It uses the Shell to scrape and organize PDFs autonomously.

3.  **Team:** It spawns parallel subagents to audit different countries simultaneously.

4.  **Security:** It runs an "Adversarial Critic" to fact-check every methane target it finds.

5.  **Observability:** It tracks its own costs and reasoning traces, alerting you if it gets stuck.

**Your Final Lab Exercise: The "Sovereign Hand-off"**

This is your "graduation" task. You will set up a system that runs while you sleep.

1.  **The Directive:** Open Claude Code and give it a "Sovereign Mission":

> "I am going offline. Your mission is to audit the remaining 5 PDFs in /Inbox. For each one: 1) Extract the Methane goal. 2) Have a subagent critique the finding. 3) Update the JSON database. 4) If you hit a budget of \$1.00, stop and write a 'State of the Audit' report in CHECKPOINT.md."

2.  **The Verification:** When you return, don't check the code. Check the **Logic Receipt**. Look at the CHECKPOINT.md to see *why* it made the choices it did.

3.  **The Scale:** Realize that you can now do this for 1, 10, or 1,000 documents. You have scaled your **Intellect**, not your **Labor**.

**Summary of the 10-Week Evolution**

-   **Week 1:** AI as a **Person**.

-   **Week 5:** AI as an **Operator**.

-   **Week 10:** AI as an **Ecosystem**---and you are its Architect.
