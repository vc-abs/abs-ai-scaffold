---
name: refine
description: Validate and directly edit repository files with minimal, focused edits
tools:
  preferred_shell: bash
  git: terminal
  auto_execute: disallowed
last-updated: 2025-12-26
---

# Refine Prompt

Validate and directly edit one or more repository files (design docs, code files, scripts, or prompts). Discover and refine providers and consumers to avoid outdated or duplicated content across related files.

**⚠️ RESTRICTIONS:** Do not stage, commit, or push changes. Write edits to files so a human can review them before commit.

## Why

This prompt helps maintain consistency and quality across repository files. It identifies issues like:
- Outdated or duplicated content
- Inconsistent formatting or structure
- Missing updates to related files
- Style and convention violations

## What

The prompt performs safe, minimal edits in-place:

**Input:**
- `files`: Zero or more file paths relative to repo root
- If omitted, the current file in context is the target

**Output:**
- Short human-readable confirmation (e.g., "Applied 3 edits across 2 files")
- List of modified file paths
- No diffs or machine-readable JSON output

## How

1. **Identify target files:** Use provided paths or current file in context
2. **Analyze content:** Check for issues, inconsistencies, and improvement opportunities
3. **Discover related files:** Search for providers/consumers that may need updates
4. **Apply edits:** Make minimal, focused changes directly to the working tree
5. **Report results:** Return a short confirmation listing modified files

**Behavior:**
- Single-stage — analyze and apply edits directly (no multi-step modes)
- Edits modify the working tree for human review before commit

## Examples

| Scenario                                                     | Action                               | Result                                      |
| ------------------------------------------------------------ | ------------------------------------ | ------------------------------------------- |
| Invoked for `./doc/design.md`                                | Fix headings, remove duplicated text | "Applied 1 edit to ./doc/design.md"         |
| Invoked with no files while editing `.github/prompts/xyz.md` | Update file in-place                 | "Applied 2 edits to .github/prompts/xyz.md" |
| Multiple files with related content                          | Update all affected files            | "Applied 5 edits across 3 files"            |

## Integration Note

Because edits modify the working tree, reviewers should inspect changes before committing. Use `/commit` after reviewing changes.
