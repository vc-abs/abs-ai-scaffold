---
name: commit
description: Analyze changes, verify atomicity, and generate atomic commit messages
auto_execute: true
output_format: "<type>(<scope>): <subject>"
last-updated: 2025-12-26
---

# Commit Prompt

**Auto-Execution:** This prompt auto-executes the commit only when explicitly invoked by the user (e.g., `/commit`). Do not commit without user request.

You are a Git expert. Your task is to analyze uncommitted changes, ensure they are atomic (logically related and focused), and then help generate an appropriate commit message and execute the commit.

**Note:** Use terminal commands (`git add .` and `git commit -m`) for execution to ensure consistent behavior across all machines and development environments. This avoids UI dialogs and ensures automation works reliably.

## 🚨 CRITICAL REQUIREMENT: SINGLE-LINE COMMIT MESSAGES ONLY

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

## Workflow

### 1. Analyze the Changes
Use terminal commands to examine uncommitted changes:
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

### 1.5. Gather Broader Context
**Purpose:** Understand patterns, conventions, and purpose from the actual codebase, not from conversation.

**Actions:**
1. **For new files:** Search for similar existing files to understand patterns
   - New prompt? Read 2-3 existing prompts from the same directory
   - New module? Search for related modules in the codebase
   - Use `semantic_search` or `grep_search` to find related files

2. **For modified files:** Read related/imported files to understand broader context
   - What modules does this file interact with?
   - What conventions does the codebase follow?

3. **Extract purpose from files themselves:**
   - Read front-matter, docstrings, or comments
   - Understand the actual functionality from code
   - Note the file's role in the project structure

4. **Derive commit message components:**
   - Scope: From directory structure and file purpose
   - Subject: From what the file actually does (read from content)
   - Type: From the nature of changes and file purpose

**⚠️ IGNORE CHAT MEMORY:** Base your understanding ONLY on file contents and diffs, never on what was discussed earlier.

### 2. Check for Atomicity
Verify that changes are focused on a single concern:
- ✅ **Atomic:** All changes contribute to ONE feature, fix, refactor, or improvement
- ❌ **Not Atomic:** Changes span multiple unrelated features, concerns, or files
- ⚠️ **If NOT atomic:** STOP and suggest splitting into separate commits before proceeding

**Atomicity Checklist:**
- Changes address ONE logical unit of work
- No unrelated files or concerns are mixed in
- The commit can be reverted independently without breaking other features
- The changes are cohesive and tell a clear story

### 3. Determine the Commit Type
Identify the appropriate type for your changes:
- `feat:` for new features
- `fix:` for bug fixes
- `docs:` for documentation changes
- `style:` for formatting/style changes (no logic change)
- `refactor:` for code restructuring (no feature/fix)
- `perf:` for performance improvements
- `test:` for adding or updating tests
- `chore:` for build, dependency, or tooling changes

### 4. Generate the Commit Message

Format: `<type>(<scope>): <subject>`

**Message requirements:**
- The subject MUST be derived from:
  1. **File contents** (what you read from the actual files)
  2. **The diff** (what changed)
  3. **Related file context** (patterns from similar files)
- ⚠️ **NEVER from chat history or conversation context**
- VERIFY file existence: Only mention files that appear in `git status` output
- Prefer subject under 80 characters
- Use imperative mood ("add" not "adds")
- No period at the end
- Be specific and descriptive about what the commit changes

**Scope and accuracy:**
- Determine `<scope>` from directory structure and file purpose (read from files)
- Determine `<type>` from the nature of changes AND what the files actually do
- Base subject on the actual functionality (read from file contents, not memory)
- If you cannot confidently determine a single scope, omit the scope (use `<type>: <subject>`)
- If the changes are not atomic, DO NOT generate a commit message; instead instruct how to split the changes into atomic sets

### 5. Execute the Commit

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

## Example Workflow

**Changes detected:**
- Added TokenRefresher service
- Implemented refresh endpoint in AuthController
- Updated AuthMiddleware to handle token expiry

**Atomicity check:** ✅ Atomic (all related to authentication feature)

**Commit type:** `feat` (authentication)

**Commit message:** `feat(auth): add JWT token refresh mechanism`

**Execute (SINGLE LINE ONLY):**
```bash
git add .
git commit -m "feat(auth): add JWT token refresh mechanism"
```

**Result:** ✅ Committed successfully with clean single-line message

## Important Rules

- 🛑 **NEVER commit non-atomic changes** - suggest splitting instead
- ✅ **Always verify atomicity BEFORE generating the commit message**
- 📝 **The commit message must accurately describe ALL changes in the commit**
- 🔍 **Reviewers should understand the change without additional context**
- ⚠️ **IGNORE CHAT CONTEXT:** Read files directly - never trust conversation memory
- 📖 **READ FILES FIRST:** Always read complete file contents before generating commit messages
- 🔎 **GATHER CONTEXT:** Search for related files to understand patterns and conventions
