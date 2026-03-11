# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Purpose

A Claude Code plugin repository containing reusable agents and skills. Installable via `claude plugin install` or `--plugin-dir`.

## Repository Structure

```
.claude-plugin/plugin.json    — Plugin manifest (name, version, metadata)
.claude/                       — Project-level Claude Code settings for developing this repo
agents/                        — Agent definitions (*.md with YAML frontmatter)
skills/<skill-name>/SKILL.md   — Skill definitions (YAML frontmatter + instructions)
scripts/                       — Helper scripts referenced by skills/agents/hooks
hooks/hooks.json               — Lifecycle hooks (PreToolUse, PostToolUse, etc.)
```

**Critical layout rule:** `agents/`, `skills/`, `hooks/`, and `scripts/` live at the repo root — NOT inside `.claude-plugin/`.

## File Formats

### Agent files (`agents/*.md`)
YAML frontmatter with: `name`, `description` (both required), plus optional `tools`, `disallowedTools`, `model`, `maxTurns`, `permissionMode`, `isolation`, `skills`, `background`, `memory`, `mcpServers`, `hooks`. Body is the system prompt.

### Skill files (`skills/<name>/SKILL.md`)
YAML frontmatter with: `name`, `description`, optional `disable-model-invocation`, `user-invocable`, `allowed-tools`, `model`, `context`, `agent`, `argument-hint`, `hooks`. Body is the skill instructions. Use `$ARGUMENTS`, `$0`, `$1` for args. Use `` !`command` `` for dynamic shell injection.

### Plugin manifest (`.claude-plugin/plugin.json`)
Name, version, description, author, repository, license, keywords.

## Naming Conventions

- Agent/skill names: lowercase, hyphens and numbers only, max 64 chars
- When installed, skills are namespaced: `/aidan-claude-agents:skill-name`
- Use `disable-model-invocation: true` for destructive skills (deploy, send messages, etc.)
