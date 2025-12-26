---
name: commit
description: Analyze changes, verify atomicity, and generate atomic commit messages
agent: worker
---

# Commit Prompt

Analyze uncommitted changes, ensure they are atomic (logically related and focused), and generate an appropriate commit message.

**⚠️ AUTO-EXECUTION:** When the user invokes `/commit`, **execute the commit immediately** without asking for permission. Do not present the message and wait for approval - analyze, generate the message, and commit automatically.

## What

**Input:** Uncommitted changes in the working tree

**Output:** A single-line commit message in the format:
```
<type>(<scope>): <subject>
```

**Types:** `feat` | `fix` | `docs` | `style` | `refactor` | `perf` | `test` | `chore`

## 🚨 CRITICAL: Single-Line Messages Only

**MANDATORY FORMAT:** `git commit -m "<type>(<scope>): <subject>"`

- ✅ **CORRECT:** Single `-m` argument with one line only
- ❌ **WRONG:** Multi-line messages with bullet points or body text
- ❌ **WRONG:** Multiple `-m` arguments
- ❌ **WRONG:** Newlines, bullets, or additional details in the message

**Examples of CORRECT format:**
```bash
git commit -m "feat(auth): add JWT token refresh mechanism"
git commit -m "docs(readme): update installation instructions"
git commit -m "fix(api): resolve null pointer in user service"
```

**Examples of INCORRECT format (DO NOT USE):**
```bash
# WRONG - Multi-line with bullets
git commit -m "feat(auth): add JWT token refresh mechanism

- Implement refresh token endpoint
- Add token expiry validation
- Update middleware"

# WRONG - Multiple -m arguments
git commit -m "feat(auth): add JWT" -m "Details here"
```

**If you find yourself wanting to add details:** The single-line subject should be complete and descriptive enough on its own. DO NOT add a body unless the user explicitly requests it.

## How

### 1. Analyze Changes
```bash
git status
git diff
```

**⚠️ CRITICAL: Ignore all chat/conversation context. Only trust what you read from files.**

**Required actions:**
1. Identify all changed files from `git status` output
2. **Read the complete contents** of ALL changed files using `read_file` tool
3. Understand what each file does from its actual content, not from memory
4. Examine the nature and purpose of changes from the diff
5. Verify all changes are logically related

**Critical Verification:**
- Only reference files that ACTUALLY EXIST in the working tree and git status output
- Use `git ls-files` or `ls` commands to verify file existence before referencing them
- Do not assume files were created just because create_file tool reported success
- Verify the diff shows actual content changes for all referenced files
- **Read full file contents** - do not rely on chat history or assumptions

### 2. Gather Broader Context
**⚠️ IGNORE CHAT MEMORY:** Base understanding ONLY on file contents and diffs.

- **New files:** Read 2-3 similar existing files from the same directory
- **Modified files:** Read related/imported files for context
- **Extract purpose:** From front-matter, docstrings, comments — not from memory
- **Derive scope:** From directory structure and file purpose (read from files)

### 3. Check for Atomicity
- ✅ **Atomic:** All changes contribute to ONE logical unit of work
- ❌ **Not Atomic:** Changes span multiple unrelated concerns
- ⚠️ **If NOT atomic:** STOP and suggest splitting before proceeding

### 4. Generate the Commit Message

**Format:** `<type>(<scope>): <subject>`

**Derive subject from:**
1. **File contents** (what you read from actual files)
2. **The diff** (what changed)
3. **Related file context** (patterns from similar files)

**⚠️ NEVER derive the subject from chat history or conversation context**

**Rules:** Under 80 chars | Imperative mood | No period | Scope from directory structure

### 5. Execute the Commit

**CRITICAL:** Execute immediately without asking for permission. The user already consented by invoking `/commit`.

Execute using terminal commands with a single `-m` argument:

```bash
git add .
git commit -m "<type>(<scope>): <subject>"
```

Example:
```bash
git add .
git commit -m "feat(auth): add JWT token refresh mechanism"
```

## Example

| Step      | Details                                                     |
| --------- | ----------------------------------------------------------- |
| Changes   | TokenRefresher service, refresh endpoint, middleware update |
| Atomicity | ✅ All related to auth feature                               |
| Message   | `feat(auth): add JWT token refresh mechanism`               |

## Important Rules

- 🛑 **NEVER commit non-atomic changes** - suggest splitting instead
- ✅ **Always verify atomicity BEFORE generating the commit message**
- 📝 **The commit message must accurately describe ALL changes in the commit**
- 🔍 **Reviewers should understand the change without additional context**
- ⚠️ **IGNORE CHAT CONTEXT:** Read files directly - never trust conversation memory
- 📖 **READ FILES FIRST:** Always read complete file contents before generating commit messages
- 🔎 **GATHER CONTEXT:** Search for related files to understand patterns and conventions
