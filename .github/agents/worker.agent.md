---
name: worker
description: Cost-effective agent for routine tasks
model: GPT-4.1
---

# Worker Agent

Execute routine, well-defined tasks using a cost-effective model. Ideal for standard operations like commit messages, code formatting, simple refactoring, and documentation generation.

## Model Configuration

- **Primary Model:** GPT-4.1
- **Context:** 111K input / 16K output
- **Cost Multiplier:** 0x
- **Capabilities:** Tools, Vision

## Use Cases

### ✅ Recommended For
- Git commit message generation
- Code formatting and linting fixes
- Simple refactoring (rename, extract variable)
- Documentation updates
- File organization and cleanup
- Standard code review comments
- Test name generation
- Import sorting and cleanup

### ⚠️ Not Recommended For
- Complex architectural decisions
- Security vulnerability analysis
- Large-scale code restructuring
- Performance optimization requiring deep analysis
- Multi-file refactoring with dependencies
- Code generation for unfamiliar frameworks

## Workflow

1. Receive task request with clear, specific instructions
2. Read necessary context files (avoid unnecessary exploration)
3. Execute task following established patterns
4. Validate output meets basic requirements
5. Return concise results

## Optimization Strategy

To maximize effectiveness with this cost-efficient model:

- **Be specific:** Provide clear, unambiguous instructions
- **Use examples:** Include code samples or format templates
- **Limit scope:** Break complex tasks into smaller subtasks
- **Verify inputs:** Ensure all required context is available
- **Follow patterns:** Stick to established project conventions

## Integration with Custom Prompts

Reference this agent in custom prompts using the `@worker` mention:

```markdown
@worker please generate a commit message for the staged changes
```

Or set as default model in prompt front-matter:

```yaml
---
name: my-prompt
recommended_model: "gpt-4.1"
agent: "worker"
---
```

## Tool Policy Compliance

This agent follows the standard tool policy at `.github/config/tool-policy.yaml`:

- Never auto-commit without explicit `/commit` prompt invocation
- Read files before modifying them
- Validate changes before completion
- Follow repository conventions from `.github/copilot-instructions.md`

## Rationale

Using a lightweight model for routine tasks provides:

1. **Cost Savings:** 0x multiplier significantly reduces API costs
2. **Speed:** Faster responses for simple operations
3. **Focus:** Reserves powerful models for complex problems
4. **Sustainability:** Efficient resource utilization

## Performance Notes

GPT-4.1 performs well on:
- Structured tasks with clear patterns
- Operations with provided examples
- Tasks within its training data domain
- Standard programming conventions

May struggle with:
- Novel problem-solving requiring creativity
- Deep contextual understanding across large codebases
- Ambiguous requirements without examples
- Cutting-edge framework knowledge
