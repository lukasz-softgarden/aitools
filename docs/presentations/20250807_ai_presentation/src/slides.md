---
title: LLM Basics
theme: default
highlighter: shiki
layout: cover
---

# LLM Basics

AI concepts every developer should know

---
layout: image-right
image: /img/1_llms_are_stateless.png
---

## LLMs are stateless

Each request is independent — no built-in memory of previous interactions.

- You ask for a vacation plan in one chat, then open a new chat and expect the model to remember your preferences. It won’t.
- You say “fix the bug,” but don’t include the code snippet from the previous message. The model won’t recall it.

**How to work with this:**

- Chat apps: Keep conversation history in the same thread.
- Dev tools: Include the code, error, and context each time (files, stack traces, etc).

---
layout: image-right
image: /img/2_knowledge_cutoff.png
---

## Knowledge Cutoff

Models are trained up to a specific date and don’t “know” events after that.

- “Who won the 2024 Olympics?” may be unknown or wrong without fresh context.
- Asking about the latest React/Java/Python API introduced after the cutoff.

**How to work with this:**

- Bring current info: Paste links, snippets, or docs into your prompt.
- Or use web-connected tools/agents; specify sources to consult.

---
layout: image-right
image: /img/2_knowledge_cutoff.png
---

## Knowledge Cutoff

If you ask GPT-5 who is current President of the USA, it will answer "Joe Biden".

| Model Name | Knowledge Cutoff Date |
|------------|-----------------------|
| GPT-5      | October 01, 2024      |
| GPT-4      | September 01, 2021    |
| GPT-3.5    | September 01, 2021    |

Source: https://www.allmo.ai/articles/list-of-large-language-model-cut-off-dates

---
layout: image-right
image: /img/3_context_window.png
---

## Context Window

There’s a limit to how much text fits in one request (varies by model, roughly ~8K–200K tokens).

- Long chats get summarized or older parts dropped; details can be lost.
- Huge files/projects won’t fit; the model may miss an import or earlier definition.

**How to work with this:**

- Prioritize essentials: Problem statement → relevant code → error logs → constraints.
- Chunk/summarize: “Summarize this log to the 5 key errors,” then iterate.
- For IDE copilots: Keep the critical file and related files open.

---
layout: image-right
image: /img/4_hallucinations.png
---

## Hallucinations

Models can sound confident but be wrong or invent APIs.

- Claiming “there are 27 hours in a day.”
- Suggesting non-existent APIs like `array.last()` in JavaScript or `HttpClient.getJson()` in Java, or making up config flags.

**How to work with this:**

- Verify: Run the code, check docs, and rely on compiler/tests/linters.
- Ask for sources: “Cite the official docs for this API,”
- Use defensive prompts: “If uncertain, ask clarifying questions instead of guessing.”

---
layout: image-right
image: /img/5_training_bias.png
---

## Training Data Bias

Models learn from public data — including outdated, insecure, or low‑quality patterns.

- Recommending practices popular online but not actually best practice.
- Proposing string‑concatenated SQL (`"… WHERE id=" + userId`) or weak hashing (MD5) because of legacy examples.

**How to work with this:**

- Enforce quality: Linters, SAST/DAST, code review, and tests for AI‑generated changes.
- Ask for rationale: “Explain why this is secure and cite the OWASP reference.”

---
layout: image-right
image: /img/6_key_takeaways.png
---

## Key takeaways

- Design prompts and workflows that respect knowledge cutoff and context‑window limits (prioritize essentials, chunk, iterate).
- Bring current, trusted sources for anything time‑sensitive or beyond the cutoff.
- Treat outputs as fallible: verify by running code, use tests/linters, and ask for citations or minimal examples.
- Use defensive prompting: ask clarifying questions when uncertain; be explicit over assuming.

---
layout: center
---

# DEMO

---

## Bonus — This presentation was 90% created by AI

1. Created `llms_basics.md` draft with an initial list of topics.
2. Asked GPT-5 to review, explain the topics, and suggest additional topics where helpful.
3. Generated the slide visuals from the finalized `llms_basics.md` using ChatGPT’s agentic image workflow ([conversation](https://chatgpt.com/share/6895fcec-7ee0-800e-a0dc-7452902a4d02)).
4. Did research in Perplexity to choose the tool to create a presentation from Markdown file => [sli.dev](https://sli.dev/)
5. Asked GPT-5 to create a presenation (pasted link to [sli.dev](https://sli.dev/) docs)
6. Asked GPT-5 to introduce minor edits to the slides.

---
layout: center
---

# Thank you