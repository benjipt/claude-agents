# Claude Code Agents

A collection of specialized agents for [Claude Code](https://claude.com/claude-code).

## Installation

Copy the desired agent `.md` files into your Claude Code agents directory:

```bash
# macOS / Linux
cp <agent-name>.md ~/.claude/agents/

# Or clone the entire repo
git clone <repo-url> ~/.claude/agents/
```

## Available Agents

| Agent | Description | Notes |
|-------|-------------|-------|
| [atomic-commit-agent](./atomic-commit-agent.md) | Analyzes completed work and decomposes it into multiple atomic commits | Uses `[scope]` style—see customization below |

## Usage

Agents are automatically available to Claude Code once installed. They can be invoked when the context matches the agent's description.

For example, after completing a feature:

```
> I've finished implementing the user notifications feature. Please commit my changes.
```

Claude Code will recognize this as a task for the `atomic-commit-agent` and use it to decompose your changes into well-structured atomic commits.

## Customization

### Commit Scope Style

The `atomic-commit-agent` uses square bracket scopes by default:

```
feat[auth]: add login endpoint
```

Most conventional commit tooling uses parentheses. To switch to the standard style, find and replace in the agent file:

| Find | Replace |
|------|---------|
| `square brackets for scope` | `parentheses for scope` |
| `[scope]` | `(scope)` |
| `[auth]` | `(auth)` |
| `[contact-form]` | `(contact-form)` |
| `[eslint]` | `(eslint)` |
| `[deps]` | `(deps)` |
| `[utils]` | `(utils)` |

Or run:

```bash
sed -i '' 's/\[scope\]/(scope)/g; s/\[auth\]/(auth)/g; s/\[contact-form\]/(contact-form)/g; s/\[eslint\]/(eslint)/g; s/\[deps\]/(deps)/g; s/\[utils\]/(utils)/g; s/square brackets/parentheses/g' atomic-commit-agent.md
```

## Agent Format

Each agent is a markdown file with YAML frontmatter:

```yaml
---
name: agent-name
description: When to use this agent
tools: Bash, TodoWrite
model: haiku
color: green
---

Agent instructions go here...
```

### Frontmatter Fields

| Field | Required | Description |
|-------|----------|-------------|
| `name` | Yes | Unique identifier for the agent |
| `description` | Yes | When Claude Code should invoke this agent |
| `tools` | Yes | Comma-separated list of tools the agent can use |
| `model` | No | Model to use (`haiku`, `sonnet`, `opus`) |
| `color` | No | Status indicator color |

## Contributing

Contributions are welcome! When submitting a new agent:

1. Follow the agent format above
2. Include clear examples in the agent body
3. Keep the tool list minimal—only include what's necessary
4. Test the agent before submitting
