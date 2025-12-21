---
tools:
  preferred_shell: bash
  git: terminal
  auto_execute: disallowed
policy_reference: .github/config/tool-policy.yaml
---
## Streamline Prompt

Purpose: Make safe, minimal, in-place edits to one or more repository files (docs, code, scripts).

Behavior and expectations:
- Single-stage — analyze and apply edits directly to the working tree. Do not perform multi-step modes.
- Do not stage, commit, or push changes. Write edits to files so a human can review them before commit.

Input:
- `files`: zero or more file paths relative to repo root. If omitted, the current file in context is the target.

Output and reporting:
- Do not print diffs or output machine-readable JSON. After making edits, return a short human-readable confirmation, e.g. "Applied 3 edits across 2 files" and list the modified file paths.

Examples:
- Invoked for `./doc/design.md`: fix headings and remove duplicated policy text, write the updated file in-place, and return: "Applied 1 edit to ./doc/design.md".
- Invoked with no `files` while editing `.github/prompts/xyz.md`: update that file in-place and return a short confirmation listing the changed file.

Integration note:
- Because edits modify the working tree, reviewers should inspect changes before committing. A `scripts/commit.sh` wrapper is recommended but optional.

This prompt focuses on making safe, minimal edits in-place for human review; it does not stage, commit, or push changes.
