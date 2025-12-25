---
name: copilot-customization-guide
applies_to:
  - ".github/prompts/**/*.md"
  - ".github/agents/**/*.md"
  - ".github/instructions/**/*.md"
  - ".github/config/**/*.{yaml,yml}"
purpose: Complete guide for managing GitHub Copilot customization files
last-updated: 2025-12-25
---

# GitHub Copilot Customization Guide

Complete guide for creating, managing, and maintaining GitHub Copilot customization files.

## Required Front-Matter Fields

All GitHub Copilot customization files must include YAML front-matter with required metadata fields.

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

### Example Front-Matter

```yaml
---
name: example-prompt
description: Brief description of what this does
last-updated: 2025-12-25
---
```

### Additional Optional Fields

- `applies_to` - Glob patterns for files this instruction affects
- `owner` - Team or person responsible
- `auto_execute` - Execution behavior for prompts
- `output_format` - Expected output format
- `tools` - Tool-specific configuration

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
git mv .github/path/old-name.md .github/path/new-name.md
```

**Note:** After renaming, use the `/commit` prompt to stage and commit changes with proper atomicity and message formatting.

## Consistency Rules

- Filename must match the `name` field (both in kebab-case)
- Keep descriptions concise (one sentence preferred)
- Update `last-updated` on every modification
- Use `git mv` when renaming to preserve file history
