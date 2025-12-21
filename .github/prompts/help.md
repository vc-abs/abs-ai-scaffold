# Help

**Tool Policy:** See `.github/config/tool-policy.yaml` for authoritative tool preferences and execution constraints.

## Custom Prompts

- **`/commit`** — Analyze changes, verify atomicity, and generate a one-line commit message strictly from the diff. Executes only when explicitly invoked.
- **`/help`** — Quick reference for available prompts and repository conventions (this prompt).
- **`/refine`** — Validate and directly edit files (design docs, code, scripts) by discovering relationships and applying minimal, focused edits in-place. Never commits or pushes changes.

## Getting Started

1. Read `.github/copilot-instructions.md` for project conventions and file naming
2. Invoke `/commit` when you want to commit changes (analyze, verify atomicity, and execute)
3. Invoke `/refine` to validate and edit files in-place
4. Follow `.editorconfig` for formatting

## Quick Links

- **Conventions:** `.github/copilot-instructions.md`
- **Commit Workflow:** `/commit` prompt
- **Refine:** `/refine` prompt
- **Editor Config:** `.editorconfig`
