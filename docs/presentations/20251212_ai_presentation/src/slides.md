---
title: "Coding with AI"
theme: default
highlighter: shiki
lineNumbers: false
drawings:
  persist: false
transition: slide-left
mdc: true
---

<style>
@import './styles/index.css';
</style>

# Coding with AI

### From Vibe-Coding to Conscious Design of Specifications and Context

<div class="author-info">
  <div>12/12/2025</div>
  <div style="font-weight: 600;">Łukasz Wojtaszek</div>
</div>

---

## From the previous presentation

<div class="mt-4"></div>

### LLM Basics

<div class="grid grid-cols-4 gap-3 mt-4">

<div class="card-compact">
  <div class="flex items-center gap-2 mb-1">
    <span class="text-xl">🔄</span>
    <strong class="text-sm">LLMs are stateless</strong>
  </div>
  <p class="text-xs text-gray-600">Each query is independent. The context from previous interactions must be explicitly provided each time.</p>
</div>

<div class="card-compact">
  <div class="flex items-center gap-2 mb-1">
    <span class="text-xl">📅</span>
    <strong class="text-sm">Knowledge Cutoff</strong>
  </div>
  <p class="text-xs text-gray-600">The models do not know events or data that appeared after the date of completion of their training.</p>
</div>

<div class="card-compact">
  <div class="flex items-center gap-2 mb-1">
    <span class="text-xl">📦</span>
    <strong class="text-sm">Context Window</strong>
  </div>
  <p class="text-xs text-gray-600">There is a limit to the amount of text (tokens) that the model can process in a single query.</p>
</div>

<div class="card-compact">
  <div class="flex items-center gap-2 mb-1">
    <span class="text-xl">👻</span>
    <strong class="text-sm">Hallucinations</strong>
  </div>
  <p class="text-xs text-gray-600">Models can generate false, but credible-sounding information, e.g., by inventing non-existent API functions.</p>
</div>

</div>

<div class="mt-4"></div>

### Coding with AI Workflow

<div class="flex items-center justify-center mt-4">
  <FlowDiagram
    direction="horizontal"
    :compact="true"
    :steps="[
      { label: 'Requirements', sublabel: 'Define requirements', icon: '📋', output: { label: 'jira-task.md', icon: '📄' } },
      { label: 'Plan', sublabel: 'Technical design', icon: '🔍', output: { label: 'plan.md', icon: '📄' } },
      { label: 'Implementation', sublabel: 'Execute plan', icon: '⚙️', output: { label: 'code', icon: '💻' } },
      { label: 'Review', sublabel: 'Quality check', icon: '🗣️', output: { label: 'review.md', icon: '📄' } },
      { label: 'Apply', sublabel: 'Address comments', icon: '🔧', output: { label: 'code', icon: '💻' } },
      { label: 'PR', sublabel: 'Publish', icon: '🚀' }
    ]"
  />
</div>

---

## AI tools evolution

<div class="mt-2">

- **CLI agents popularization**: Claude Code, Cursor CLI, OpenAI Codex, Gemini CLI, Copilot CLI, Droid, OpenCode

- **AGENTS.md standard** introduced by OpenAI: `.github/copilot-instructions.md` → `AGENTS.md`

- **Anthropic open-sourced [Sandbox Runtime (srt)](https://github.com/anthropic-experimental/sandbox-runtime)** — available in CC via `/sandbox`

</div>

<div class="grid grid-cols-2 gap-4 mt-4">
<div>

- **GitHub Copilot changes**:
  - Native `Plan` mode
  - Custom chat modes → Custom agents
  - New embedding model

</div>
<div class="flex items-center justify-center mt-6 flex-col">
  <img src="/img/copilot_new_embedding_model.png" class="rounded-lg shadow-lg max-h-64" />
  <div class="img-source">Src: <a href="https://github.blog/news-insights/product-news/copilot-new-embedding-model-vs-code/" target="_blank">GitHub Copilot - new embedding model</a></div>
</div>
</div>


---

## Spec Driven Development

<div class="mt-4"></div>

### Your Intent is the New Source Code

<div class="mt-4">

> "When we prompt LLMs, we keep the generated code and we delete the prompt. This feels like you shred the source and then you very carefully version control the binary."
>
> — Sean Grove, OpenAI

</div>

<div class="mt-2 text-gray-700 text-sm">
We must stop throwing away our prompts and plans. The specification is the most valuable artifact. It is the executable description of our intent.
</div>

<div class="mt-4"></div>

### GitHub Spec Kit

<div class="mt-4 text-gray-700 text-sm mb-4">
Spec-Driven Development <strong>flips the script</strong> on traditional software development. For decades, code has been king — specifications were just scaffolding we built and discarded once the "real work" of coding began. Spec-Driven Development changes this: <strong>specifications become executable</strong>, directly generating working implementations rather than just guiding them.
</div>

<div class="flex items-center justify-center">
  <FlowDiagram
    direction="horizontal"
    :compact="true"
    :steps="[
      { label: '/constitution', sublabel: 'Project principles', icon: '📜' },
      { label: '/specify', sublabel: 'Define requirements', icon: '📋' },
      { label: '/plan', sublabel: 'Technical design', icon: '🔍' },
      { label: '/tasks', sublabel: 'Generate task list', icon: '✅' },
      { label: '/implement', sublabel: 'Execute tasks', icon: '⚙️' }
    ]"
  />
