---
tool_policy:
  canonical_ref: ".github/config/tool-policy.yaml"
  policy_version: "2025-12-25"
  ci_required: true
  commit_allowed: false
  policy_hash: "sha256:46daf97d244614d54ab52edfaa6c4c4aecdb146c0c1a55f5a36dc5b06bca3070"
---

# GitHub Copilot Instructions

⛔ **CRITICAL:** Never auto-commit or auto-push changes. Only execute `git commit` when the user invokes the `/commit` prompt. See `.github/config/tool-policy.yaml` for the canonical policy and enforcement details.

## File Naming Conventions
- Use **kebab-case** for files (e.g., `read-me.md`, `user-service.js`).
- Use **SCREAMING_SNAKE_CASE** for constants (e.g., `MAX_RETRIES`, `API_TIMEOUT`).

## Code Style
- Follow `.editorconfig` settings for formatting.
- **Indentation:** 2 spaces for YAML files; tabs for other files and shell scripts.
- **Line endings:** LF (Unix-style).
- **Encoding:** UTF-8 for all files.
- **Trailing whitespace:** Remove all trailing whitespace.
- **Final newline:** Always include a newline at end of file.

## Documentation Standards
- Keep documentation in sync with code changes.
- Use clear, concise language in comments.

## Architecture Principles
- Follow separation of concerns (SoC).
- Keep dependencies minimal and well-documented.
- Use interfaces/types for public APIs.
- Organize code/instructions by feature or functional domain.
- Avoid deep nesting; keep functions readable.

## Tool Policy
The canonical, authoritative policy lives at `.github/config/tool-policy.yaml` (machine-readable). This document contains only a minimal front-matter summary for quick agent checks (keys: `canonical_ref`, `policy_version`, `ci_required`, `commit_allowed`, `policy_hash`).

Guidance: agents must consult the canonical policy for enforcement; CI should verify `policy_hash` matches the canonical file. Do not auto-commit from CI; bots may open PRs to propose synchronized updates.

