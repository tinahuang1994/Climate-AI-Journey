# AI Agentic Design Patterns with AutoGen

*Created: March 2026 | Source: DeepLearning.AI — AI Agentic Design Patterns with AutoGen*

**🌟 Introduction: The "Group Chat" Paradigm**

If your previous LangChain courses taught you how to give AI a "filing cabinet" (RAG), and CrewAI taught you how to build a strict "assembly line," AutoGen teaches you how to build a **Dynamic Group Chat**.

AutoGen allows AI agents to text each other, debate, ask humans for help, and even write/run code on their own. This course outlines the 4 main "Patterns" (blueprints) you can use to build these chat rooms.

**🧠 Pattern 1: Reflection (The "Evaluator-Optimizer" Loop)**

**The Concept:** Standard AI writes a first draft and stops. In the Reflection pattern, you create a two-agent chat: a "Writer" and a "Critic." The Writer writes, and the Critic reviews it against a rubric. They loop back and forth until the Critic is satisfied.

**Your Case Study: The SBTi Navigator / Climate Triple Takes**

-   **The Problem:** When building the *SBTi Navigator*, you cannot afford for the AI to hallucinate a company's Scope 3 emissions.

-   **The AutoGen Solution:** You tell Claude Code to build a Reflection chat.

    -   **Agent 1 (The Analyst):** Reads the corporate report and extracts the numbers.

    -   **Agent 2 (The Auditor):** Acts as the Critic. It looks at Agent 1's numbers and says: *"Wait, you forgot to include supply chain travel. Fix this."*

    -   Agent 1 fixes it and sends it back. You only see the final, fact-checked result.

**🧠 Pattern 2: Sequential Chats (The "Relay Race")**

**The Concept:** A sequence of dependent chats where the output of Chat A becomes the starting context for Chat B. Crucially, it allows a "Human Proxy Agent" to jump in, answer a question, and pass that human context to the next AI.

**Your Case Study: The "No Thanks" App**

-   **The Problem:** You want to help people say no to their boss, but you need context about their specific workplace vibe before writing the email.

-   **The AutoGen Solution:** You build a Sequential Chat.

    -   **Chat 1 (Intake Bot & Human):** The AI asks you: *"Is your boss toxic, or just disorganized?"* You type: *"Disorganized."*

    -   **Chat 2 (Strategy Bot & Human):** The AI takes that info and asks: *"Do you want to offer a compromise, or just a hard no?"* You type: *"Compromise."*

    -   **Chat 3 (Writer Bot):** The AI takes the summary of the first two chats and generates the perfect, high-EQ Eisenhower Matrix email.

**🧠 Pattern 3: Tool Use (The Agent with "Hands")**

**The Concept:** AI agents are usually trapped in a chat window. "Tool Use" is the pattern of giving agents external tools, like a calculator, a web browser, or access to an API, which they can use *during* their conversation.

**Your Case Study: Climate Watch / NDC Analyst**

-   **The Problem:** The AI cannot analyze a Nationally Determined Contribution (NDC) if it doesn't have the latest PDF.

-   **The AutoGen Solution:** You build an Agent with Tools.

    -   You give the AutoGen bot a "Web Search Tool" and a "PDF Reader Tool."

    -   In the chat, the bot says: *"I need to analyze Brazil's 2026 climate goals. Let me use my Web Search Tool to find it."* It searches, downloads the PDF, reads it, and then writes the audit---all autonomously in the background.

**🧠 Pattern 4: Planning & Group Chat (The "Boardroom")**

**The Concept:** This is the ultimate, heavyweight architecture. Instead of a simple 1-on-1 chat, you put 4 or 5 different specialized agents in a room. You also add a "Planner Agent" whose only job is to manage the other bots, tell them who should speak next, and ensure the project stays on track.

**Your Case Study: Smoke Story V2**

-   **The Problem:** Analyzing open geospatial data for wildfires involves mapping, storytelling, and climate science---too much for one AI.

-   **The AutoGen Solution:** You create a Boardroom.

    -   **The Planner (CEO):** Receives your prompt: *"Tell a story about the California wildfires."*

    -   **The GIS Agent (Data Scientist):** The Planner tells the GIS Agent to fetch the open geospatial coordinates.

    -   **The Climate Expert (Scientist):** Looks at the coordinates and explains the wind patterns.

    -   **The Storyteller (Writer):** Takes the data and science and writes a beautiful, emotional narrative.

    -   They debate in the group chat until the Planner decides the story is perfect and hands it to you.

**🎓 Summary for your Notes**

-   **CrewAI** is for rigid, predictable pipelines (The Factory).

-   **AutoGen** is for fluid, conversational problem-solving (The Group Chat).

-   **Your Role:** You are the **Manager** of the group chat. You decide who is in the room, what tools they have, and when they need to stop and ask you (the human) for your opinion.
