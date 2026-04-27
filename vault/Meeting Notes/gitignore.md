---
tags:
  - project-file
  - git
aliases:
  - .gitignore
---

# .gitignore

## Overview

Standard git ignore configuration for the project. Currently configured to exclude `.claude/settings.local.json` so each developer's personal Claude Code permissions and preferences are never accidentally committed to the shared repository.

**Path:** `.gitignore` (project root)
**Owner:** Shared — committed to git

## Open Questions

- none

## Session Log

### 2026-04-27 — Initial creation [shipped]

- **What was done:** Created with a single rule to ignore `settings.local.json`.
- **Decisions:** Only personal settings are excluded; shared settings.json is committed intentionally.
- **Notes / Caveats:** Add additional ignore patterns here as the project grows (e.g. `.env`, `node_modules`, build artifacts).
- **Related:** [[claude-settings-local]], [[claude-settings]]
