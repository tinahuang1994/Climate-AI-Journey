# Obsidian + Claude Code: Building a Private Research System

*Created: March 2026 | Author: Tina Huang*

I want to show you how I am combining two tools---**Obsidian** and **Claude Code**---to move beyond simple AI "chats" and into a professional, automated research system. Think of this as a **private library** and a **dedicated researcher** working for you 24/7.

**1. Why This is the "Ultimate Power Couple"**

Separately, these are just tools; together, they create a system where our data stays private and the AI has "hands" to work with it.

-   **Obsidian (The Librarian, kind of like Notion):** This is a folder on my computer where I store all my notes. It is "private-first," meaning our data stays with us. It is excellent at linking ideas together, such as connecting "India" to "Renewable Subsidies."

    -   **For example:** For the **Climate Watch 2026 project**, I want to score an NDC based a rubric I defined. I can create a dedicated folder in my Obsidian vault called /Climate_Watch_2026.

    -   **The Blueprint:** Inside, I have a core note called **\@Policy_Rubric**. This is our "gold standard"---it contains the specific definitions and scoring criteria we've developed for what a high-quality National Determined Contribution (NDC) looks like.

    -   **The Raw Ingredients:** I have a sub-folder called /Source_Data where I drop the latest NDC PDFs and transcripts pulled from Climate Watch.

    -   **The Finished Meal:** When I give Claude an **Explicit Directive** to perform an audit, it doesn't just talk about it---it creates a brand new, timestamped file (e.g., Brazil_Audit_March2026.md) and saves it directly into a sub-folder called **/Audits**.

-   **Claude Code (The Engineer):** This is the AI "agent" that, unlike the standard Claude website, has "hands." It can open our Obsidian notes, read them, perform analysis, and write new reports directly into the folders.

> For now, if you only work in Claude Code, Claude will generate a file called Claude.md. This file remembers your preferences; however, if you exit your session, then Claude actually forgets them.

That is why we need to use Obsidian, because it will save all your preferences. For example:

> 1\. We will save the \@Policy_Rubric to grade an NDC inside Obsidian.
>
> 2\. Whenever we need to score a new NDC, Claude will always reference that rubric.
>
> However, I think using the Claude Code + Obsidian is just an interim step, because I would assume that Claude Code will very soon have its own function as an Obsidian plugin. That way, everything can be in just one tool. But this is what we're working with right now.

**2. The Golden Rule: The "Explicit Directive"**

Because the "Engineer" is working in our "Library," you must be a highly specific manager. Every session should start with a clear mission statement so the AI knows exactly which "ingredients" to use from the pantry.

-   **Climate Watch Example:** *"Open the file \@brazil_2025_ndc.pdf. Compare the methane targets on page 10 to the **\@Policy_Rubric** already in my Obsidian folder. Write the final audit to a new note in our /Audits folder."*

**3. Essential Tricks for World-Class Results**

Once you give an explicit order, we use these commands to ensure the work is perfect. Each trick is ranked by its importance to our workflow:

**A. The "Foundation" (/init)**

**Rank:** ⭐⭐⭐⭐⭐

This command introduces the Engineer to the Library. It sets the ground rules and ensures Claude knows that your Obsidian folder is its primary workspace.

-   **Climate Watch Example:** Use /init at the start of a new project to tell Claude: *"This folder contains all our Climate Watch data. Always format country names in ISO-3 codes."*

**B. The "Work Plan" (/plan)**

**Rank:** ⭐⭐⭐⭐⭐

Before asking Claude to analyze a massive file, use /plan. This tells the Engineer: *"Stop. Show me your step-by-step logic."*

-   **Climate Watch Example:** Ask for a /plan to compare India's 2022 vs. 2026 solar targets. Claude will outline the steps (e.g., "1. Open 2022 PDF, 2. Open 2026 PDF, 3. Calculate GW growth"). You approve this *before* it spends time reading the files.

-   **Note:** it's important to plan because you do, to make sure you like how Claude is approaching your task. I also plan with Gemini about project ideas. Also, you can throw Claude Code's plan to Gemini/Cursor agent to ask whether there is a better solution.

**C. The "Safety Inspector" (/test)**

**Rank:** ⭐⭐⭐⭐

Use /test to make the AI verify its own math and logic. It ensures our deliverables are bulletproof.

-   **Climate Watch Example:** After Claude writes a report on China's emissions, run /test. It will verify: *"Does the 2060 Net Zero date in the report match the raw data in the PDF?"* If there is a typo, it fixes it immediately.

**D. Surgical Focus (@ Mention)**

**Rank:** ⭐⭐⭐⭐

Since we already have files like **\@Policy_Rubric** in our folder, we use the @ symbol to point Claude's "eyes" exactly where to look.

-   **Climate Watch Example:** *"Analyze the gaps in the \@Mexico_NDC_Draft using the criteria in my **\@Policy_Rubric**."* This prevents the AI from using generic internet standards instead of *our* specific rules.

**E. The "Context Squeezer" (/compact)**

**Rank:** ⭐⭐⭐⭐⭐

This command summarizes the key decisions and changes made so far. It "wipes the slate" of messy chat history while keeping the essential context.

-   **Climate Watch Example:** If you've been debating 50 different data points for the EU, use /compact to boil it down to the final agreed-upon figures. This makes the AI faster and keeps the session cost-effective.

**Claude Code: The Command Cheat Sheet**

  **Command**     **Rank**   **What it does**                                **When to use it**
  --------------- ---------- ----------------------------------------------- -----------------------------------------
  **/init**       ⭐⭐⭐⭐⭐      Sets the project foundation and rules.          **Start here.** Every new project.
  **/plan**       ⭐⭐⭐⭐⭐      Forces Claude to "Think" before "Acting."   Before any multi-step task.
  **/compact**    ⭐⭐⭐⭐⭐      Cleans chat memory to save costs.               When the AI gets slow or "forgetful."
  **/test**       ⭐⭐⭐⭐       Auto-verifies your logic and math.              After every report or code change.
  **@ mention**   ⭐⭐⭐⭐       Focuses Claude on specific library files.       To avoid "Distracted AI" syndrome.
