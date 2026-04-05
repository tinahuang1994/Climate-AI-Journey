# Building Customized LLMs with OpenAI — Module 2: Fine-Tuning vs. RAG

*Created: March 2026 | Source: Columbia University — Building Customized LLMs with OpenAI*

## 1. The Big Difference: RAG vs. Fine-Tuning

In Module 1, you learned RAG. RAG is like giving GadgetBot a **Rulebook**. When a customer asks a question, GadgetBot looks at the rulebook, finds the answer, and reads it back. *The AI's brain never changes.*

**Fine-Tuning** (Module 2) is completely different. It is like sending GadgetBot to an **Intensive Training Bootcamp**. We are not giving it a book to read; we are mathematically rewriting its neural pathways (updating its parameters). When it finishes, you essentially have a brand-new, custom-built AI.

**2. How to Fine-Tune GadgetBot (The 5 Steps)**

According to your professor's slides, if you want to fine-tune an AI to become a perfect customer service rep, you must follow the Machine Learning Process:

-   **Step 1: Gather Data.** You don't use PDFs for this. You download 10,000 real, high-quality chat logs between your best human employees and actual customers.

-   **Step 2: Preprocessing.** You "clean" the data. You remove any customer credit card numbers, fix typos, and format it so the AI can read it.

-   **Step 3: Split the Data.** You hide 2,000 of those chats in a locked folder (Testing data). You only use 8,000 to train the AI.

-   **Step 4: Fine-Tune.** You feed the 8,000 chats into the AI, slowly altering its brain so it learns to speak exactly like your best employees.

-   **Step 5: Test.** You bring out the 2,000 hidden chats to test if the AI actually learned the skills, or if it just memorized the first batch.

**3. Supervised Fine-Tuning (SFT)**

This is the most common way to train your chatbot. "Supervised" simply means you are giving the AI the exact **Question** and the exact perfect **Answer**.

You feed the AI thousands of pairs like this:

**Prompt:** "How can I return my LCD TV?" **Response:** "I can help with that! To return your TV, please bring your receipt to the front desk within 30 days."

By seeing this pattern thousands of times, the AI's internal parameters change. It stops sounding like a generic robot (like ChatGPT) and permanently starts sounding like a friendly Gadget Store employee.

**4. The "Cheaper" Alternatives: Prefix & Prompt Tuning**

Full fine-tuning (changing the whole brain) is very expensive and requires massive computers. Your professor introduces two shortcuts that are much cheaper because they only add a tiny mathematical layer *before* the AI's brain.

**A. Prefix Tuning (Setting the Mood)** Instead of changing the AI's brain, you attach a mathematical "Prefix Vector" to the front of the customer's question.

-   **How it works for GadgetBot:** You train a small mathematical vector that essentially screams, *"ACT LIKE A CUSTOMER SERVICE REP!"* \* **The Result:** Every time a customer types a message, this invisible math vector is attached first. It forces the AI into "Customer Service Mode" without needing to rewrite the whole AI.

**B. Prompt Tuning (The Translator)** Customers ask the same question in weird ways.

-   Customer A: *"How do I return my LCD TV?"*

-   Customer B: *"I bought a TV, it's too big for my wall, want my money back, what do I do?"*

-   **How it works for GadgetBot:** Prompt Tuning adds a "Translation Layer" between the customer and the AI. It learns that Customer B's messy rant mathematically means the exact same thing as Customer A's simple question.

-   **The Result:** It invisibly converts the messy question into a standard mathematical embedding, so the AI always knows exactly how to answer.

**Professor's Summary**

-   **Use RAG** when you want the AI to look up facts (like "What is our return policy?").

-   **Use Fine-Tuning** when you want to permanently change the AI's *behavior, tone, and format* (so it naturally speaks like a highly-trained customer service agent).

**Q&A**

**Q: https://nothanks-xi.vercel.app/:Actually, my No Thanks website is also chat based. But I mean I haven't, I mean I don't think I use RAG or supervised fine tuning for it. I think I, I mean maybe it's supervised, because I fed it, I mean I I told it them to generate the response based onThe framework, the Eisenhower Matrix, and how to say no, like How would you think that did I use fine tuning here then?**

A: This is a brilliant question and a very common "aha!" moment for developers who are just starting to look under the hood of AI.

To answer your question directly: **No, you did not use Fine-Tuning, and you did not use RAG.** What you actually used for the *No Thanks* app is called **System Prompting** (or Advanced Prompt Engineering).

Let me explain the difference using the "Employee" analogy we used earlier, so you can see exactly where your app fits into the AI landscape.

**The Three Levels of AI Customization**

Imagine you just hired a very smart, college-educated intern (the base AI, like ChatGPT or Claude).

**1. System Prompting (What you did for "No Thanks")**

-   **The Analogy:** You hand the intern a clipboard and a sticky note at the beginning of their shift that says: *"For the rest of the day, act like a professional career coach. When people complain about being overworked, use the Eisenhower Matrix to help them say no."*

-   **How it works mathematically:** You are just attaching a set of instructions to the front of the user's message. The AI's brain doesn't change permanently. When the user closes the chat, the AI "forgets" the sticky note.

