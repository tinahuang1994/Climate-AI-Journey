# Building Customized LLMs with OpenAI — Module 1: The Foundations of RAG and AI Agents

*Created: March 2026 | Source: Columbia University — Building Customized LLMs with OpenAI*

**🌟 Introduction: The Architecture of Truth**

Welcome to Module 1! In your previous projects (like *Smoke Story* and the *SBTi Navigator*), you learned how to prompt AI and build user interfaces. Now, we are moving into backend architecture.

The biggest problem with AI is that it hallucinates. If you ask it about a corporate sustainability report, it might make up the numbers. This module introduces the industry standard for fixing this: **Retrieval-Augmented Generation (RAG)**.

By the end of this study guide, you will understand the five core objectives of Module 1, explained in simple English using your actual projects as case studies.

**🧠 Objective 1: Understanding RAG & Its Applications**

**The Concept: The "Open Book Exam"** Standard AI models take a "closed-book exam." They answer questions based only on what they memorized during their training years ago. **RAG** turns this into an "open-book exam." It gives the AI a private library (your data) and forces it to look up the answer before speaking.

-   **R**etrieval: The system searches your private documents for relevant information.

-   **A**ugmented: It attaches those relevant paragraphs to your original prompt.

-   **G**eneration: The AI writes the final answer using *only* the attached data.

**Case Study: The SBTi Navigator** If you upload a 300-page corporate climate report, the AI cannot memorize it instantly. With RAG, when an auditor asks, *"What are the Scope 3 emissions for 2024?"*, the RAG system **retrieves** just page 45 (where the data lives), **augments** the prompt, and **generates** a perfectly accurate answer.

**🤖 Objective 2: Human Agents vs. LLM Agents**

**The Concept: From "Tool User" to "Autonomous Worker"** The course makes a critical distinction between how humans use computers and how AI is starting to use them.

-   **Human Agent:** *You* open a PDF, *you* hit Ctrl+F to find a keyword, and *you* copy the text into a spreadsheet. You are doing the labor.

-   **LLM Agent:** The AI is given a goal (e.g., "Audit this company"). The AI autonomously uses "tools" to do the work. It decides to open the PDF, it decides what to search, and it decides how to format the spreadsheet.

**Case Study: Claude Code as the NDC Analyst** In your *Climate Watch Project*, you experienced this firsthand. When you use ChatGPT on a website, it is just a chatbot. When you use **Claude Code** in your terminal, it acts as an LLM Agent. It has "hands." It reads your \@Policy_Rubric, opens the PDF, and writes the Brazil_Audit_2026.md file without you clicking a single button.

**🗄️ Objective 3: Vector Search (The "Smart Filing Cabinet")**

**The Concept: Searching by Meaning, Not Keywords** To make RAG work, the AI needs to find the right information instantly. Traditional search engines use *Keywords* (matching exact letters). AI uses **Vector Search**. A Vector Database takes a sentence and turns it into a long string of numbers (a "Vector" or "Embedding"), plotting it on a giant 3D mathematical map.

-   **Why it's a superpower:** Sentences that *mean* the same thing are placed physically close to each other on this map, even if they don't share any of the same words.

**Case Study: The "No Thanks" App** If a user types, *"My boss is dumping their busywork on my desk,"* a traditional keyword search would fail because the word "overworked" isn't there. Vector Search understands the *semantic meaning* of the sentence and immediately retrieves your advice framework for "Redirecting Urgent/Unimportant Tasks."

**🧪 Objective 4: Building & Testing with Synthetic Data**

**The Concept: The "Flight Simulator" for AI** Before you launch a customized LLM to the public, you need to test it. But what if you don't have enough real data yet? Or what if the real data is highly confidential? You use the AI to generate **Synthetic Data** (fake, but highly realistic data) to test your system.

**Case Study: Smoke Story Testing** Imagine it is winter, and there are no active wildfires in California. How do you test if your *Smoke Story* website works? You command the AI: *"Generate 50 rows of synthetic JSON data simulating a massive wildfire in Los Angeles County, including fake PM2.5 readings and wind speeds."* You feed this synthetic data into your RAG pipeline to ensure the storytelling feature works perfectly before the real fire season begins.

**🕸️ Objective 5: Text Analytics and Knowledge Graphs**

