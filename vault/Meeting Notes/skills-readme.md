---
tags:
  - project-file
  - skills
aliases:
  - skills/README.md
---

# skills/README.md

## Overview

Root README for the `skills/` directory — the development workspace for custom slash command definitions. Skills are authored and refined here, then copied or linked to `.claude/commands/` when ready for activation. Separating authoring from activation keeps the active commands folder clean and lets drafts evolve freely.

**Path:** `skills/README.md`
**Owner:** Shared — committed to git

## Open Questions

- Should skills have a version or status field in their frontmatter?

## Session Log

### 2026-04-27 — Initial creation [shipped]

- **What was done:** Created README explaining the two-stage workflow: author in skills/, activate in .claude/commands/.
- **Decisions:** Kept directory separate from .claude/commands/ so draft skills don't become live commands prematurely.
- **Notes / Caveats:** The `the-five-agent/skills/` subfolder pre-existed with the three Obsidian skills; workspace-root `skills/` was created alongside the git infrastructure.
- **Related:** [[claude-commands-example]], [[skill-obsidian-vault-workflow]], [[skill-obsidian-bases]], [[skill-obsidian-markdown]]
