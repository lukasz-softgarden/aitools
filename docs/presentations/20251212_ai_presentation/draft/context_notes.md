The successful use of large context windows does not guarantee better performance; in fact, overloading the context can cause AI agents and applications to fail in surprising ways.
Here are the key pitfalls of long context usage:

The Pitfalls of Long Context
1. Context Poisoning (When errors are amplified)
   • Description: Occurs when a hallucination or an error makes it into the context and is then repeatedly referenced by the agent during its operation.
   • Result: The model can become fixated on achieving impossible or irrelevant goals if critical parts of the context (like goals or summaries) are corrupted with misinformation.
   • Example: The Gemini agent playing Pokémon would occasionally hallucinate the game state, poisoning its context and leading it to develop nonsensical strategies.
2. Context Distraction (Overwhelming Model Knowledge)
   • Description: When the context grows too long (accumulating history), the model over-focuses on this history, neglecting the general knowledge it learned during training.
   • Result: Instead of synthesizing novel plans, the agent shows a tendency toward favoring repeating actions from its extensive context history.
   • Example: This behavior was observed when the context grew significantly beyond 100K tokens for one frontier model. For smaller models (Llama 3.1 405b), correctness began to fall around 32K tokens.
3. Context Confusion (Superfluous Noise)
   • Description: When too much superfluous content, such as irrelevant tool definitions or excessive documents, is included, it influences the model to generate a low-quality response. The model must pay attention to everything in the context, even irrelevant noise.
   • Result: Models demonstrate low tool selection accuracy and occasionally call irrelevant tools.
   • Example: The Berkeley Function-Calling Leaderboard shows that every model performs worse when provided with more than one tool. A small model (quantized Llama 3.1 8b) failed a query when given 46 tools but succeeded when the number was reduced to 19, demonstrating that the sheer number of tools caused failure, not the context limit.
4. Context Clash (Internal Contradictions)
   • Description: Occurs when information accumulated in the context (especially during multi-turn reasoning) conflicts with other data already present.
   • Result: Models tend to rely on early, incorrect assumptions and prematurely attempt to generate final solutions, on which they overly rely, making it difficult for them to recover if the context later contradicts those assumptions.
   • Example: Modifying benchmark prompts to be ‘sharded’ (split across multiple conversational turns) caused a dramatic average accuracy drop of 39% because the context retained the model’s early, incorrect attempts to answer before all information was gathered.

--------------------------------------------------------------------------------
Inefficient Token Consumption (Cost and Latency)
A. Overload from Tool Definitions:
• Problem: Loading all tool definitions upfront consumes context space, increasing response time and costs, even if those tools are not needed for the current task.
• Example: A standard five-server setup might consume approximately 55K tokens just for 58 tool definitions before the agent starts any work.
B. Intermediate Results Pollution:
• Problem: When tools are called directly, all intermediate results must pass through the model's context window, even if the model only needs an aggregate or summary.
• Example: If an agent downloads a 2-hour meeting transcript and transfers it to another tool, the full transcript text flows through the context window twice, potentially processing an additional 50,000 tokens unnecessarily. Similarly, fetching a 10,000-row spreadsheet means all rows pollute the context if filtering isn't done externally.

--------------------------------------------------------------------------------
Core Insight: The Quality of Context is Paramount
• The only thing that improves the quality of model outputs (besides temperature or training) is the quality of the context provided.
• The fundamental principle is: The less context (tokens) you use to do the work, the better results you will get.
• The worst thing to have in your context window is bad information. A bad line of research (a fundamental misunderstanding of the system) is the most catastrophic, potentially causing thousands of bad lines of code.
Analogy: Imagine preparing for an exam by bringing every textbook, every rough draft, and every incorrect flashcard you've ever created (long context). You are more likely to get distracted, confuse conflicting facts, or repeat an initial, incorrect assumption (Context Distraction, Confusion, Clash) than if you had carefully filtered and summarized only the accurate, relevant notes (optimized context).