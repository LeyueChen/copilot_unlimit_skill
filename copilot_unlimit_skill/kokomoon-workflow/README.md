# kokomoon-workflow

An interactive workflow skill for AI agents that enforces structured design-review-execute loops with mandatory user confirmation at every stage.

## What it does

This skill ensures AI agents follow a disciplined workflow:

1. **Analyze** the user's request thoroughly before acting
2. **Design** a detailed plan with a structured todo list
3. **Confirm** with the user through an interactive inquiry window
4. **Execute** tasks only after user approval
5. **Review** results with the user before closing

The key enforcement: the agent **cannot** end the conversation without explicit user consent.

## Installation

### VS Code (Copilot)

Copy the `kokomoon-workflow/` directory to one of:
- `.github/skills/` (project-level)
- `~/.copilot/skills/` (user-level)

### Claude Code

Copy to `.claude/skills/` or install via plugin marketplace.

### Other Agent Skills clients

Place in any directory that your client scans for skills following the [Agent Skills specification](https://agentskills.io/specification).

## Usage

The skill activates automatically when the agent detects a multi-step task. You can also invoke it manually:

```
/kokomoon-workflow Analyze the audio signal chain and fix the output issue
```

## Specification Compliance

This skill follows the [Agent Skills specification](https://agentskills.io/specification):
- YAML frontmatter with required `name` and `description` fields
- Optional `license`, `compatibility`, and `metadata` fields
- Markdown body with structured instructions
- Progressive disclosure friendly (< 500 lines)

## License

Apache-2.0. See [LICENSE](./LICENSE) for details.
