# LLM Basics

## LLMs are stateless
Each request is independent — no built-in memory of previous interactions.

- General example: You ask for a vacation plan in one chat, then open a new chat and expect the model to remember your preferences. It won’t.
- Developer example: You say “fix the bug,” but don’t include the code snippet from the previous message. The model won’t recall it.

How to work with this:
- Chat apps: Keep conversation history in the same thread.
- Dev tools: Include the code, error, and context each time (files, stack traces, version info).

## Knowledge Cutoff
Models are trained up to a specific date and don’t “know” events after that.

| Model Name | Knowledge Cutoff Date |
|------------|-----------------------|
| GPT-5      | October 01, 2024      |
| GPT-4      | September 01, 2021    |
| GPT-3.5    | JSeptember 01, 2021   |

- General example: “Who won the 2024 Olympics?” may be unknown or wrong without fresh context.
- Developer example: Asking about the latest React/Java/Python API introduced after the cutoff.

How to work with this:
- Bring current info: Paste links, snippets, or docs into your prompt.
- Or use web-connected tools/agents; specify sources to consult.

## Context Window
There’s a limit to how much text fits in one request (varies by model, roughly ~8K–200K tokens).

- General example: Long chats get summarized or older parts dropped; details can be lost.
- Developer example: Huge files/projects won’t fit; the model may miss an import or earlier definition.

How to work with this:
- Prioritize essentials: Problem statement → relevant code → error logs → constraints.
- Chunk/summarize: “Summarize this log to the 5 key errors,” then iterate.
- For IDE copilots: Keep the critical file and related files open.

## Hallucinations
Models can sound confident but be wrong or invent APIs.

- General example: Claiming “there are 27 hours in a day.”
- Developer example: Suggesting non-existent APIs like `array.last()` in JavaScript or `HttpClient.getJson()` in Java, or making up config flags.

How to work with this:
- Verify: Run the code, check docs, and rely on compiler/tests/linters.
- Ask for sources: “Cite the official docs for this API,” “Show a minimal reproducible example.”
- Use defensive prompts: “If uncertain, ask clarifying questions instead of guessing.”

## Training Data Bias
Models learn from public data — including outdated, insecure, or low‑quality patterns.

- General example: Recommending practices popular online but not actually best practice.
- Developer example: Proposing string‑concatenated SQL (`"… WHERE id=" + userId`) or weak hashing (MD5) because of legacy examples.

How to work with this:
- Enforce quality: Linters, SAST/DAST, code review, and tests for AI‑generated changes.
- Ask for rationale: “Explain why this is secure and cite the OWASP reference.”

## Key takeaways
- Design prompts and workflows that respect knowledge cutoff and context‑window limits (prioritize essentials, chunk, iterate).
- Bring current, trusted sources for anything time‑sensitive or beyond the cutoff.
- Treat outputs as fallible: verify by running code, use tests/linters, and ask for citations or minimal examples.
- Use defensive prompting: ask clarifying questions when uncertain; be explicit over assuming.
