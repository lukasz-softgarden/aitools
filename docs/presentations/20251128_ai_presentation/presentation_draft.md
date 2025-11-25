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
- [Introducing advanced tool use on the Claude Developer Platform](https://www.anthropic.com/engineering/advanced-tool-use)

## Slides

In this section there are listed slides that I want to have in my presentation.
Special blocks:
- `<infographic>description</infographic>` - in this place infographic has to be displayed
- `<positon_def></positon_def>` - defines where to present content, example `<bottom_right>some text</bottom_right>`

### Slide 1. Title: "Coding with AI: From Vibe-Coding to Conscious Design of Specifications and Context"

<infographic>Thematic graphic</infographic>
<bottom_right>
    Date: 12/12/2025
    Author: Łukasz Wojtaszek
</bottom_right>

### Slide 2. Title: "From the previous presentation"

**LLM Basics**

<grid_4_cols>
LLMs are stateless - Each query is independent. The context from previous interactions must be explicitly provided each time.
Knowledge Cutoff - The models do not know events or data that appeared after the date of completion of their training.
Context Window - There is a limit to the amount of text (tokens) that the model can process in a single query.
Hallucinations - Models can generate false, but credible-sounding information, e.g., by inventing non-existent API functions.
</grid_4_cols>

**Coding with AI Workflow**

<infographic>
Requirements (jira-task.md) -> Plan (plan.md) -> Implementation (code) -> Review (review.md) -> Apply (code) -> PR
</infographic>

### Slide 3. Title: "AI tools evolution"

<left>
**What's changed?**
- Popularization of CLI agents: Claude Code, Cursor CLI, OpenAI Codex, Gemini CLI, Copilot CLI, Droid, OpenCode, etc.
- AGENTS.md standard was introduced by OpenAI (.github/copilot-instructions.md -> AGENTS.md)
- Anthropic open-sourced [Sandbox Runtime (srt)](https://github.com/anthropic-experimental/sandbox-runtime) - available in CC via `/sandbox`
- Github Copilot changes: Native `Plan` mode, Custom chat modes -> Custom agents, New embedding model
</left>

<right>
[copilot_new_embedding_model](sources/copilot_new_embedding_model.png)
</right>

### Slide 4. Title: "Spec Driven Development - Your Intent is the New Source Code"

> "When we prompt LLMs, we keep the generated code and we delete the prompt. This feels like you shred the source and then you very carefully version control the binary." - Sean Grove, OpenAI

We must stop throwing away our prompts and plans. The specification is the most valuable artifact. It is the executable description of our intent.

**GitHub Spec Kit**

Spec-Driven Development flips the script on traditional software development. For decades, code has been king — specifications were just scaffolding we built and discarded once the "real work" of coding began. Spec-Driven Development changes this: specifications become executable, directly generating working implementations rather than just guiding them.

<infographic>
/constitution (Project principles) -> /specify (Define requirements) -> /plan (Technical design) -> /tasks (Generate task list) -> /implement (Execute tasks)
</infographic>

### Slide 5. Title: "Context is everything"

> "The only thing other than training your model or playing with temperature that improves the quality of LLM output is quality of input." — Dexter Horthy

- **Less is more**: The less context (tokens) you use to do the work, the better results you will get
- **Bad info is catastrophic**: A bad line of research (fundamental misunderstanding of the system) can cause thousands of bad lines of code

<infographic>Tokens in -> LLM -> Tokens out</infographic>

src: [Advanced Context Engineering for Agents](https://www.youtube.com/watch?v=IS_y40zY-hc)

### Slide 6. Title: "Understanding the Context Window"

[Context visualisation](sources/context_visualisation.png)

### Slide 7. Title: "Understanding the Context Window"

[Intentional compaction](sources/intentional_compaction.png)

src: [Advanced Context Engineering for Agents](https://www.youtube.com/watch?v=IS_y40zY-hc)

### Slide 8. Title: "The pitfalls of long context"

Longer context windows do not automatically generate better responses. They introduce new, surprising failure modes.

<grid_2x2>
**Poisoning** - Hallucination enters context and is repeatedly referenced, leading to nonsensical strategies (e.g. Gemini Pokémon agent).
**Distraction** - Model over-focuses on long history, neglecting training knowledge. Issues start ~100K tokens (frontier) or ~32K (smaller models).
**Clash** - Conflicting info in multi-turn reasoning. Model relies on early incorrect assumptions — 39% accuracy drop on sharded prompts.
**Confusion** - Irrelevant tools/docs cause wrong tool selection. Model failed with 46 tools but succeeded with 19.
</grid_2x2>

Reference: Anthropic's tool search approach - Direct tool calls vs Tool search + programmatic calling

src: [How Long Contexts Fail](https://www.dbreunig.com/2025/06/22/how-contexts-fail-and-how-to-fix-them.html)

### Slide 9. Title: "Best Practices"

**Keep Context Clean**
- Clear context between phases (Requirements → Plan → Implementation)
- Be precise with files & instructions
- Avoid unnecessary MCPs

**Optimize Your Setup**
- Keep AGENTS.md simple
- Use personal instructions (e.g. `Always use "lwojtaszek" as author in liquibase migrations`)
- Define custom prompts for repeatable tasks

**Experiment**
- Different models for different phases (Plan vs Implement vs Review)

### Slide 10. Title: "Demo"

<centered>
Demo
</centered>

### Slide 11. Title: "Bonus"

Mobile Coding - Claude Code on mobile

[Add screenshot here]

### Slide 12. Title: "Sources"

**Context Engineering & Agent Design**
- [Advanced Context Engineering for Agents](https://www.youtube.com/watch?v=IS_y40zY-hc)
- [How Long Contexts Fail](https://www.dbreunig.com/2025/06/22/how-contexts-fail-and-how-to-fix-them.html)
- [12-Factor Agents — Dex Horthy](https://www.youtube.com/watch?v=8kMaTybvDUw&t=36s)

**Anthropic / Claude**
- [Building effective agents](https://youtu.be/2MJDdzSXL74?si=-G2osMNX-AeFbaqc)
- [Code execution with MCP](https://www.anthropic.com/engineering/code-execution-with-mcp)
- [Advanced tool use](https://www.anthropic.com/engineering/advanced-tool-use)
- [Sandbox Runtime (srt)](https://github.com/anthropic-experimental/sandbox-runtime)

**Standards & Specifications**
- [AGENTS.md](https://agents.md/)
- [GitHub Spec Kit](https://github.com/github/spec-kit)
- [Spec Driven Development — Sean Grove, OpenAI](https://youtu.be/8rABwKRsec4?si=py8nVArZYMz6YoNA)

**GitHub Copilot**
- [New embedding model](https://github.blog/news-insights/product-news/copilot-new-embedding-model-vs-code/)
- [Context engineering guide](https://code.visualstudio.com/docs/copilot/guides/context-engineering-guide)
- [AGENTS.md support](https://github.blog/changelog/2025-08-28-copilot-coding-agent-now-supports-agents-md-custom-instructions/)
- [Custom instructions](https://docs.github.com/en/copilot/how-tos/configure-custom-instructions)

### Slide 13. Title: "Thank you"

<centered>
Thank you
Questions?
</centered>