</div>

---

## Context is everything

<div class="slide-content">
<div class="content">

<div class="mt-4">

> "The only thing other than training your model or playing with temperature that improves the quality of LLM output is quality of input."
>
> — Dexter Horthy

</div>

- **Less is more**: The less context (tokens) you use to do the work, the better results you will get
- **Bad info is catastrophic**: A bad line of research (fundamental misunderstanding of the system) can cause thousands of bad lines of code

<TokenFlow class="mt-8" />

</div>
<div class="slide-source">Src: <a href="https://www.youtube.com/watch?v=IS_y40zY-hc" target="_blank">Advanced Context Engineering for Agents</a></div>
</div>

---

## The pitfalls of long context

<div class="slide-content">
<div class="content">

<div class="mt-4"></div>

### Longer context windows do not automatically generate better responses

<div class="grid grid-cols-2 gap-4 mt-4">
<div>
  <div class="grid grid-cols-2 gap-3">
    <div class="card-compact">
      <div class="flex items-center gap-2 mb-1">
        <span class="text-xl">🧪</span>
        <strong class="text-sm">Poisoning</strong>
      </div>
      <p class="text-xs text-gray-600">Hallucination enters context and is repeatedly referenced, leading to nonsensical strategies (e.g. Gemini Pokémon agent).</p>
    </div>
    <div class="card-compact">
      <div class="flex items-center gap-2 mb-1">
        <span class="text-xl">🎯</span>
        <strong class="text-sm">Distraction</strong>
      </div>
      <p class="text-xs text-gray-600">Model over-focuses on long history, neglecting training knowledge. Issues start ~100K tokens (frontier) or ~32K (smaller models).</p>
    </div>
    <div class="card-compact">
      <div class="flex items-center gap-2 mb-1">
        <span class="text-xl">⚔️</span>
        <strong class="text-sm">Clash</strong>
      </div>
      <p class="text-xs text-gray-600">Conflicting info in multi-turn reasoning. Model relies on early incorrect assumptions — 39% accuracy drop on sharded prompts.</p>
    </div>
    <div class="card-compact">
      <div class="flex items-center gap-2 mb-1">
        <span class="text-xl">🌀</span>
        <strong class="text-sm">Confusion</strong>
      </div>
      <p class="text-xs text-gray-600">Irrelevant tools/docs cause wrong tool selection. Model failed with 46 tools but succeeded with 19.</p>
    </div>
  </div>
  <div class="img-source text-center mt-2">Src: <a href="https://www.dbreunig.com/2025/06/22/how-contexts-fail-and-how-to-fix-them.html" target="_blank">How Long Contexts Fail</a></div>
</div>
<div class="flex flex-col items-center justify-center">
  <div class="text-sm font-semibold mb-2">← Direct tool calls | Tool search + programmatic calling →</div>
  <img src="/img/antrophic_tool_search.png" class="rounded-lg shadow-lg max-h-56" />
  <div class="img-source">Src: <a href="https://youtu.be/2MJDdzSXL74?si=-G2osMNX-AeFbaqc" target="_blank">Building effective agents</a></div>
</div>
</div>
</div>
</div>

---

## Understanding the Context

<div class="grid grid-cols-[60%_40%] gap-4 mt-4">
  <div class="flex flex-col items-center">
    <img src="/img/context_visualisation.png" class="max-h-80 rounded-lg shadow-lg" />
    <div class="img-source">Src: Claude Code Session</div>
  </div>
  <div class="text-sm">
    <ul>
      <li><strong>System prompt</strong> - Core instructions defining Claude's behavior</li>
      <li><strong>System tools</strong> - Built-in tools like Bash, Read, Write, Edit</li>
      <li><strong>MCP tools</strong> - External integrations via Model Context Protocol</li>
      <li><strong>Custom agents</strong> - User-defined specialized subagents</li>
      <li><strong>Memory files</strong> - CLAUDE.md and persistent project context</li>
      <li><strong>Messages</strong> - Conversation history between user and Claude</li>
      <li><strong>Free space</strong> - Available capacity for new content</li>
      <li><strong>Autocompact buffer</strong> - Reserved for automatic context compaction</li>
    </ul>
  </div>
