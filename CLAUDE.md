# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **documentation-only plugin collection** (no Python packages, no build system, no tests) providing Django development guidance to AI coding agents. It is distributed as plugins for Claude Code, Codex (VS Code Copilot), and the generic `plugins` CLI.

Forked from [vintasoftware/django-ai-plugins](https://github.com/vintasoftware/django-ai-plugins), licensed MIT.

## Architecture

### Plugin Types

- **Skills** (`plugins/*/skills/SKILL.md`) — Persistent guidance auto-loaded when relevant. Use YAML frontmatter (`name`, `description`) and progressive disclosure via reference files.
- **Agents** (`plugins/*/agents/<name>.md`) — Autonomous specialists. Use YAML frontmatter with an additional `model` field (e.g., `model: opus`).

### Plugins

| Plugin | Type | Path |
|--------|------|------|
| `django-expert` | Skill | `plugins/django-expert/` |
| `django-celery-expert` | Skill | `plugins/django-celery-expert/` |
| `cdrf-expert` | Skill | `plugins/cdrf-expert/` |
| `django-reviewer` | Agent | `plugins/django-reviewer/` |

### Per-Plugin Directory Layout

```
plugin-name/
├── .claude-plugin/plugin.json      # Claude Code metadata
├── .codex-plugin/plugin.json       # Codex metadata (includes skills path, interface, defaultPrompt)
├── skills/                         # For skill-type plugins
│   ├── SKILL.md                    # Main skill definition (YAML frontmatter + instructions)
│   └── references/                 # On-demand reference docs loaded by topic
│       └── *.md
├── agents/                         # For agent-type plugins
│   └── <agent-name>.md             # Agent definition (YAML frontmatter + system prompt)
└── README.md
```

### Distribution Manifests

- **Claude Code marketplace**: `.claude-plugin/marketplace.json` (root) — lists plugins for Claude Code
- **Codex marketplace**: `.agents/plugins/marketplace.json` (root) — lists plugins for Codex with policy fields
- **Per-plugin manifests**: each plugin has both `.claude-plugin/plugin.json` and `.codex-plugin/plugin.json`

Note: The Claude marketplace manifest currently lists 3 plugins (missing `cdrf-expert`), while the Codex marketplace lists all 4.

## Content Conventions

### SKILL.md Format
```yaml
---
name: skill-name
description: Multi-sentence description of when the skill triggers
---
```
Followed by: Overview, When to Use (trigger phrases), Instructions/Workflow, Examples.

### Agent .md Format
```yaml
---
name: agent-name
description: What the agent does and when to use it
model: opus
---
```
Followed by: system prompt with numbered priorities and review criteria.

### Reference Files
- Progressive disclosure pattern: SKILL.md is concise; detailed topic docs live in `references/`
- Reference files use standard Markdown with H1 topic, H2 subtopics, and code examples
- `django-expert/skills/references/README.md` explains how to customize/populate reference docs

## Integration

Works alongside the [django-ai-boost MCP server](https://github.com/vintasoftware/django-ai-boost) for enhanced Django development capabilities.

## When Making Changes

- Keep skills concise; put detailed content in `references/` files
- Maintain both `.claude-plugin/plugin.json` and `.codex-plugin/plugin.json` when adding or modifying plugins
- Update both root marketplace manifests (`.claude-plugin/marketplace.json` and `.agents/plugins/marketplace.json`) when adding new plugins
- The Codex `plugin.json` has extra fields (`skills`, `interface`, `defaultPrompt`, `capabilities`) that the Claude version does not — keep these in sync with the skill content
