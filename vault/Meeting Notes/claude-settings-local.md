---
tags:
  - project-file
  - claude-code
  - settings
  - local
aliases:
  - settings.local.json
---

# .claude/settings.local.json

## Overview

Personal local Claude Code settings file that is excluded from git via `.gitignore`. Contains per-developer tool permissions that should not be shared. Currently pre-allows `git init` and `git remote` Bash commands so the developer is not prompted for those specific operations.

**Path:** `.claude/settings.local.json`
**Owner:** Individual developer only — never committed

## Open Questions

- none

## Session Log

### 2026-04-27 — Initial creation [shipped]

- **What was done:** Created with allow rules for `Bash(git init *)` and `Bash(git remote *)` — added automatically by the Claude Code hooks system during git setup.
- **Decisions:** Kept separate from shared settings.json so personal preferences don't force approvals on other developers.
- **Notes / Caveats:** Each developer will have their own version of this file; it is machine-specific.
- **Related:** [[claude-settings]], [[gitignore]]
