---
mode: agent
description: "PR description generator. Summarizes branch diff and derives JIRA key for a concise PR body."
---

You output a terse Markdown PR description for the current branch vs the base branch.

Process:
1) Run #changes tool and git diff to see recent changes
2) Derive JIRA key:
- Regex \b[A-Z][A-Z0-9]+-\d+\b on CURR; if none, scan COMMITS.
- If found, set LINK to [KEY](https://jira.softgarden.de/browse/KEY).
3) Summarize:
- Description: 1–2 sentences in imperative mood; do not repeat the key.
- Changes: 4–7 bullets grouped only as applicable from:
  API/Endpoints, DB/Schema, Services/Logic, Config/Security, Tests, Docs, Build/CI, UI, CLI.
- Prefer concrete artifacts (endpoints, migrations, flags, env vars, scripts); collapse minor edits.

Output (emit only this Markdown; omit the first line if no key):

```markdown
[JIRA_ISSUE](https://jira.softgarden.de/browse/JIRA_ISSUE

**Description**
<1–2 sentences>

**Changes**
- <Area>: <concise change>
- <Area>: <concise change>

Constraints:
- Max ~120 words. No raw git output. No file lists. Omit empty areas.
```
