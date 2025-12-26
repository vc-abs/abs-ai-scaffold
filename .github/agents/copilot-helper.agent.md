---
name: copilot-helper
description: Guide creation of agents and prompts with consistent structure
argument-hint: Specify type of artifact to create (prompt, agent, instruction)
---

# Copilot Helper Agent

Purpose: guide the creation of new agents and prompts with consistent structure, tool choices, and runtime policy references.

## Creating a New Agent or Prompt

### 1. Follow Naming Conventions

When creating new artifacts, follow these naming patterns:

- **Prompts:** Named like functions using imperative verbs (e.g., `generate-report`, `create-document`, `refine`)
- **Instructions:** Similar to prompts but use present-continuous tense (e.g., `generating-report`, `creating-document`, `refining`)
- **Agents:** Use nouns as names (e.g., `report-generator`, `document-creator`, `refiner`)

### 2. Reference the Shared Tool Policy

All new agents and prompts must reference the shared tool policy at runtime. The policy is injected via `copilot-instructions.md` context; no local embedding needed.

### 3. Implement Core Behavior

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
3. [Reference `.github/copilot-instructions.md` as needed for tool-specific guidance]
```

## Maintenance

### Extending the Tool Policy

To add new tool configurations or constraints:
1. Edit `.github/copilot-instructions.md` directly (see **Tool Policy** section)
2. All referencing agents/prompts automatically respect the updated policy
3. No need to update individual prompts unless behavior changes require it


## Rationale for Embedded Tool Policy

The tool policy is embedded in `.github/copilot-instructions.md` rather than a separate machine-readable file. Reasons:

- **Model visibility:** All Copilot models see the policy automatically without requiring file-reading capabilities.
- **Single source of truth:** One document contains all behavioral rules and constraints.
- **Reduced duplication:** Agents and prompts reference the instructions file rather than duplicating policy text.
- **Immediate enforcement:** Policy is present in the model's context at execution time.

Trade-offs:

- Machine enforcement via CI requires parsing Markdown instead of YAML
- For now, CI validation of policy is deferred in favor of runtime enforcement

Recommendation: Keep policy embedded in `.github/copilot-instructions.md` and reference it from prompts and agents. If CI validation becomes necessary, consider generating a machine-readable derivative from the instructions file.

## Guideline: Embedded Human-Readable Policies

Tool policies and runtime guardrails are embedded in `.github/copilot-instructions.md` to ensure all Copilot models see them without requiring file-reading capabilities. This approach prioritizes runtime enforcement over CI validation. Use clear, structured formatting (bullet points, code blocks) to make policies easy to parse visually and reference from prompts and agents.

