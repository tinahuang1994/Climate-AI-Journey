# Claude Code: Beginner's Guide for Climate AI

*Created: March 2026 | Author: Tina Huang | Source: Anthropic Claude Code Docs + DeepLearning.AI*

> ⚠️ **Decay disclaimer:** Claude Code ships updates frequently. Specific commands, flags, and features described here may have changed. Use this as a conceptual foundation and verify current details at [claude.ai/code](https://claude.ai/code).

We are moving beyond simple chatbots and learning how to use **Claude Code**---a tool that doesn't just talk about work, but actually performs it.

Throughout this guide, we will use the **Climate Watch Project** as our example.

**The Case Study:** In this scenario, imagine we are using Claude Code as an **NDC Analyst**. A Nationally Determined Contribution (NDC) is a country's official plan to reduce emissions. Claude's job is to read these reports and score them according to a "Policy Rubric" (a set of rules) to see how well the country is doing.

**The Beginner's Guide to Claude Code**

**1. The Big Picture: What is Claude Code?**

Most people know Claude as a website where you type a question and get a text answer. **Claude Code** is different; it is an "agent" with "hands."

-   **From Chatbot to Agent:** While the website can only suggest text, Claude Code can open files on your computer, read them, and save new versions directly.

-   **The "Junior Developer" Mindset:** Think of Claude Code as a very smart junior assistant. It needs clear goals and supervision, but it handles the repetitive "grunt work" like reading 100-page NDCs for you.

-   **Local Access:** Because it lives on your computer, you don't have to copy and paste data. It works right where your climate files are stored.

**2. Getting Started (The Easy Way)**

You don't need to be a computer scientist. Claude Code lives in your **Terminal**---the text-based window on your computer.

-   **The Installation:** To get set up, follow this [Video Tutorial](https://www.youtube.com/watch?v=ntDIxaeo3Wg&t=1901s) which walks you through the installation step-by-step.

-   **The "Pay-As-You-Go" Tip:** When you sign up, you'll be asked to subscribe or "top up." If you're just starting out, **just top up \$5**. This gives you plenty of room to experiment without a heavy commitment.

-   **The First Run:** Once installed, type claude in your terminal and log in via your browser to link your account.

-   **The /init Command:** Once in your project folder (like "Climate Watch 2026"), type /init. This allows Claude to scan your files and understand your goals.

**3. Memory: CLAUDE.md & The Obsidian Upgrade**

To work effectively, Claude needs a "memory" of your project rules.

-   **Level 1: The Essential Memory (CLAUDE.md)**

> When you run /init, Claude creates a file called CLAUDE.md. Think of this as a "Sticky Note" on Claude's forehead. It tells Claude: *"Here is our project style, our naming rules, and how we check our work."*

-   **The Limitation:** CLAUDE.md is great for quick sessions, but it can feel "thin" or get cluttered as your project grows.

-   **Level 2: The Permanent Brain (Obsidian) --- *Optional but Recommended***

> To make Claude even smarter, you can use **Obsidian**, a free note-taking app. You don't *have* to use it, but it provides a "Permanent Brain" for your project.

-   **The Blueprint:** Instead of writing complex rules in a terminal, you save them as clean notes in Obsidian (like a **\@Policy_Rubric** that defines what a 'good' NDC looks like).

-   **The Librarian:** While Claude is the **Engineer** doing the work, Obsidian acts as the **Librarian**. Claude can reach into your library, read your "Gold Standard" rubrics, and save finished "Audits" directly back into your folders where they are easy to read.

**4. How to Talk to Your AI Teammate**

To get the best results, use these core strategies:

-   **The "@" Symbol:** To look at a specific file, type @ followed by the name (e.g., \@brazil_ndc.pdf) to "point" Claude to it.

-   **The /plan Command:** Before Claude changes anything, type /plan. This puts Claude in "Read-Only" mode. It will tell you exactly what it *intends* to do (e.g., "I will check Section 4 for methane targets") without changing files yet.

**5. Staying in Control**

You are always the boss. Claude Code is built with safety in mind.

-   **Permission Prompts:** Before Claude deletes a file or runs a command, it will ask for your "OK."

-   **Keeping it Fresh:** If a conversation gets too long, use /clear to start a fresh "thought" while keeping your files exactly as they are.

-   **The Finished Meal:** When Claude finishes, like creating a Brazil_Audit_2026.md file, it saves it directly into your folder for you to review in Obsidian.

**Prompt Template: The "Climate Watch" Auditor**

Copy and paste this into Claude Code to start your first analysis:

"I want to perform a Climate Watch Audit.

1.  Use **/plan** to show me how you will use my **\@Policy_Rubric** to analyze **\@brazil_ndc.pdf**.

2.  Once I approve, create a new file in my /Audits folder named **Brazil_Audit_2026.md**.

3.  Finally, use **/test** to verify the new file contains all the required sections from the rubric."

**Claude Code Cheat Sheet**

  **Command**   **What it does**                                     **Climate Watch Example**
  ------------- ---------------------------------------------------- ------------------------------------------------------
  claude        Starts the AI assistant.                             Type claude in your folder.
  /init         Sets up the initial memory (CLAUDE.md).              Run this first in a new project.
  /plan         **Read-only mode.** Claude explains the plan.        "Use /plan to outline how you'll grade this NDC."
  /clear        Wipes the current chat history for a fresh start.    Use this when switching from Brazil to Kenya.
  @             Points Claude to a specific file or folder.          "Read \@brazil_ndc.pdf"
  exit          Closes Claude Code.                                  Type exit when you're done.

**Learning**:

I also watched this [course](https://www.deeplearning.ai/short-courses/claude-code-a-highly-agentic-coding-assistant/) by Anthropic
