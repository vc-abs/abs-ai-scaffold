---
name: customization-file-requirements
applies_to:
  - ".github/prompts/**/*.md"
  - ".github/agents/**/*.md"
  - ".github/instructions/**/*.md"
  - ".github/config/**/*.{yaml,yml}"
purpose: Required front-matter fields for all GitHub Copilot customization files
last-updated: 2025-12-25
---

# GitHub Copilot Customization File Requirements

All GitHub Copilot customization files must include YAML front-matter with required metadata fields.

## Required Front-Matter Fields

### 1. `name`
- Identifier matching the filename (kebab-case)
- Example: `name: example-prompt`

### 2. `description` or `purpose`
- Clear, concise explanation of the file's function
- Use `description` for prompts
- Use `purpose` for instructions and configs

### 3. `last-updated`
- Date in YYYY-MM-DD format
- Update whenever the file is modified

## Example Front-Matter

```yaml
---
name: example-prompt
description: Brief description of what this does
last-updated: 2025-12-25
---
```

## Additional Optional Fields

- `applies_to` - Glob patterns for files this instruction affects
- `owner` - Team or person responsible
- `auto_execute` - Execution behavior for prompts
- `output_format` - Expected output format
- `tools` - Tool-specific configuration

## Consistency Rules

- Filename must match the `name` field (both in kebab-case)
- Keep descriptions concise (one sentence preferred)
- Update `last-updated` on every modification
