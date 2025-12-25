---
name: commit
description: Analyze changes, verify atomicity, and generate atomic commit messages
auto_execute: true
output_format: "<type>(<scope>): <subject>"
last-updated: 2025-12-26
---

# Commit Prompt

Analyze uncommitted changes, ensure they are atomic (logically related and focused), and generate an appropriate commit message.

**⚠️ AUTO-EXECUTION:** This prompt auto-executes the commit only when explicitly invoked by the user (e.g., `/commit`). Do not commit without user request.

## Why

This prompt ensures consistent, high-quality commit messages by:
- Verifying changes are atomic (single logical unit of work)
- Deriving commit messages from actual file contents, not chat memory
- Enforcing conventional commit format for clear project history
- Gathering codebase context to understand patterns and conventions

## What

**Input:** Uncommitted changes in the working tree

**Output:** A single-line commit message in the format:
```
<type>(<scope>): <subject>
```

**Supported types:**
- `feat:` new features
- `fix:` bug fixes
- `docs:` documentation changes
- `style:` formatting/style changes (no logic change)
- `refactor:` code restructuring (no feature/fix)
- `perf:` performance improvements
- `test:` adding or updating tests
- `chore:` build, dependency, or tooling changes

## 🚨 CRITICAL: Single-Line Messages Only

**MANDATORY FORMAT:** `git commit -m "<type>(<scope>): <subject>"`

✅ **CORRECT:**
```bash
git commit -m "feat(auth): add JWT token refresh mechanism"
git commit -m "docs(readme): update installation instructions"
```

❌ **WRONG:** Multi-line messages, multiple `-m` arguments, or bullet points

## How

### 1. Analyze Changes
```bash
git status
git diff
```

**⚠️ CRITICAL: Ignore chat/conversation context. Only trust what you read from files.**

**Required actions:**
1. Identify all changed files from `git status` output
2. **Read complete contents** of ALL changed files using `read_file` tool
3. Understand what each file does from its actual content, not from memory
4. Examine the nature and purpose of changes from the diff
5. Verify all changes are logically related

**Verification:**
- Only reference files that ACTUALLY EXIST in `git status` output
- Use `ls` commands to verify file existence before referencing
- **Read full file contents** - do not rely on chat history or assumptions

### 2. Gather Broader Context
Understand patterns and conventions from the actual codebase, not from conversation.

**For new files:** Search for similar existing files (e.g., read 2-3 existing prompts from the same directory)

**For modified files:** Read related/imported files to understand broader context

**Extract purpose from files:** Read front-matter, docstrings, or comments to understand actual functionality

**⚠️ IGNORE CHAT MEMORY:** Base understanding ONLY on file contents and diffs.

### 3. Check for Atomicity
Verify that changes are focused on a single concern:
- ✅ **Atomic:** All changes contribute to ONE feature, fix, refactor, or improvement
- ❌ **Not Atomic:** Changes span multiple unrelated features or concerns
- ⚠️ **If NOT atomic:** STOP and suggest splitting into separate commits

**Checklist:**
- Changes address ONE logical unit of work
- No unrelated files or concerns are mixed in
- The commit can be reverted independently
- The changes tell a clear story

### 4. Generate the Commit Message

**Format:** `<type>(<scope>): <subject>`

**Requirements:**
- Derive subject from: file contents, the diff, and related file context
- ⚠️ **NEVER from chat history or conversation context**
- Prefer subject under 80 characters
- Use imperative mood ("add" not "adds")
- No period at the end

**Scope determination:**
- Determine `<scope>` from directory structure and file purpose
- If you cannot confidently determine a single scope, omit it (use `<type>: <subject>`)
- If changes are not atomic, DO NOT commit; suggest splitting instead

### 5. Execute the Commit

```bash
git add .
git commit -m "<type>(<scope>): <subject>"
```

## Example

| Step      | Details                                                           |
| --------- | ----------------------------------------------------------------- |
| Changes   | Added TokenRefresher service, refresh endpoint, middleware update |
| Atomicity | ✅ All related to authentication feature                           |
| Type      | `feat`                                                            |
| Message   | `feat(auth): add JWT token refresh mechanism`                     |

## Important Rules

- 🛑 **NEVER commit non-atomic changes** - suggest splitting instead
- ⚠️ **IGNORE CHAT CONTEXT:** Read files directly - never trust conversation memory
- 📖 **READ FILES FIRST:** Always read complete file contents before generating messages
- 🔎 **GATHER CONTEXT:** Search for related files to understand patterns
