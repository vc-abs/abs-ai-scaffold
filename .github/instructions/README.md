---
name: repository-assistant-instructions
description: High-level, repository-wide guidance for Copilot assistant behaviors
last-updated: 2025-12-26
---

# Repository Assistant Instructions

This folder contains high-level, repository-wide guidance for Copilot / assistant behaviors. Keep rules concise and stable; individual skills should reference these instructions rather than duplicating policy.

Key rules (short)
- Do not auto-push or auto-deploy. Destructive actions require explicit human invocation.
- Never expose secrets, credentials, or private tokens in prompts or outputs.
- Prefer machine-parsable outputs where applicable (JSON, single-line formats).
- Keep assistant tone neutral, concise, and technical.
- Limit external tool usage; refer to `.github/config/tool-policy.yaml` for allowed tools and commands.

Where to put things
- Global instructions: this directory (`.github/instructions/`)
- Skill prompts: `.github/prompts/` (one skill per file)
- Tool policy: `.github/config/tool-policy.yaml`

Authoring a new skill
1. Copy `.github/prompts/skill-template.md` to `.github/prompts/<skill-name>.md`.
2. Fill metadata, inputs, outputs, and examples.
3. Add `owner` and `last-updated` fields in the front-matter.
4. Add a minimal test input and expected output in the Examples section.
5. Open a PR and request review from the `owner`.

Validation and testing
- Include example diffs or inputs so reviewers can validate outputs.
- Prefer strict output formats to make automated checks possible.

Security & Tooling
- Reference `.github/config/tool-policy.yaml` before adding any command execution.
- If a skill needs new tooling permissions, open an RFC PR and include justification.

Maintenance
- Update `last-updated` and `owner` when editing skills.
- Keep global rules minimal and stable.
