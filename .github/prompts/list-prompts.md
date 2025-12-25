---
name: list-prompts
**description**: Scan for available custom prompts from multiple locations and display them in an organized table format
last-updated: 2025-12-25
---

# Help (⚠️ Workspace Scope Limited)

**🚨 IMPORTANT LIMITATION:** When invoked from within a workspace, this prompt may only be able to scan files within the current workspace scope and cannot access global user prompts outside the workspace directory.

## Custom Prompts

| Command             | Location          | Description         |
| ------------------- | ----------------- | ------------------- |
| (scan and populate) | (source location) | (from front-matter) |

**Scan Locations (Priority Order):**
1. `<project-root>/.github/prompts/` - Repository-specific custom prompts
2. `~/.config/Code/User/prompts/` - VS Code user prompts directory
3. User VS Code settings directory - Other user-defined global prompts
4. VS Code extensions - Extension-provided prompts

**Implementation Notes:**
- Extract the `name` and `description` from YAML front-matter
- Format command as: `/<name>`
- Include the source location for reference
- Handle missing front-matter gracefully

