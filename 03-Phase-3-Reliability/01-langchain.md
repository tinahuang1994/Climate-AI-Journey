# LangChain: Chat with Your Data

*Created: March 2026 | Source: [DeepLearning.AI — LangChain: Chat with Your Data](https://learn.deeplearning.ai/courses/langchain-chat-with-your-data/)*

Welcome to your official course summary and study guide.

As an AI educator, I have designed this guide specifically for someone who is new to the mechanics of AI but eager to understand the technical architecture behind it. To make these abstract concepts concrete, we will run the entire guide through the lens of your real-world project: **The Science Based Target (SBTi) Navigator**.

**🌟 Introduction: What is the SBTi Navigator?**

Before we dive into the code, let's define the tool we are building.

The **SBTi Navigator** is an AI-powered climate auditing assistant. Corporate sustainability reports are often hundreds of pages long, filled with complex math, emission tables (Scope 1, 2, and 3), and dense text. The Science Based Targets initiative (SBTi) also has its own massive, strict rulebooks.

The goal of the SBTi Navigator is to ingest these massive documents, cross-reference a company's reported emissions against strict SBTi regulations, and allow a human auditor to "chat" with the data to verify compliance and spot "greenwashing."

To build this, you need a technique called **RAG (Retrieval-Augmented Generation)**. This course taught you exactly how to build a RAG pipeline using **LangChain**.

**🧠 Core Concept: The "Open Book Exam"**

Standard AI models (like ChatGPT) take a "closed-book exam." They answer questions based only on what they memorized during their training years ago.

**RAG** turns this into an "open-book exam." LangChain provides the plumbing to let the AI search your private, up-to-date documents (your "book"), read the relevant paragraphs, and formulate an accurate answer.

Here are the 5 steps to building this, applied to the SBTi Navigator.

**Step 1: Document Loading (The Intake)**

**The Concept:** AI models can't naturally read PDFs, Notion pages, or website URLs. You need to extract the raw text from these files first. LangChain provides over 80 "Loaders" to do this.

**SBTi Application:** You receive a 300-page PDF of a company's Annual ESG (Environmental, Social, and Governance) Report.

-   **The Technical Move:** You use LangChain's PyPDFLoader. This tool cracks open the PDF, extracts the text page by page, and attaches "metadata" (e.g., "This text came from page 42"). This metadata is crucial so that when the Navigator later flags an anomaly, it can cite the exact page for the human auditor.

**Step 2: Document Splitting (The Chunking)**

**The Concept:** AI models have a "Context Window"---a limit on how many words they can process at once. You cannot shove a 300-page book into the AI in one go. You must cut the book into smaller paragraphs, or "chunks."

**SBTi Application:** This is the most dangerous step for climate data. If you split the document blindly, you might cut a "Scope 3 Supply Chain" data table in half, separating the emission numbers from their headers. The AI would become hopelessly confused.

-   **The Technical Move:** You use a RecursiveCharacterTextSplitter. Instead of just chopping text every 1,000 words, it looks for natural breaks (like double line breaks or new paragraphs). Crucially, you set a **"Chunk Overlap."** This ensures that chunk \#2 repeats the last 100 words of chunk \#1, preserving the flow of complex SBTi regulatory clauses.

**Step 3: Vector Stores and Embeddings (The Math Translation)**

**The Concept:** How does an AI know which chunk of text to read when you ask a question? Keyword matching (like Ctrl+F) is too dumb. Instead, we use **Embeddings**---a way of translating human text into a list of numbers (vectors) that represent the *meaning* of the text.

**SBTi Application:** An auditor asks the Navigator: *"What is the company's carbon footprint?"* The ESG report might never use the word "footprint"; it might use the phrase *"Greenhouse Gas (GHG) Inventory."*

-   **The Technical Move:** Because "carbon footprint" and "GHG inventory" share the same mathematical "meaning" in an embedding model, the AI knows they are related. You store all these number-translated chunks in a **Vector Store** (like Chroma or FAISS), which acts as a highly efficient, mathematically searchable library.

**Step 4: Retrieval (Finding the Needle)**

**The Concept:** When the user asks a question, the system translates the question into numbers, searches the Vector Store for the closest matching chunks, and retrieves them.

**SBTi Application:** Sometimes, mathematical closeness isn't enough. If an auditor asks, *"Summarize the company's Scope 1 and Scope 2 targets,"* a basic search might bring back 5 chunks that *only* talk about Scope 1 because those were mathematically "closest" to the prompt.

-   **The Technical Move:** You use **MMR (Maximum Marginal Relevance)**. MMR tells the LangChain retriever: *"Find me the most relevant information, but make sure the results are DIVERSE."* This forces the AI to grab chunks about Scope 1 *and* chunks about Scope 2, giving the auditor the complete picture.

**Step 5: Question Answering & Memory (The Auditor Chat)**

**The Concept:** Finally, you take the question, package it together with the retrieved chunks of text, and hand it to the LLM (like Claude or GPT-4) to write a human-readable answer. To make it a true "chat," you also need to pass the "Chat History" back and forth so the AI remembers what you just talked about.

**SBTi Application:** The human auditor is doing a deep-dive investigation.

-   **Auditor:** *"What is the baseline year for their Scope 3 emissions?"* \* **AI:** *"The baseline year is 2021."*

-   **Auditor:** *"Is **that** compliant with the latest standard?"*

-   **The Technical Move:** Using LangChain's ConversationalRetrievalChain, the system injects the chat history into the memory. The AI knows that the word **"that"** refers to *"the 2021 baseline year for Scope 3 emissions."* It grabs the SBTi rulebook chunk for baselines, compares it, and outputs a highly accurate, context-aware verification.

**Q: teach me how to use Langchain in Claude Code**

**A:** As your AI Professor, I am thrilled we are moving from theory into execution. It is completely normal to feel a gap between watching a course video and actually making the code work on your machine.

To bridge this gap, we need to correct a slight conceptual misunderstanding: **You do not use LangChain *inside* Claude Code.** Instead, **Claude Code is your Junior Developer**, and you are going to command it to write, test, and run LangChain Python scripts inside your computer's terminal.

Here is your step-by-step practical guide on how to command Claude Code to build the first piece of your **SBTi Navigator**.

**Step 1: Prepare the Environment**

Before you write any code, you need to prepare your workspace. Open your terminal, navigate to your project folder, and start claude-code.

Instead of typing terminal commands yourself, ask Claude Code to set the stage:

**Prompt to Claude Code:** *"I am building the SBTi Navigator. Please set up a Python virtual environment, activate it, and install the core LangChain libraries we need: langchain, langchain-openai, pypdf, and python-dotenv."*

Claude Code will literally run the pip install commands for you and report back when it is done.

**Step 2: Secure Your API Keys**

Remember your question about "opening" an API key? Now we put that into practice. You need a secure .env file so LangChain can talk to the LLM.

**Prompt to Claude Code:** *"Create a .env file in the root directory. Add a placeholder for OPENAI_API_KEY and ANTHROPIC_API_KEY. Also, make sure to create a .gitignore file so I don't accidentally upload my keys to GitHub."*

*(Note: After Claude Code does this, you must manually open the .env file and paste your actual, real API keys. Never give your raw API keys to Claude Code in the chat).*

**Step 3: Write the "Document Splitter" Script**

Now we apply the exact lesson you just learned from DeepLearning.AI. We will tell Claude Code to write a script that loads an SBTi manual and chunks it intelligently.

Create a folder named docs and drop a sample PDF in it (e.g., sbti-manual.pdf). Then, give Claude Code this exact instruction:

**Prompt to Claude Code:** *"Write a Python script named ingest.py. I want this script to use LangChain's PyPDFLoader to load a PDF from the /docs folder. Then, use the RecursiveCharacterTextSplitter to chunk the document. Set the chunk size to 1000 and the overlap to 200. Finally, print the first two chunks to the terminal so I can verify it worked."*

**Step 4: The Sovereign Workflow (Execution & Auto-Debugging)**

This is where Claude Code shines. Once the script is written, you don't need to leave the terminal.

**Prompt to Claude Code:** *"Run ingest.py and tell me what the output is."*

**The Magic:** If the script fails (for example, if a LangChain update changed how PyPDFLoader is imported), Claude Code will read the red error text in your terminal, apologize, rewrite the code to fix the bug, and run it again automatically. You are acting as the Manager; Claude Code is the Worker.

**Professor's Engineering Challenge**

You now have the exact workflow to start building. To make sure you master this, here is your homework for today:

**Would you like me to draft a CLAUDE.md rulebook for your SBTi Navigator project folder, so that every time you open Claude Code, it automatically knows you are using LangChain for climate auditing and follows strict data-splitting rules?**

**Q: Whenever I work with large documents, do I always have to use LangChain to split the text so the analysis based on my text is better? Is that the right logic and understanding?**

**Gemini said**

That is a fantastic and very "2026" question. The short answer is: **No, you don't always have to split text anymore, but you usually *should* for a professional tool like the SBTi Navigator.**

We are currently in a transition period in AI history. In 2023, splitting was mandatory because AI "memory" (the Context Window) was tiny. In 2026, models like **Gemini 1.5 Pro** and **Claude 3.5/4** have massive "Long Context Windows" that can read 1--2 million tokens (roughly 1,500 pages) in one go.

Here is the breakdown of when to use the "LangChain Splitting" method vs. the "Just Feed it the Whole PDF" method.

**1. The "Long Context" Method (Feeding the whole PDF)**

**The Logic:** "If it fits, it sits." If your document is under 500 pages, modern models can technically read the whole thing at once.

-   **Pros:** \* **Holistic Understanding:** The AI sees the entire document structure. It won't miss a connection between a footnote on page 2 and a table on page 200.

    -   **Simple Code:** You don't need a vector database or complex splitting logic.

-   **Cons:**

    -   **Cost:** You pay for every single word in that 500-page document *every time* you ask a question. This gets expensive fast.

    -   **Latency:** It takes much longer (sometimes 30--60 seconds) for the AI to "read" the whole book before answering.

    -   **"Lost in the Middle":** Even the best AI models still struggle with accuracy when the answer is buried in the middle of a massive 1-million-token prompt.

**2. The "LangChain Splitting" Method (RAG)**

**The Logic:** "Find the needle, then show it to the AI." This is what you learned in your course.

-   **Pros:**

    -   **Speed:** The AI only reads the 3--4 most relevant paragraphs. Answers come back in 1--2 seconds.

    -   **Cost-Efficient:** You only pay for a few hundred tokens per query, not a few hundred thousand.

    -   **Traceability:** It is much easier to show the auditor exactly which "chunk" of text the AI used to make a decision.

-   **Cons:**

    -   **Context Loss:** If your "splitter" is bad, you might cut a sentence in half, making the data useless.

    -   **Setup Heavy:** Requires managing embeddings and a vector store.

**Which is right for the SBTi Navigator?**

For the **SBTi Navigator**, I recommend a **Hybrid Approach**. Here is how a "World Class AI Engineer" would build it today:

  Task                            Method                Why?
  ------------------------------- --------------------- --------------------------------------------------------------------------------------------------------------------------------------------
  **Initial Audit / Summary**     **Long Context**      You want the AI to see the *whole* report once to identify overall themes and find where the major tables are.
  **Specific Compliance Check**   **LangChain / RAG**   When checking a specific rule (e.g., "Is the Scope 3 methodology valid?"), you want high-speed, low-cost retrieval of just that section.
  **Cross-Referencing**           **Knowledge Graph**   (Your future Step 8) To link a company's target to an SBTi regulation, you need a structured "map" that splitting alone can't provide.

**The Verdict**

Your understanding is **mostly right**---splitting usually makes the analysis better because it forces the AI to focus on the "Relevant Truth" rather than getting distracted by 300 pages of marketing fluff in a corporate report.

However, you should no longer see splitting as a *limitation* of the AI, but rather as a **filter** you use to save money, increase speed, and provide audit-grade citations.
