# AGENTS.md

This file provides guidance to Agents when working with code in this repository.

## Repository Overview

Collection of AI-related materials: Slidev presentations about LLM fundamentals, GitHub Copilot custom chat modes/prompts, and curated learning resources. No Java code despite the path name.

## Common Commands

### Slidev Presentations
```bash
cd docs/presentations/20250807_ai_presentation/src  # or 20251128_ai_presentation
npm i
npm run dev     # local dev server
npm run build   # static site
npm run export  # PDF export
```
Requires Node.js 18+. Images referenced via `/img/...` from `public/img/`.

## Structure

- `docs/presentations/` - Slidev presentations (slides.md + assets)
- `tools/github-copilot/chatmodes/` - Custom Copilot chat modes (Plan/Implement workflow)
- `tools/github-copilot/prompts/` - Reusable prompts (code review, JIRA issue, PR description)
- `docs/useful_resources.md` - Curated ML/AI learning links

## GitHub Copilot Tools

### Chat Modes (Plan → Implement workflow)
- **Plan mode**: Generate implementation plans (Overview, Requirements, Steps, Testing). Store as file only on explicit request.
- **Implement mode**: Execute plan with progress tracking via markdown checkboxes.

### Prompts
- `codeReview.prompt.md` - Reviews changes for quality/security
- `jiraIssue.prompt.md` - Converts notes to structured JIRA description
- `prDescription.prompt.md` - Generates terse PR body from git diff; auto-detects JIRA key pattern `[A-Z][A-Z0-9]+-\d+`

Global prompts/chatmodes location: `~/Library/Application Support/Code/User/prompts/`
