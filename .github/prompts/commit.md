# Commit Prompt

**Tool Policy:** See `.github/agents/copilot-helper.md` for authoritative guidelines.

**Auto-Execution:** This prompt auto-executes the commit only when explicitly invoked by the user (e.g., `/commit`). Do not commit without user request.

You are a Git expert. Your task is to analyze uncommitted changes, ensure they are atomic (logically related and focused), and then help generate an appropriate commit message and execute the commit.

**Note:** Use terminal commands (`git add .` and `git commit -m`) for execution to ensure consistent behavior across all machines and development environments. This avoids UI dialogs and ensures automation works reliably.

## Workflow

## Tools and Execution Guidelines
- **Preferred shell for automation:** `bash`.
- **Use terminal commands for Git operations:** `git status`, `git diff`, `git add .`, `git commit -m "<message>"`.
- **Avoid GUI Git tools** for automated workflows (GitKraken, SourceTree, etc.), as they may require interactive approval.
- **Optional wrapper:** Projects may provide `scripts/commit.sh` to encapsulate commit behavior for agents.


### 1. Analyze the Changes
Use terminal commands to examine uncommitted changes:
```bash
git status
git diff
```
Understand what was modified:
- Which files were changed?
- What is the nature of each change?
- Are all changes logically related?

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
- REQUIRE a single-line subject (one-line commit message). Do not include a separate multi-line body unless the user explicitly requests it.
- The subject MUST be derived strictly from the actual diff (use `git diff`/`git status` to determine changes). Do not reference files, edits, or states that are not present in the diff or working tree.
- Prefer subject under 80 characters.
- Use imperative mood ("add" not "adds").
- No period at the end.
- Be specific and descriptive about what the commit changes.

Notes on scope and accuracy:
- Determine the `<type>` and optional `<scope>` strictly from the changes seen in the diff. If you cannot confidently determine a single scope, omit the scope (use `<type>: <subject>`).
- If the changes are not atomic, DO NOT generate a commit message; instead instruct how to split the changes into atomic sets.

### 5. Execute the Commit
Generate the commit and execute it using terminal commands. Use a single `-m` argument containing the one-line subject only.

```bash
git add .
git commit -m "<type>(<scope>): <subject>"
```

Example:
```bash
git add .
git commit -m "feat(auth): add JWT token refresh mechanism"
```

The changes are now committed to the repository (with a single-line subject). If a multi-line body is required, ask the user explicitly before including it.

## Example Workflow

**Changes detected:**
- Added TokenRefresher service
- Implemented refresh endpoint in AuthController
- Updated AuthMiddleware to handle token expiry

**Atomicity check:** ✅ Atomic (all related to authentication feature)

**Commit type:** `feat` (authentication)

**Commit message:** `feat(auth): add JWT token refresh mechanism`

**Execute:** Commit changes with the generated message

## Important Rules

- 🛑 **NEVER commit non-atomic changes** - suggest splitting instead
- ✅ **Always verify atomicity BEFORE generating the commit message**
- 📝 **The commit message must accurately describe ALL changes in the commit**
- 🔍 **Reviewers should understand the change without additional context**
