# Coding with AI

**Context**
In 11/08/25 (4 months ago) I gave internal talk in Softgarden titled "AI tips & tricks".
This presentations is followup for brother audience ~150 people.
I want to start from quick reminder what was covered during my 1st presentation.
Then I want to explain what has changed since then.
After that there is going to be demo section.
At the end I plan to show bonus - coding from mobile (claude code).

**Resources**

This is list of resources my presentation was referring to:
- [Spec Driven Development — Sean Grove, OpenAI](https://youtu.be/8rABwKRsec4?si=py8nVArZYMz6YoNA)
- [Code execution with MCP: Building more efficient agents](https://www.anthropic.com/engineering/code-execution-with-mcp)
- [12-Factor Agents: Patterns of reliable LLM applications — Dex Horthy, HumanLayer](https://www.youtube.com/watch?v=8kMaTybvDUw&t=36s)
- [Advanced Context Engineering for Agents](https://www.youtube.com/watch?v=IS_y40zY-hc)
- [AGENTS.md](https://agents.md/)
- [GitHub Spec Kit](https://github.com/github/spec-kit)
- [GitHub Copilot context engineering flow](https://code.visualstudio.com/docs/copilot/guides/context-engineering-guide)
- [GitHub Copilot - new embedding model](https://github.blog/news-insights/product-news/copilot-new-embedding-model-vs-code/)
- [How Long Contexts Fail](https://www.dbreunig.com/2025/06/22/how-contexts-fail-and-how-to-fix-them.html)
- [Copilot coding agent now supports AGENTS.md custom instructions](https://github.blog/changelog/2025-08-28-copilot-coding-agent-now-supports-agents-md-custom-instructions/)
- [GitHub Copilot - custom instructions](https://docs.github.com/en/copilot/how-tos/configure-custom-instructions)

## Slides

In this section there are listed slides that I want to have in my presentation.
Special blocks:
- `<infographic>description</infographic>` - in this place infographic has to be displayed
- `<positon_def></positon_def>` - defines where to present content, example `<bottom_right>some text</bottom_right>`

### Slide 1. Title: "Coding with AI: From Vibe-Coding to Conscious Design of Specifications and Context"

<infographic>Thematic graphic</infographic>
<bottom_right>
    Date: 28/11/2025
    Author: Łukasz Wojtaszek
</bottom_right>

### Slide 2. Title: "From the previous presentation"

<left>
LLMs are stateless (pure functions) - Each query is independent. The context from previous interactions must be explicitly provided each time.
Context Window - There is a limit to the amount of text (tokens) that the model can process in a single query.
</left>

<right>
Knowledge Cutoff - The models do not know events or data that appeared after the date of completion of their training.
Hallucinations - Models can generate false, but credible-sounding information, e.g., by inventing non-existent API functions.
</right>

### Slide 3. Title: "From the previous presentation"

<infographic>
Requirements -> jira-task.md -> Research & Plan -> plan.md -> Implementation -> Generated code -> Review & fixes -> Pull request
</infographic>

### Slide 4. Title: "AI tools evolution"

<left>
**What's changed?**
- Popularization of CLI agents: Claude Code, Cursor CLI, OpenAI Codex, Gemini CLI, Copilot CLI, Droid, OpenCode, etc.
- AGENTS.md standard was introduced by OpenAI (.github/copilot-instructions.md -> AGENTS.md)
- Github Copilot changes: Native `Plan` mode, Custom chat modes -> Custom agents, New embedding model
</left>

<right>
[copilot_new_embedding_model](sources/copilot_new_embedding_model.png)
</right>

### Slide 5. Title: "Spec Driven Development - Your Intent is the New Source Code"

<left>
- "When we prompt LLMs, we keep the generated code and we delete the prompt. This feels like you shred the source and then you very carefully version control the binary." - Sean Grove, OpenAl
- We must stop throwing away our prompts and plans. The specification is the most valuable artifact. It is the executable description of our intent.
</left>

<right>
<infographic>
/specify (Define intent) -> /plan (Plan implementation) -> /implement (Execute plan)
</infographic>
</right>

### Slide 6. Title: "Context is everything"

<top>
LLMs are stateless (pure functions). _The only thing other than training your model or playing with temperature that improves the quality of LLM output is quality of input._ ~Dexter Horthy
</top>

<bottom>
<infographic>Tokens in -> LLM -> Tokens out</infographic>
</bottom>

src: [Advanced Context Engineering for Agents](https://www.youtube.com/watch?v=IS_y40zY-hc)

### Slide 7. Title: "Understanding the Context Window"

[Context visualisation](sources/context_visualisation.png)

### Slide 8. Title: "Understanding the Context Window"

[Intentional compaction](sources/intentional_compaction.png)

src: [Advanced Context Engineering for Agents](https://www.youtube.com/watch?v=IS_y40zY-hc)

### Slide 9. Title: "The pitfalls of long context"

Longer context windows do not automatically generate better responses. They introduce new, surprising failure modes.

<infographic>
Poisoning
Confusion
Distraction
Clash
</infographic>

### Slide 10. Title: "Advices"

1. Research & plan -> plan.md -> Clean context -> Execute plan (implementation) -> Clean context -> Read plan & execute review
2. Be precise: do not overload context with not relevant files and instructions
3. Experiment with the models, you can use different models for Planning, Implementation, Review
4. Do not use MCPs if you don't have to
5. Keep AGENTS.md (project instructions) simple
6. Use personal instructions to personalize agent behaviour. Example: `Always use "lwojtaszek" as author in liquibase scripts`
7. Explain repeatable tasks as custom prompts/instructions

### Slide 11. Title: "Demo"

<centered>
Demo
</centered>

### Slide 12. Title: "Bonus"

Screenshot

### Slide 13

<centered>
Thank you
</centered>
