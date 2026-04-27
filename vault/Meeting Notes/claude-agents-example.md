---
tags:
  - project-file
  - claude-code
  - agent
aliases:
  - agents/example.md
---

# .claude/agents/example.md

## Overview

Placeholder sub-agent definition in `.claude/agents/`. Every `.md` file with valid YAML frontmatter (`name`, `description`) in this directory becomes a named sub-agent that Claude Code can spawn automatically when the task matches the agent's description. The `example.md` demonstrates the required frontmatter format.

**Path:** `.claude/agents/example.md`
**Owner:** Shared — committed to git

## Open Questions

- What specialized agents are needed for this project (e.g. a code-reviewer agent, a documentation agent)?

## Session Log

### 2026-04-27 — Placeholder created [wip]

- **What was done:** Created example.md as a template for future sub-agents.
- **Decisions:** Used minimal frontmatter (name + description) to show the required format.
- **Notes / Caveats:** The agent description field is critical — Claude uses it to decide when to spawn this agent automatically.
- **Related:** [[claude-commands-example]]
