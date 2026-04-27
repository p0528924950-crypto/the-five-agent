---
tags:
  - project-file
  - claude-code
  - settings
aliases:
  - settings.json
---

# .claude/settings.json

## Overview

Project-level Claude Code settings file committed to git and shared across all contributors. Controls which tools Claude may use automatically (allow/deny permissions) and defines hooks that fire on events like tool calls or session start/end. Currently holds an empty allow/deny list and no hooks.

**Path:** `.claude/settings.json`
**Owner:** Shared — committed to git

## Open Questions

- What tool permissions should be pre-allowed to reduce prompts for common operations?
- Are any hooks needed (e.g. run tests after file edits)?

## Session Log

### 2026-04-27 — Initial creation [wip]

- **What was done:** Created with empty permissions and hooks structure.
- **Decisions:** Left blank intentionally; permissions will be added as the team identifies repeating approval patterns.
- **Notes / Caveats:** Use the `/fewer-permission-prompts` skill to auto-generate allow rules from past session transcripts.
- **Related:** [[claude-settings-local]], [[claude-md]]
