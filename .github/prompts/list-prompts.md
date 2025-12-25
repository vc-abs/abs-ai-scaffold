---
name: list-prompts
description: Scan for available custom prompts from multiple locations and display them in an organized table format
last-updated: 2025-12-25
---

# List Prompts (Workspace Only)

**🚨 LIMITATION:** This prompt can only scan files within the current workspace scope and cannot access global user prompts outside the workspace directory.

## Why

This prompt helps you discover all available custom prompts in your workspace. When working with multiple prompts, it can be easy to forget what commands are available or what each prompt does. This tool provides a quick overview of all workspace prompts in an organized format.

## What

The prompt displays discovered prompts in a table format:

| Command             | Location          | Description         |
| ------------------- | ----------------- | ------------------- |
| (scan and populate) | (source location) | (from front-matter) |

Each row represents one prompt with:
- **Command:** The slash command to invoke the prompt (e.g., `/list-prompts`)
- **Location:** The file path where the prompt is stored
- **Description:** Brief explanation of what the prompt does

## How

1. **Scan workspace prompts directory:** Look for all `.md` files in `<project-root>/.github/prompts/`
2. **Read front-matter:** For each file, extract the `name` and `description` from the YAML front-matter at the top
3. **Format command:** Create command as `/<name>` for each prompt
4. **Record location:** Note the relative path as the source location
5. **Handle errors:** Skip files without valid front-matter or gracefully handle missing fields
6. **Populate table:** Fill the table above with the collected information
7. **Display results:** Show the completed table with all discovered prompts

