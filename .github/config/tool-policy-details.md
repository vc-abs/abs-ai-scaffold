---
# Tool Policy Details

This document contains human-readable descriptions, rationale, and examples for the compact
`tool-policy.yaml` runtime configuration. Prompts and agents should reference the compact
policy for enforcement but can present sections of this file to users when showing warnings
or explanations.

Sections below match keys in `tool-policy.yaml` under `guardrails`.

1) push
  - Description: Agents and prompts must not push to remote repositories automatically.
  - Rationale: Remote pushes can modify shared state and cause unexpected deploys or CI runs.
  - Example: Never run `git push` without explicit human approval and a clear description
    of what will be pushed.

2) api_access
  - Description: Agents must not call external web APIs, cloud provider APIs, or other
    networked services on behalf of the user unless the user explicitly authorizes it.
  - Rationale: API calls may leak credentials, incur costs, or change remote infrastructure.
  - Example: Do not call deployment APIs, package registries, secret stores, or telemetry
    endpoints without explicit, auditable user consent.

3) arbitrary_commands
  - Description: Agents should not execute arbitrary shell commands not listed in `shell_commands`.
  - Rationale: Arbitrary commands may be destructive or exfiltrate data.
  - Example: Disallow `curl | sh`, `ssh`, or other unapproved commands unless explicitly whitelisted.

4) operations_beyond_branch
  - Description: Automated actions must remain scoped to the current branch and working tree.
  - Rationale: Branch switching, ref manipulation, or force-pushing risks cross-branch contamination.
  - Example: Avoid creating/deleting branches, force-pushes, or changing remotes without consent.

5) local_git_operations
  - Description: Local git operations listed in the allowlist may be run automatically.
  - Rationale: Read and small local write operations are useful for automation; allow them when safe.
  - Example: `git status`, `git diff`, `git log` can run automatically. `git add` and `git commit`
    are allowed to be automated per the compact policy, but implementations may require an explicit
    confirmation step depending on repository policy.

6) report_summary
  - Description: Agents must present a concise human-readable summary of proposed changes before
    taking impactful actions.
  - Example: A one-paragraph summary plus a short changed-file list.

7) warnings_and_decisions
  - Description: When detecting destructive or sensitive changes, agents must warn and require
    explicit approval before proceeding.
  - Example: Deleting files, upgrading dependencies, or touching infra should trigger an explicit
    escalation and typed confirmation by the user.

Versioning and updates
----------------------
- Keep `guardrails.version` in `tool-policy.yaml` in sync with this document when structural
  changes are made.
- Use `policy_details_path` to locate the companion doc; prompts may link to it for full
  explanations instead of embedding long text.

If you want me to further compress names (shorter keys) or convert this to JSON for compactness,
I can do that next.
