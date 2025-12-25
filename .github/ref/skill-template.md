---
name: skill-template
owner: <team-or-person>
allowed_tools: []
purpose: Short description of the skill's goal
output_format: "<type>(<scope>): <subject>" # example; replace as needed
last-updated: 2025-12-23
---

# Skill Template

Purpose
- One-line description of what this skill does.

Inputs
- What the assistant will receive (e.g., `git diff`, file contents, PR body).

Outputs
- Exact expected output format. Be explicit (single-line commit, JSON array, patch text).

Constraints
- Character limits (e.g., subject ≤ 80 chars).
- Tone (concise, neutral, technical).
- Forbidden actions (no auto-push, no secrets, no external network requests).

Execution Rules
- List terminal commands the skill may run (if any).
- Require explicit invocation for side effects (e.g., `/commit` to run `git commit`).

Examples
- Input (short):
  ```diff
  diff --git a/README.md b/README.md
  @@
  -Old line
  +Added project overview and usage
  ```

- Output (example):
  ```
  docs(readme): add project overview and basic usage
  ```

Testing & Validation
- Provide a minimal test diff or sample input maintainers can use to validate the skill.

Maintenance
- Add `last-updated` and `owner` metadata at top when you change the prompt.

Notes
- Keep skills single-responsibility and machine-parseable when possible.
