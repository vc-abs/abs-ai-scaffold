# Copilot Helper Agent

Purpose: guide the creation of new agents and prompts with consistent structure, tool choices, and runtime policy references.

## Creating a New Agent or Prompt

### 1. Reference the Shared Tool Policy

All new agents and prompts must reference the shared tool policy at runtime. The policy is injected via `copilot-instructions.md` context; no local embedding needed.

### 2. Implement Core Behavior

- Define the agent/prompt's purpose clearly
- Document inputs, outputs, and key workflow steps
- Reference tool policy for any automation (git, file operations, etc.)
- **Do not embed tool policy details** — users/agents will read the referenced file at runtime

### 3. Example Structure

```markdown
# My New Prompt

## Purpose
[Clear description of what the prompt does]

## Workflow
1. [Step 1]
2. [Step 2]
3. [Reference tool policy as needed for tool-specific guidance]
```

## Maintenance

### Extending the Tool Policy

To add new tool configurations or constraints:
1. Edit `.github/config/tool-policy.yaml` directly
2. All referencing agents/prompts automatically respect the updated policy
3. No need to update individual prompts unless behavior changes require it

