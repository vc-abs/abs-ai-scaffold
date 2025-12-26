---
name: refine
description: Validate and directly edit repository files with minimal, focused edits
argument-hint: Optional file paths or description of changes to make
---

# Refine Prompt

Validate and directly edit one or more repository files (design docs, code files, scripts, or prompts). Discover and refine providers and consumers to avoid outdated or duplicated content across related files.

**⚠️ RESTRICTIONS:** Do not stage, commit, or push changes. Edits are for human review before commit.

## What

**Input:** File paths (or current file if omitted)

**Output:** Short confirmation (e.g., "Applied 3 edits across 2 files") + list of modified paths

## How

**⚠️ CRITICAL: Read actual file contents. Do not rely on chat history or assumptions.**

1. **Identify targets:** Use provided paths or current file in context
2. **Read file contents:** Always read complete files before making edits
3. **Analyze:** Check for issues, inconsistencies, improvement opportunities
4. **Discover related files:** Search for providers/consumers that may need updates
5. **Apply edits:** Make minimal, focused changes directly to the working tree
6. **Report:** Return short confirmation listing modified files

**⚠️ DO NOT stage, commit, or push.** Edits are for human review.

## Example

| Scenario                                             | Result                                      |
| ---------------------------------------------------- | ------------------------------------------- |
| Invoked for `./doc/design.md`                        | "Applied 1 edit to ./doc/design.md"         |
| No files specified, editing `.github/prompts/xyz.md` | "Applied 2 edits to .github/prompts/xyz.md" |

## Prompt Optimization Strategy

When refining **prompt files** (`.github/prompts/*.md`), apply this approach:

| Strategy                        | When to Use                                                                         | Example                                                    |
| ------------------------------- | ----------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| **Redundancy** (repeat rule 3×) | Critical rules models often violate; instructions that conflict with model defaults | "Ignore chat context", "Read files first", "Do not commit" |
| **Density** (compact info)      | Reference material models already know; token-limited situations                    | Type lists, syntax examples                                |
| **Emphasis** (highlight once)   | Important but intuitive rules; one-time warnings                                    | Formatting requirements                                    |

**For prompts consumed by AI models:**
- Keep redundancy for rules that are frequently violated
- Cut fluff (verbose Why sections, motivational text)
- Repeat critical warnings at: beginning, middle (in How section), and end (Important Rules)
- Models don't need motivation — they need clear, repeated instructions

## Important Rules

- 🛑 **DO NOT stage, commit, or push** — human reviews before commit
- 📖 **READ FILES FIRST:** Always read complete file contents before editing
- ⚠️ **IGNORE CHAT CONTEXT:** Base edits on actual file contents, not conversation memory
- 🔎 **DISCOVER RELATED FILES:** Search for providers/consumers that may need updates
- ✨ **MINIMAL EDITS:** Make focused changes, avoid unnecessary rewrites

Use `/commit` after reviewing changes.
