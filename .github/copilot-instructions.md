# GitHub Copilot Instructions

⛔ **Critical constraint:** Do not auto-commit or auto-push changes. Only commit when the user explicitly invokes `/commit`.

## Overview

Repository-level guidance for Copilot workflows, file naming, and conventions. For authoritative tool policies and execution guidelines, see `.github/agents/copilot-helper.md`. Users can invoke `/help` to discover available prompts.

## File Naming Conventions
- Use **kebab-case** for files (e.g., `read-me.md`, `user-service.js`)
- Use **SCREAMING_SNAKE_CASE** for constants (e.g., `MAX_RETRIES`, `API_TIMEOUT`)

## Code Style
- Follow `.editorconfig` settings for formatting
- **Indentation:** 2 spaces for YAML files, tabs for other files
- **Line endings:** LF (Unix-style)
- **Encoding:** UTF-8 for all files
- **Trailing whitespace:** Remove all trailing whitespace
- **Final newline:** Always include a newline at end of file

## Documentation Standards
- Keep documentation in sync with code changes
- Use clear, concise language in comments

## Architecture Principles
- Follow separation of concerns (SoC)
- Keep dependencies minimal and well-documented
- Use interfaces/types for public APIs
- Organize code / instructions by feature or functional domain
- Avoid deep nesting; keep functions readable

## Language-Specific Rules
- **Shell Scripts:** Use meaningful variable names; add header comments with purpose
