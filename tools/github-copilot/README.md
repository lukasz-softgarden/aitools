# GitHub Copilot — Custom Chat Modes & Prompts

## Chat Modes (Plan → Implement)

- **Plan mode** (`chatmodes/global/Plan.chatmode.md`): Generate implementation plan (Overview, Requirements, Steps, Testing). Store as file on request.
- **Implement mode** (`chatmodes/global/Implement.chatmode.md`): Execute plan with progress tracking.

See [COPILOT_CHATMODES.md](chatmodes/COPILOT_CHATMODES.md) for workflow details.

## Prompts

- `codeReview.prompt.md` — Immediate code review checklist (readability, errors, security, tests)
- `jiraIssue.prompt.md` — Convert notes to structured JIRA description
- `prDescription.prompt.md` — Generate PR body from git diff; auto-detects JIRA key `[A-Z][A-Z0-9]+-\d+`

See [COPILOT_PROMPTS.md](prompts/COPILOT_PROMPTS.md).

## Installation

Global chat modes/prompts location (VS Code):
```
~/Library/Application Support/Code/User/prompts/
```

Repo-level: `.github/chatmodes/`