</div>

---

## Understanding the Context

<div class="slide-content">
<div class="content">

<div class="flex justify-center items-center mt-8 flex-col">
  <img src="/img/intentional_compaction.png" class="max-h-80 rounded-lg shadow-lg" />
  <div class="img-source">Src: <a href="https://www.youtube.com/watch?v=IS_y40zY-hc" target="_blank">Advanced Context Engineering for Agents</a></div>
</div>

</div>
</div>

---

## Best Practices

<div class="space-y-5 mt-6">

<div class="flex items-start gap-3">
  <span class="text-xl">🧹</span>
  <div>
    <div class="font-semibold">Keep Context Clean</div>
    <ul class="text-sm text-gray-600 mt-1 ml-4">
      <li>Clear context between phases (Requirements → Plan → Implementation)</li>
      <li>Be precise with files & instructions</li>
      <li>Avoid unnecessary MCPs</li>
    </ul>
  </div>
</div>

<div class="flex items-start gap-3">
  <span class="text-xl">⚙️</span>
  <div>
    <div class="font-semibold">Optimize Your Setup</div>
    <ul class="text-sm text-gray-600 mt-1 ml-4">
      <li>Keep AGENTS.md simple</li>
      <li>Use personal instructions <span class="text-xs text-gray-400">e.g. <code>Always use "lwojtaszek" as author in liquibase migrations</code></span></li>
      <li>Define custom prompts for repeatable tasks</li>
    </ul>
  </div>
</div>

<div class="flex items-start gap-3">
  <span class="text-xl">🔬</span>
  <div>
    <div class="font-semibold">Experiment</div>
    <ul class="text-sm text-gray-600 mt-1 ml-4">
      <li>Different models for different phases (Plan vs Implement vs Review)</li>
    </ul>
  </div>
</div>

</div>

---
layout: center
---

<div class="demo-text animate-pulse">
  DEMO
</div>

---
layout: center
---

<div class="text-center">
  <h2 class="text-4xl font-bold mb-8 gradient-text">Bonus</h2>
  <div class="bonus-card">
    <div class="text-5xl mb-4">📱</div>
    <div class="text-xl font-semibold text-gray-700">Mobile Coding</div>
    <div class="text-sm mt-2 text-gray-500">Claude Code on mobile</div>
    <div class="text-xs mt-6 text-gray-400">[Add screenshot here]</div>
  </div>
</div>

---

## Sources

<div class="grid grid-cols-2 gap-x-8 gap-y-4 mt-4 text-xs">

<div>

**Context Engineering & Agent Design**
- [Advanced Context Engineering for Agents](https://www.youtube.com/watch?v=IS_y40zY-hc)
- [How Long Contexts Fail](https://www.dbreunig.com/2025/06/22/how-contexts-fail-and-how-to-fix-them.html)
- [12-Factor Agents — Dex Horthy](https://www.youtube.com/watch?v=8kMaTybvDUw&t=36s)

</div>
<div>

**Anthropic / Claude**
- [Building effective agents](https://youtu.be/2MJDdzSXL74?si=-G2osMNX-AeFbaqc)
- [Code execution with MCP](https://www.anthropic.com/engineering/code-execution-with-mcp)
- [Advanced tool use](https://www.anthropic.com/engineering/advanced-tool-use)
- [Sandbox Runtime (srt)](https://github.com/anthropic-experimental/sandbox-runtime)

</div>
<div>

**Standards & Specifications**
- [AGENTS.md](https://agents.md/)
- [GitHub Spec Kit](https://github.com/github/spec-kit)
- [Spec Driven Development — Sean Grove, OpenAI](https://youtu.be/8rABwKRsec4?si=py8nVArZYMz6YoNA)

</div>
<div>

**GitHub Copilot**
- [New embedding model](https://github.blog/news-insights/product-news/copilot-new-embedding-model-vs-code/)
- [Context engineering guide](https://code.visualstudio.com/docs/copilot/guides/context-engineering-guide)
- [AGENTS.md support](https://github.blog/changelog/2025-08-28-copilot-coding-agent-now-supports-agents-md-custom-instructions/)
- [Custom instructions](https://docs.github.com/en/copilot/how-tos/configure-custom-instructions)

</div>
</div>

---
layout: center
---

<div class="text-center">
  <h1 class="text-6xl font-bold mb-4 gradient-text">Thank you</h1>
  <p class="text-xl text-gray-500 mt-8">Questions?</p>
</div>
