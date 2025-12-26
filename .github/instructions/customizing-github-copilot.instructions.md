---
name: copilot-customization-guide
description: Complete guide for managing GitHub Copilot customization files
applyTo: ".github/**/*.{prompt.md,agent.md,instructions.md}"
---

# GitHub Copilot Customization Guide

Complete guide for creating, managing, and maintaining GitHub Copilot customization files.

## Required Front-Matter Fields

All GitHub Copilot customization files must include YAML front-matter with required metadata fields.

### Core Required Fields

#### 1. `name`
- Identifier matching the filename (kebab-case)
- Required for: prompts, agents, instructions
- Example: `name: example-prompt`

#### 2. `description`
- Clear, concise explanation of the file's function
- Required for: prompts, agents, instructions
- Example: `description: Brief description of what this does`

### Supported Optional Fields by File Type

#### Prompts (`*.prompt.md`)
- `agent` - Specify which agent should handle this prompt
- `argument-hint` - Hint for prompt arguments
- `model` - Override the default model
- `tools` - Tool-specific configuration

#### Agents (`*.agent.md`)
- `argument-hint` - Hint for agent arguments
- `handoffs` - Define agent handoff rules
- `infer` - Inference configuration
- `model` - Specify model to use
- `target` - Target environment or scope
- `tools` - Tool-specific configuration

#### Instructions (`*.instructions.md`)
- `applyTo` - Glob patterns for files this instruction affects

### Example Front-Matter

**Prompt:**
```yaml
---
name: example-prompt
description: Brief description of what this does
---
```

**Agent:**
```yaml
---
name: example-agent
description: Brief description of what this agent does
model: GPT-4.1
---
```

**Instruction:**
```yaml
---
name: example-instruction
description: Brief description of what this instruction does
applyTo:
  - "src/**/*.ts"
---
```

## Renaming Workflow

When renaming GitHub Copilot customization files:

### 1. Update Front-Matter
Change the `name` field in YAML front-matter to match the new functionality:
```yaml
---
name: new-name
---
```

### 2. Rename the File
Use `git mv` to preserve file history:
```bash
git mv .github/prompts/old-name.prompt.md .github/prompts/new-name.prompt.md
git mv .github/agents/old-name.agent.md .github/agents/new-name.agent.md
git mv .github/instructions/old-name.instructions.md .github/instructions/new-name.instructions.md
```

**Note:** After renaming, use the `/commit` prompt to stage and commit changes with proper atomicity and message formatting.

## Consistency Rules

- Filename must match the `name` field (both in kebab-case)
- Always include `name` and `description` fields
- Keep descriptions concise (one sentence preferred)
- Use `git mv` when renaming to preserve file history
- For instructions, use `applyTo` (not `applies_to`) for glob patterns
