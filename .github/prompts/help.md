---
name: help
description: List all available custom prompts and agents in the workspace in an organized table format
last-updated: 2025-12-26
---

# Help: List Prompts and Agents (Workspace Only)

**🚨 LIMITATION:** This prompt can only scan files within the current workspace scope and cannot access global user prompts or agents outside the workspace directory.

## Why

This prompt helps you discover all available custom prompts and agents in your workspace. When working with multiple prompts and agents, it can be easy to forget what commands or assistants are available or what each does. This tool provides a quick overview of all workspace prompts and agents in an organized format.

## What

The prompt displays discovered prompts and agents in two tables:

### Prompts
| Command             | Location          | Description         |
| ------------------- | ----------------- | ------------------- |
| (scan and populate) | (source location) | (from front-matter) |

Each row represents one prompt with:
- **Command:** The slash command to invoke the prompt (e.g., `/help`)
- **Location:** The file path where the prompt is stored
- **Description:** Brief explanation of what the prompt does

### Agents
| Agent Name          | Location          | Purpose/Description |
| ------------------- | ----------------- | ------------------- |
| (scan and populate) | (source location) | (from front-matter) |

Each row represents one agent with:
- **Agent Name:** The name of the agent (from front-matter)
- **Location:** The file path where the agent is stored
- **Purpose/Description:** Brief explanation of what the agent does

## How

1. **Scan workspace prompts directory:** Look for all `.md` files in `<project-root>/.github/prompts/`
2. **Scan workspace agents directory:** Look for all `.md` files in `<project-root>/.github/agents/`
3. **Read front-matter:** For each file, extract the `name` and `description` (or `purpose`) from the YAML front-matter at the top
4. **Format command:** For prompts, create command as `/<name>`; for agents, use the agent name
5. **Record location:** Note the relative path as the source location
6. **Handle errors:** Skip files without valid front-matter or gracefully handle missing fields
7. **Populate tables:** Fill the tables above with the collected information
8. **Display results:** Show the completed tables with all discovered prompts and agents

