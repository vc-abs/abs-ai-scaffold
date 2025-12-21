# Copilot Helper Agent

Purpose: guide the creation of new agents and prompts with consistent structure, tool choices, and runtime policy references.

## Creating a New Agent or Prompt

### 1. Add Tool Policy Reference

All new agents and prompts must reference the shared tool policy. Add this line near the top:

```markdown
**Tool Policy:** See `.github/config/tool-policy.yaml` for authoritative tool preferences and execution constraints.
```

This ensures agents/prompts automatically pull the latest tool policy at runtime without embedding it.

### 2. Implement Core Behavior

- Define the agent/prompt's purpose clearly
- Document inputs, outputs, and key workflow steps
- Reference tool policy for any automation (git, file operations, etc.)
- **Do not embed tool policy details** — users/agents will read the referenced file

### 3. Safety and Constraints

All agents/prompts must respect `.github/config/tool-policy.yaml`, especially:
- **No auto-commit:** Only commit when user explicitly invokes the commit prompt
- **No auto-push:** Only push when explicitly requested
- **Use terminal commands:** Prefer bash/shell over GUI tools for automation

### 4. Example Structure

```markdown
# My New Prompt

**Tool Policy:** See `.github/config/tool-policy.yaml` for authoritative tool preferences and execution constraints.

## Purpose
[Clear description of what the prompt does]

## Workflow
1. [Step 1]
2. [Step 2]
3. [Reference tool policy as needed for tool-specific guidance]

## Safety
- Respects no-auto-commit constraint (see tool policy)
- Uses terminal commands for git operations
```

## Extending the Tool Policy

To add new tool configurations or constraints:
1. Edit `.github/config/tool-policy.yaml` directly
2. All referencing agents/prompts automatically respect the updated policy
3. No need to update individual prompts unless behavior changes require it

## Available Prompts

Current prompts in `.github/prompts/`:
- **`/commit`** — Analyze changes, verify atomicity, generate one-line commit message from diff
- **`/help`** — Quick reference and prompt discovery
- **`/refine`** — Validate and directly edit files in-place

See `.github/prompts/help.md` for user-facing prompt documentation.

