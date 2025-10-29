## AI Tools

Presentation recording: [AI trip&tricks-20250811_130119-Meeting Recording.mp4](https://softgarden-my.sharepoint.com/:v:/r/personal/krzysztof_piotrowski_softgarden_de/Documents/AI/AI%20trip%26tricks-20250811_130119-Meeting%20Recording.mp4?csf=1&web=1&e=RTu13C&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0%3D)

A small collection of AI-related materials and utilities:

- Presentations (Slidev) about LLM fundamentals
- GitHub Copilot custom chat modes and prompts to streamline day-to-day development
- Curated learning resources

### Repository structure

- `docs/presentations/20250807_ai_presentation/`
  - `llms_basics.md`: Source draft for the talk
  - `src/`: Slidev project (slides + assets)
    - `slides.md`: Slidev slides
    - `public/img/`: Images used in slides
    - `package.json`: Slidev scripts (`dev`, `build`, `export`)
- `tools/github-copilot/`
  - `chatmodes/`: Custom Copilot Chat modes (Plan/Implement workflow)
  - `prompts/`: Reusable Copilot prompts (code review, JIRA issue, PR description)
- `docs/useful_resources.md`: Links to videos, articles, channels, and references

### LLM Basics — Slidev presentation

Located at `docs/presentations/20250807_ai_presentation/src`.

Prerequisites:
- Node.js 18+ recommended

Run locally:

```bash
cd docs/presentations/20250807_ai_presentation/src
npm i
npm run dev
```

Build/export:

```bash
npm run build   # static site
npm run export  # PDF
```

Notes:
- Slides reference images from `public/img/` via relative paths like `/img/…`
- Slidev documentation: https://sli.dev/

### GitHub Copilot — custom chat modes and prompts

- `tools/github-copilot/chatmodes/COPILOT_CHATMODES.md`: Overview of using Plan → Implement workflow.
  - Plan mode (`global/Plan.chatmode.md`): Generates an implementation plan with sections (Overview, Requirements, Steps, Testing). Plans are stored only on request.
  - Implement mode (`global/Implement.chatmode.md`): Focused Java implementation guidelines (minimal edits, DDD patterns, MapStruct DTOs, testing conventions, progress tracking).
- `tools/github-copilot/prompts/COPILOT_PROMPTS.md`: Notes about global prompts.
  - Prompts available under `prompts/global/`:
    - `codeReview.prompt.md`: Run immediate code review with a concise checklist (readability, errors, security, tests).
    - `jiraIssue.prompt.md`: Turn notes into a structured JIRA issue description template.
    - `prDescription.prompt.md`: Generate a short PR description from git diff; auto-detects JIRA key pattern.

Suggested usage (VS Code):
- Global chat modes/prompts live under `~/Library/Application\ Support/Code/User/prompts/`
- Repo-level chat modes can live under `.github/chatmodes` if you choose to adopt that structure

### Learning resources

See `docs/useful_resources.md` for curated links on ML fundamentals, Copilot usage tips, X accounts, YouTube channels, and other references.