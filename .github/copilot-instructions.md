# GitHub Copilot Instructions

## Tools and Execution Guidelines

See `.github/agents/copilot-helper.md` for authoritative tool preferences and auto-execution policy. Key principles:
- **Preferred shell:** `bash` for automation
- **Git operations:** Use terminal commands; avoid GUI tools for automated workflows
- **Auto-execution policy:** Do not auto-commit without explicit user request (e.g., `/commit` invocation)

## File Naming Conventions
- Use **kebab-case** for files (e.g., `read-me.md`, `user-service.js`)
- Use **SCREAMING_SNAKE_CASE** for constants (e.g., `MAX_RETRIES`, `API_TIMEOUT`)

## Committing Changes
Use the custom prompt `/commit` when committing changes. This prompt ensures:
- Changes are **atomic** and logically related (no mixing unrelated concerns)
- Generates appropriate commit type and message
- Changes are validated before committing to promote clean, focused commits

For detailed commit conventions and workflow, refer to the `/commit` prompt.

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
