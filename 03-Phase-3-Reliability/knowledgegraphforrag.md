# Knowledge Graphs for RAG

*Created: March 2026 | Source: [DeepLearning.AI — Knowledge Graphs for RAG](https://www.deeplearning.ai/short-courses/knowledge-graphs-rag/)*

Welcome to your official course summary and study guide.

As an AI educator, I have designed this guide to help you transition from simply "searching" for data to actually "understanding" how data connects. We will frame these technical concepts using a real-world project so they are easy to grasp but technically rich.

**🌟 The Case Study: The SBTi Navigator**

Before we get into the tech, let's define the tool we are using as our example.

The **SBTi Navigator** is an AI-powered climate auditing assistant. Corporate sustainability reports are often hundreds of pages long, filled with complex math, parent-subsidiary company relationships, and dense text. The Science Based Targets initiative (SBTi) also has its own massive, strict rulebooks. The goal of the SBTi Navigator is to ingest these massive documents, cross-reference a company's reported emissions against strict SBTi regulations, and allow a human auditor to "chat" with the data to verify compliance and spot "greenwashing."

**❓ The Big Questions: Why Knowledge Graphs?**

**1. Why is it important to use Knowledge Graphs?** In your previous LangChain course, you learned standard RAG (Retrieval-Augmented Generation). Standard RAG uses **Vector Search**. Think of Vector Search like a very smart librarian: you ask for "Scope 3 emissions," and the librarian runs to the shelf, grabs the 5 pages that talk about Scope 3, and hands them to the AI. But what if you ask a complex question: *"Which subsidiary of Acme Corp had the highest Scope 3 emissions last year, and are they compliant with SBTi Rule 4.2?"* Standard RAG fails here. It might find the page about "Acme Corp," the page about "Scope 3," and the page about "Rule 4.2," but it cannot connect the dots. A **Knowledge Graph** acts like a detective's evidence board, using string to physically connect Acme Corp to its subsidiary, the subsidiary to its emissions, and the emissions to the rule.

**2. Will AI technology just "catch up" so we don't need Knowledge Graphs?** This is a common debate. AI models now have massive "Long Context Windows" (they can read 10,000 pages at once). So, won't they eventually just figure out the connections on their own? **No. We cannot wait for technology to catch up, because Large Language Models (LLMs) and Knowledge Graphs do fundamentally different things.**

-   **LLMs are Probability Engines:** They guess the next most likely word. Even with a massive memory, they can get confused by dense, overlapping financial or climate logic ("hallucinations").

-   **Knowledge Graphs are Truth Engines:** They are mathematical databases of absolute facts. For a high-stakes tool like the SBTi Navigator, you cannot rely on "probability" to audit a company's climate goals. You need the deterministic, hard-coded logic of a Knowledge Graph to prove that the data is accurate.

**🧠 Module 1: The Anatomy of a Knowledge Graph**

A Knowledge Graph (KG) moves us away from storing data in messy paragraphs and instead stores data in a structured network. It consists of two main parts:

-   **Nodes (The "Nouns"):** These are the specific entities in your documents.

    -   *SBTi Example:* "Acme Corp" (Company), "Scope 3" (Emission Category), "2025" (Year).

-   **Edges / Relationships (The "Verbs"):** These are the directional lines connecting the Nodes.

    -   *SBTi Example:* "OWNS" (Acme Corp -\> Subsidiary), "EMITS" (Subsidiary -\> Scope 3), "TARGETS" (Scope 3 -\> 2025).

**The Result:** Instead of the AI reading a paragraph that says *"Acme Corp owns GlobalTech, which emitted 500 tons of Scope 3,"* the AI queries a mathematical map: (Acme Corp) -\[OWNS\]-\> (GlobalTech) -\[EMITS\]-\> (500 Tons).

**🏗️ Module 2: Building the Graph (Entity Extraction)**

How do we turn a 300-page PDF into this neat web of Nodes and Edges? We use the AI itself to build the graph.

**The Concept:** You pass chunks of text to an LLM and use a strict prompt to force it to act as an "Information Extractor." **The Technical Move:** In the course, you learned to prompt the AI to extract a JSON list of entities and relationships.

-   *Text:* "GreenTech's subsidiary, EcoParts, failed to meet the 2024 SBTi standard."

-   *AI Extraction:* \* Node 1: GreenTech (Company)

    -   Node 2: EcoParts (Subsidiary)

    -   Node 3: 2024 SBTi standard (Regulation)

    -   Relationship: GreenTech -\[OWNS\]-\> EcoParts

    -   Relationship: EcoParts -\[FAILED_COMPLIANCE\]-\> 2024 SBTi standard

**🗣️ Module 3: Querying the Graph (Enter Cypher)**

Once your graph is built in a database (like **Neo4j**, the tool used in this course), how do you get answers out of it? You use a specialized query language called **Cypher**.

**The Concept:** Cypher is the "SQL of Graphs." It is a visual coding language designed to trace the paths between nodes. It uses parentheses () for Nodes and arrows -\> for relationships.

**SBTi Application:** Imagine an auditor wants to find all companies failing a specific rule.

-   **Cypher Code:** MATCH (c:Company)-\[:REPORTS\]-\>(e:Emissions)-\[:VIOLATES\]-\>(r:Rule {name: "SBTi 4.2"}) RETURN c.name

-   **Translation:** "Find me any Company that reported Emissions which violate Rule 4.2, and give me the Company's name." Because this is a database query, it is 100% accurate. There are no AI hallucinations here.

**🤝 Module 4: GraphRAG (The Ultimate Combo)**

The climax of the course is **GraphRAG**---combining standard Vector RAG with a Knowledge Graph.

**The Concept:** Text Embeddings (Vectors) are great at understanding concepts and synonyms. Graphs are great at logic and connections. By combining them, you get the ultimate AI brain.

**The SBTi Workflow:**

1.  **The Auditor Asks:** *"How does Acme Corp's supply chain carbon footprint compare to the latest global warming guidelines?"*

2.  **Vector Search Kicks In:** The system uses Vector Search to realize that "supply chain carbon footprint" means "Scope 3 Emissions," and "guidelines" means "SBTi Sectoral Decarbonization Approach."

3.  **Graph Search Kicks In:** The system takes those concepts and traverses the Knowledge Graph. It starts at "Acme Corp," jumps to its 50 "Suppliers," grabs their "Scope 3" nodes, and checks the connections to the "SBTi Guidelines."

4.  **The Generation:** The LLM reads the perfect, logically sound data pulled from the Graph and writes a beautifully formatted, highly accurate audit report for the user.

**🎓 Course Conclusion**

By finishing this course, you have learned how to give your AI a **Structured Brain**. While standard Vibe Coding and prompting are great for creative tasks, tools like the **SBTi Navigator** require an "Audit-Grade" foundation. Knowledge Graphs provide the mathematical "Safety Net" that ensures your AI's conclusions are not just well-written, but provably, factually true.

When I'm building SBTi Navigator, how can I apply knowledge graphs in Claude Code?

As your AI Professor, I love this question because it represents the exact moment you transition from "learning concepts" to "building systems."

To apply Knowledge Graphs using **Claude Code**, we need to revisit our mental model: **Claude Code does not "hold" the Knowledge Graph inside itself.** Instead, Claude Code is your Junior Developer. You will command it to write the Python scripts that extract data from your PDFs and push that data into a graph database (like **Neo4j**, which you used in your course).

Here is the exact step-by-step playbook to command Claude Code to build the "Brain" of your SBTi Navigator.

### Phase 1: The Infrastructure Setup

First, you need a place for your graph to live. I recommend setting up a free **Neo4j AuraDB** cloud instance (or a local Neo4j desktop database). Once you have your connection URI, Username, and Password, open your terminal with Claude Code.

**1. Secure the Credentials:**

**Prompt to Claude Code:** *"I am adding a Neo4j Knowledge Graph to the SBTi Navigator. Please update my .env file to include placeholders for NEO4J_URI, NEO4J_USERNAME, and NEO4J_PASSWORD."* *(Remember to paste your actual credentials in manually afterward!)*

**2. Install the Graph Tools:**

**Prompt to Claude Code:** *"Please install the necessary Python libraries for this phase: neo4j, langchain-community, and langchain-openai."*

### Phase 2: Define the "SBTi Graph Schema"

If you tell Claude Code to "extract entities," it will guess what to look for, resulting in a messy graph. You must give it a strict architectural blueprint.

Create a file named GRAPH_SCHEMA.md in your project folder. This is your "rulebook" for Claude Code. Include rules like:

-   **Allowed Nodes:** Company, Subsidiary, EmissionCategory (e.g., Scope 3), TargetYear, Regulation (e.g., SBTi 4.2).

-   **Allowed Relationships:** OWNS (Company -\> Subsidiary), REPORTED_EMISSIONS (Subsidiary -\> EmissionCategory), MUST_COMPLY_WITH (EmissionCategory -\> Regulation).

### Phase 3: Building the "Extractor" Script

Now, command Claude Code to write the script that actually reads the PDFs and builds the graph. In your recent course, you learned that LLMs can extract entities automatically.

**Prompt to Claude Code:** *"Read the rules in \@GRAPH_SCHEMA.md. Write a Python script named build_graph.py. I want this script to use LangChain's LLMGraphTransformer to process chunks of text from our /docs folder. It should strictly extract only the Nodes and Relationships defined in the schema and push them to my Neo4j database."*

If Claude Code runs into an error connecting to the database or formatting the extraction, let it auto-debug! That is the power of agentic engineering.

### Phase 4: Building the "Auditor Chat" (GraphRAG)

Once the graph is populated with data from your corporate reports, it is time to build the interface for the human auditor.

Instead of searching for text chunks, we want the AI to write **Cypher queries** to trace the exact logic of the emissions.

**Prompt to Claude Code:** *"Write a script named audit_chat.py. Use LangChain's GraphCypherQAChain. The script should take a user's question (like 'Which subsidiaries failed Scope 3 compliance?'), translate it into a Cypher query, run it against the Neo4j database, and return a natural language answer."*

### Professor's "Pro-Tip" for Claude Code

When working with Knowledge Graphs, the most common error is "Schema Drift" (where the AI starts inventing new node types like CarbonFootprint instead of sticking to EmissionCategory).

To prevent this, use your Claude Code /test skill. After Claude Code writes the extraction script, command it:

*"Run build_graph.py on a sample PDF. Then, write a test to query the database and verify that absolutely NO nodes exist outside of the 5 allowed in our \@GRAPH_SCHEMA.md."*
