# aidan-claude-agents

A suite of reusable agents and skills for [Claude Code](https://claude.ai/code).

## Quick Start

### Install as a plugin

```bash
claude plugin install /path/to/aidan-claude-agents --scope user
```

Or from GitHub:

```bash
claude plugin install https://github.com/YOUR_USERNAME/aidan-claude-agents --scope user
```

### Use during development

```bash
claude --plugin-dir /path/to/aidan-claude-agents
```

### Use a specific agent

Once installed, agents are available automatically. Skills are namespaced:

```
/aidan-claude-agents:skill-name
```

## What's Included

### Agents (`agents/`)

Custom agents that Claude Code can delegate tasks to. Each agent has a focused role, specific tool access, and a tailored system prompt.

### Skills (`skills/`)

User-invocable slash commands and background knowledge. Each skill lives in its own directory with a `SKILL.md` file.

## Adding New Agents

Create a new `.md` file in `agents/` with YAML frontmatter:

```yaml
---
name: my-agent
description: What this agent does and when to use it
tools: Read, Grep, Bash
model: sonnet
maxTurns: 10
---

System prompt instructions here.
```

## Adding New Skills

Create a new directory in `skills/` with a `SKILL.md`:

```yaml
---
name: my-skill
description: What this skill does
user-invocable: true
allowed-tools: Read, Grep
---

Instructions for the skill here. Use $ARGUMENTS for user input.
```

## License

MIT
