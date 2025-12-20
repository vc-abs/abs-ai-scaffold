# Copilot Helper Agent

**Tool Policy:**
```yaml
tools:
  prefer: bash
  git: terminal
  auto_execute: disallowed
  dry_run_required: false
```

Purpose: provide a single authoritative reference for tools, execution guidelines, and best practices for any AI agents or custom prompts in this repository.

## Tools and Execution Guidelines

- **Preferred shell for automation:** `bash` (use terminal for scripted operations)
- **Git operations:** Use terminal `git` commands (`git status`, `git diff`, `git add .`, `git commit -m "<message>"`) for automation; avoid GUI tools (GitKraken, SourceTree) for automated workflows.
- **File and CI operations:** Use shell scripts and terminal tools (grep, diff, sed, awk) when automating.
- **Wrapper scripts:** Projects may provide `scripts/commit.sh` to encapsulate commit behavior for agents; prefer calling wrappers from prompts when available.
- **Why:** Terminal commands ensure consistent behavior across machines and avoid interactive UI dialogs that block automation.

## Auto-Execution Policy

- **No auto-commits by default:** Do not commit changes unless the user explicitly requests it (e.g., via `/commit` prompt invocation or explicit `/do commit` instruction).
- **Explicit invocation required:** Auto-execution is allowed only when a user invokes a prompt or agent that is designed to auto-execute (e.g., `/commit` prompt when user types `/commit`).
- **Safe operations:** Analysis, dry-run, and informational operations may be auto-executed without explicit confirmation.

## Agent Responsibilities

- Serve as the canonical source for tool choices and execution patterns across prompts and agents in this repository.
- Help authors create prompts that explicitly prefer terminal commands when automation is intended.
- Provide example terminal commands for common operations (git status, add, commit) and note why they are preferred.

## Usage

- Reference this agent from prompt-level or repository-level documentation (e.g., `.github/copilot-instructions.md`, `.github/prompts/*`).
- When a prompt needs to instruct an AI or agent how to act at session start, include a short pointer to this agent and, if necessary, paste the minimal commands required for that operation.

# Copilot Helper Agent

Purpose: provide a single authoritative reference for tools, execution guidelines, and best practices for any AI agents or custom prompts in this repository.

## Tools and Execution Guidelines

- **Preferred shell for automation:** `bash` (use terminal for scripted operations)
- **Git operations:** Use terminal `git` commands (`git status`, `git diff`, `git add .`, `git commit -m "<message>"`) for automation; avoid GUI tools (GitKraken, SourceTree) for automated workflows.
- **File and CI operations:** Use shell scripts and terminal tools (grep, diff, sed, awk) when automating.
- **Wrapper scripts:** Projects may provide `scripts/commit.sh` to encapsulate commit behavior for agents; prefer calling wrappers from prompts when available.
- **Why:** Terminal commands ensure consistent behavior across machines and avoid interactive UI dialogs that block automation.

## Auto-Execution Policy

- **No auto-commits by default:** Do not commit changes unless the user explicitly requests it (e.g., via `/commit` prompt invocation or explicit `/do commit` instruction).
- **Explicit invocation required:** Auto-execution is allowed only when a user invokes a prompt or agent that is designed to auto-execute (e.g., `/commit` prompt when user types `/commit`).
- **Safe operations:** Analysis, dry-run, and informational operations may be auto-executed without explicit confirmation.

## Agent Responsibilities

- Serve as the canonical source for tool choices and execution patterns across prompts and agents in this repository.
- Help authors create prompts that explicitly prefer terminal commands when automation is intended.
- Provide example terminal commands for common operations (git status, add, commit) and note why they are preferred.

## Usage

- Reference this agent from prompt-level or repository-level documentation (e.g., `.github/copilot-instructions.md`, `.github/prompts/*`).
- When a prompt needs to instruct an AI or agent how to act at session start, include a short pointer to this agent and, if necessary, paste the minimal commands required for that operation.