**The Concept: The "Detective's String Board"** Vector Search is amazing, but it has a blind spot: it is bad at connecting the dots across multiple documents. If you need to understand *relationships*, you use a **Knowledge Graph**. Instead of storing text chunks, it stores "Entities" (Nouns) and "Relationships" (Verbs).

**Case Study: GraphRAG for Corporate Audits** In the SBTi Navigator, Vector Search can easily find a paragraph about "Company X's emissions." But what if an auditor asks: *"Which subsidiary of Company X shares a supply chain with Company Y?"* A Knowledge Graph maps this out visually: \[Company X\] -\> (OWNS) -\> \[Subsidiary A\] -\> (BUYS FROM) -\> \[Company Y\] This allows the AI to trace complex corporate logic that standard RAG would completely miss.

**🎓 Professor's Final Note:**

Module 1 sets the absolute foundation for modern AI Engineering. You are learning that building an AI app is **not** about writing a clever prompt. It is about building a robust data pipeline: structuring your knowledge (Vector Search & Graphs), giving it to an autonomous worker (LLM Agents), and proving that it works safely (Synthetic Data Testing).

Study Note: When to Use RAG vs. Knowledge Graphs
================================================

❓ The Critical Question
-----------------------

"In a new project, how do I know if I should use RAG or a Knowledge Graph? Is it just for projects with many PDFs? Give me a simple, new example (not from my previous projects) and tell me how exactly I should command Claude Code to build it."

🛠️ Decision Framework: The "Search vs. Connect" Rule
------------------------------------------------------

You can determine the right architecture by looking at your **Data Volume** and your **Query Type**.

### 1. When to use RAG (Retrieval-Augmented Generation)

-   **Data Profile:** You have a massive library of documents (PDFs, Wikis, Manuals) that exceed the AI's "immediate memory" (context window).

-   **Query Type:** "Needle in a Haystack." You need to find a specific fact or a few relevant pages.

-   **Key Value:** Accuracy, cost-efficiency, and speed.

### 2. When to use Knowledge Graphs (GraphRAG)

-   **Query Type:** "Connecting the Dots." You need to understand relationships between different entities across different files.

-   **Key Value:** Complex logic, tracking "who did what to whom," and multi-step reasoning.

💡 A Simple Example: The "Pet Hospital Archive"
------------------------------------------------

Imagine you are building a system for a large chain of veterinary clinics.

-   **The Data:** 10 years of medical records (50,000+ PDFs) for different pets.

-   **The Problem:** A vet has a Golden Retriever with a rare skin rash. They want to know: *"In the last 5 years, have we treated other Golden Retrievers over 30kg with these exact symptoms? What was the successful treatment plan?"*

-   **Why RAG?**

    1.  **Volume:** You can't feed 50,000 PDFs to Claude; it would be too expensive and slow.

    2.  **Retrieval:** You only need the AI to find the **3 most similar cases** out of the thousands available.

💻 How to Use Claude Code for Implementation
-------------------------------------------

You don't need to be a coding expert; you act as the **Architect**. Here is the exact workflow to use with Claude Code:

### Step 1: Organize your files

Place all your PDFs in a folder (e.g., /medical_records).

### Step 2: The "Architect Command"

Instead of asking for "code," give Claude Code an **Intent-Based Directive**. Type this into your terminal:

*"Claude, I have a library of PDFs in /medical_records. I want to build a RAG pipeline so I can query symptoms and find matching past cases. Use **LangChain** and a local vector store like **ChromaDB**. Use /plan to show me how you will create an ingestion script to 'vectorize' these PDFs and a query script to retrieve them."*

### Step 3: Execution & Testing

1.  **Review the Plan:** Claude will explain how it will "chunk" the text and store the "embeddings."

2.  **Build:** Tell Claude to execute the plan. It will write the Python scripts and install the libraries for you.

3.  **The Test:** Once finished, use the /test command:

> *"Use /test to query the system for 'Golden Retriever skin allergy treatment' and verify that it returns the correct source file names from the /medical_records folder."*

🎓 Summary for your Notes
------------------------

-   **RAG** = The AI "reads" only the relevant pages to save time and money.

-   **Knowledge Graph** = The AI "maps" the relationships to understand complex links.

-   **Claude Code** = Your Senior Engineer who handles the "how" as long as you define the "what."
