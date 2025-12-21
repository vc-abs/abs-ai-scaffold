---
tools:
  prefer: bash
  git: terminal
  auto_execute: disallowed
---
## Streamline Prompt

Purpose: validate and directly edit one or more repository files (design docs, code files, scripts, or image-generation pipelines). The prompt accepts file paths or — when no paths are provided — uses the current file in context as the target.

Behavior and expectations:
- Single-stage edit: discover relationships between files (references, duplicated policy text, inconsistent frontmatter/schema, shell mismatches) and perform minimal, focused edits directly in the working tree.
- The prompt does NOT stage, commit, or push changes. All edits are written to files in the working tree so the human can review them before committing.

Input:
- `files`: zero or more file paths relative to repo root. If omitted, the prompt uses the current file in context.

Output and reporting:
- The prompt does not print diffs. It writes edits directly to files in the working tree and does not output JSON.
- It may return a short human-readable confirmation `summary` such as: "Applied 3 edits across 2 files." Review the modified files in the IDE or with `git diff` before committing.

Safety:
- Never run `git commit` or `git push`. Leave the working tree modified and await human review and explicit commit.
- Avoid destructive commands. Prefer in-file edits that are reversible; rely on version control history rather than creating backup files.

Examples:
- When invoked for `./doc/design.md`, fix headings and remove duplicated policy text, write the updated file in-place, and return the unified diff for the change.
- When invoked with no `files` while editing `.github/prompts/xyz.md`, treat that file as the target and update it in-place, returning the diff.
Integration note:
- Because edits modify the working tree, reviewers should inspect changes before committing. A `scripts/commit.sh` wrapper is recommended for consistent commit validation, but is optional and not required by this prompt.

This prompt focuses on making safe, minimal edits in-place for human review; it does not stage, commit, or push changes.
