---
name: renaming-copilot-customizations
applies_to:
  - ".github/prompts/**/*.md"
  - ".github/agents/**/*.md"
  - ".github/instructions/**/*.md"
  - ".github/config/**/*.{yaml,yml}"
purpose: Renaming workflow for GitHub Copilot customization files
last-updated: 2025-12-25
---

# Renaming GitHub Copilot Customization Files

Best practices for renaming GitHub Copilot customization files (prompts, agents, instructions, configs).

## Workflow

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

## File Organization Reference

- **`.github/prompts/`** - Active custom prompts (named after their command)
- **`.github/ref/`** - Reference templates and documentation
- **`.github/config/`** - Configuration files and policies
- **`.github/agents/`** - Agent definitions and workflows
- **`.github/instructions/`** - Additional Copilot instruction files
