# Prompt Engineering Masterclass: Advanced Logic & Persona Patterns

*Created: March 2026 | Source: Vanderbilt University — Prompt Engineering for ChatGPT (Coursera)*

> **Case Study:** Planning the Ultimate 10-Day Trip to Italy

---

## Phase 1: Defining the "Brain" (Context Patterns)

*These patterns tell the AI who it should be and who it is talking to.*

### 1. The Persona Pattern
- **Prompt:** "Act as a luxury travel concierge who specializes in 'Slow Food' and authentic Italian experiences. You prioritize hidden gems over tourist traps."
- **Why it works:** It forces the AI to use a specific "expert" subset of its knowledge.

### 2. The Audience Persona Pattern
- **Prompt:** "Explain how the Italian train system works, but assume I am a first-time traveler who is nervous about navigating foreign stations."
- **Why it works:** It ensures the explanation is supportive and simple, rather than overly technical.

---

## Phase 2: The Interactive Interview (Interaction Patterns)

*These patterns make the AI do the heavy lifting of gathering requirements.*

### 3. The Flipped Interaction Pattern *(The "Pro" Choice)*
- **Prompt:** "I want to plan a trip to Italy. Do not give me an itinerary yet. Instead, ask me 5 questions about my budget, interests, and pace. Ask them one by one. Once I answer all five, then build the trip."
- **Why it works:** You don't have to guess what info the AI needs; it tells you.

### 4. The Question Refinement Pattern
- **Prompt:** "Whenever I ask a question about where to go in Italy, suggest a better version of my question that would help me find more authentic, less crowded spots."
- **Why it works:** It helps you learn to ask better questions as you go.

### 5. The Cognitive Verifier Pattern
- **Prompt:** "When I ask for a 3-city route, first ask me about my tolerance for long travel days and my interest in art vs. nature. Use my answers to pick the cities."
- **Why it works:** It guarantees the AI considers your personal "logic" before giving advice.

---

## Phase 3: Shaping the Results (Structure Patterns)

*These patterns control how the information looks and is organized.*

### 6. The Few-Shot Pattern
- **Prompt:** "I want my schedule to look like this: [Morning: Espresso at the Piazza | Afternoon: Museum Tour]. Now, use this format to plan a day in Florence."
- **Why it works:** AI is a master mimic. Giving it one example is worth a thousand instructions.

### 7. The Template Pattern
- **Prompt:** "Create a city summary for Rome, Florence, and Venice. Use this template: City: \<NAME\>, Top Dish: \<FOOD\>, Vibe: \<1-WORD DESCRIPTION\>."
- **Why it works:** It creates a clean, uniform list that is easy to read.

### 8. The Recipe Pattern
- **Prompt:** "I have $2,000 and 7 days. Provide a step-by-step 'recipe' (sequence of actions) for how to book the most efficient trip starting from Rome."
- **Why it works:** It provides a logical order of operations to reach a goal.

---

## Phase 4: Creating Tools (Advanced Logic Patterns)

*These patterns turn the chat into a custom-built travel application.*

### 9. The Meta Language Creation Pattern
- **Prompt:** "From now on, when I type 'PriceCheck', tell me the average cost of a meal in the city we are discussing. When I type 'NextStop', suggest the next logical city to visit."
- **Why it works:** It creates your own shorthand commands for the conversation.

### 10. The Menu Actions Pattern
- **Prompt:** "After every city suggestion, provide a menu: 1. See Hotels, 2. See Museums, 3. Change City."
- **Why it works:** It makes the AI feel like a clickable app.

### 11. The Semantic Filter Pattern
- **Prompt:** "Show me 10 things to do in Venice, but filter out anything that is considered a 'tourist trap' or costs more than 50 Euros."
- **Why it works:** It automatically removes irrelevant data based on meaning.

### 12. The Fact-Check List Pattern
- **Prompt:** "At the end of the itinerary, list every opening time you mentioned and provide a warning if that info might be outdated."
- **Why it works:** It adds a layer of safety and verification to the AI's suggestions.

---

## Summary

If you want to get the most out of AI, remember: **it is a brilliant but literal intern.**

| Pattern | What it does |
|---------|-------------|
| **Persona** | Give it a job title and expertise |
| **Flipped Script** | Let the AI ask *you* the questions |
| **Few-Shot** | Show it one example of what you want |
| **Cognitive Verifier** | Tell it to check its logic before answering |
