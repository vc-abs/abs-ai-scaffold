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


## Rationale for a Separate Tool Policy

Keep the tool-policy as a distinct, machine-readable file (`.github/config/tool-policy.yaml`) rather than embedding detailed policy text inside each prompt or agent. Reasons:

- **Machine enforcement:** CI, agent runners, and automation can parse YAML to enforce policy programmatically.
- **Precision:** Structured YAML reduces ambiguity (exact commands, scopes, and flags) compared to free-form prose.
- **Automation integration:** Tools that grant or deny actions rely on a canonical policy source they can read at runtime.
- **Change control:** Policies in a single file are easier to review, lint, and test; reviewers can see precise diffs when policy changes.

Risks of embedding policy in prose:

- Automation may not reliably parse human-readable instructions, causing drift between intended and enforced policy.
- Duplicate or conflicting rules can appear across prompts, increasing maintenance burden.

Recommendation: reference the central YAML from prompts and agents, and include only short human-friendly summaries in prompt files when helpful.