-   **Why it worked perfectly for your app:** The AI *already read* millions of articles about the Eisenhower Matrix during its initial training years ago. You didn't need to teach it what the matrix was; you just needed to **direct** it to use that specific framework.

**2. RAG (Module 1)**

-   **The Analogy:** You give the intern a key to a massive filing cabinet and say, *"Every time someone asks a question, go open the cabinet, find a relevant document, and read from it."*

-   **When you would need it:** If you wanted the *No Thanks* app to reference highly specific, private data. For example, if you wanted the AI to say, *"According to your company's HR handbook on page 4, you are legally allowed to decline weekend work."* The AI doesn't know your specific HR handbook, so it would need RAG to look it up.

**3. Fine-Tuning (Module 2)**

-   **The Analogy:** You send the intern to a 6-month intensive bootcamp to get a degree in Assertiveness Coaching. You literally rewire their brain.

-   **How it works mathematically:** You provide thousands of examples of perfect "No Thanks" conversations (Supervised Fine-Tuning) and permanently change the model's internal weights. You don't need to give it a sticky note anymore; its default state of being is now a career coach.

-   **When you would need it:** If the AI simply couldn't get the "vibe" right using a prompt. If it kept sounding too robotic, and you wanted it to perfectly mimic the exact tone of a specific famous therapist, you would fine-tune it on that therapist's actual transcripts.

**🎓 Professor's Verdict on Your App**

You made the **correct engineering choice** for the *No Thanks* app!

As a software developer, your goal is to use the cheapest, fastest, and simplest tool for the job. Because the Eisenhower Matrix is common knowledge, a well-written System Prompt was all you needed. You don't need the heavy machinery of RAG or Fine-Tuning unless the AI lacks specific knowledge (RAG) or fails to adopt the right behavior (Fine-Tuning).

**Q: Can you tell me when is a good use case to use fine tuning?I guess for example, for a very specific company, when this company wants to build customized AI for this very specific company, you should use fine tuning, is that correct?**

A: This is a fantastic question, and you have just stumbled upon the **\#1 most common misconception** in AI engineering today!

It is a very logical guess, but the short answer is: **No, just because a company wants a "customized AI" does not mean they should use fine-tuning.** In fact, 90% of the time, they should *not* use fine-tuning.

Let me gently correct this and give you the ultimate industry rule of thumb so you know exactly when to use which.

### The Golden Rule of Custom AI

-   **RAG** is for teaching the AI new **Knowledge** (Facts, documents, company secrets).

-   **Fine-Tuning** is for teaching the AI new **Behavior** (Tone, format, style, specific skills).

If a specific company comes to you and says, *"We want a custom AI that knows all our private HR policies, our secret product roadmaps, and our past financial reports,"* you should build them a **RAG system**.

-   **Why?** Because you can just drop all their PDFs into a database. If the company updates its HR policy tomorrow, you just swap out the PDF. If you used fine-tuning for this, you would have to spend thousands of dollars to completely re-train the AI's brain every time a policy changed!

### So, when is a GOOD use case for Fine-Tuning?

You should only use fine-tuning when prompting fails and you need the AI to consistently output a very specific **format, style, or highly specialized skill**. Here are three perfect real-world use cases for a company to use fine-tuning:

#### 1. Mastering a Highly Specific Tone of Voice

Imagine a company like *Duolingo* wants a customer service bot. They don't want it to sound polite and corporate; they want it to sound slightly passive-aggressive, funny, and quirky (like their famous mascot).

-   **Why Fine-Tuning?** It is really hard to write a prompt that says *"Be funny but not offensive, quirky but helpful."* Instead, you use Supervised Fine-Tuning. You feed the AI 10,000 examples of perfect Duolingo tweets and chats. The AI's brain is permanently altered to naturally speak in that exact quirky voice.

#### 2. Specialized Output Formats (e.g., Medical or Legal Tech)

Imagine a hospital needs an AI to read messy doctor's notes and convert them into a very strict, proprietary JSON code format used only by their ancient billing software.

-   **Why Fine-Tuning?** A standard AI will often make formatting mistakes or add extra chatty text like, *"Here is the JSON you requested!"* which breaks the hospital's software. By fine-tuning the model on 5,000 examples of \[Messy Notes\] -\> \[Perfect JSON\], the AI learns to output *only* the exact code format, every single time, with zero extra words.

#### 3. Hyper-Niche Tasks (Where the AI just "doesn't get it")

Let's say a cybersecurity company wants an AI to look at raw, confusing server network logs to detect a very specific, rare type of Russian hacker attack. Standard ChatGPT has no idea what this specific attack looks like.

-   **Why Fine-Tuning?** You can't just put a network log in a prompt and say "find the hacker." You need to fine-tune the AI on thousands of logs labeled *"Normal"* and thousands labeled *"Hacked."* You are training it to develop a new "instinct" or skill.

### Summary for your Notes

If a client asks you to build a custom AI for their company, ask them one question: **"Does the AI need to *know* things it doesn't currently know, or does it need to *act* in a way it currently doesn't act?"**

-   Needs to know company secrets? **Build RAG.**

-   Needs to perfectly mimic the CEO's writing style or output a strict proprietary code? **Fine-Tune.**
