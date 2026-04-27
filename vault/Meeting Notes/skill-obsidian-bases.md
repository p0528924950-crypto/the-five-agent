---
tags:
  - project-file
  - skill
  - obsidian
aliases:
  - obsidian-bases
  - SKILL.md (obsidian-bases)
---

# Skill: obsidian-bases

## Overview

Skill definition for creating and editing Obsidian Bases (`.base` files) — database-like views of vault notes using YAML configuration. Provides the full schema reference: filters (AND/OR/NOT with operators), formula language (date arithmetic, conditionals, string formatting), view types (table, cards, list), summary formulas, and YAML quoting rules. Activates when working with `.base` files or when the user mentions Bases, table views, card views, or computed columns.

**Path:** `the-five-agent/skills/obsidian-bases/SKILL.md`
**Frontmatter name:** `obsidian-bases`

## Open Questions

- none

## Session Log

### 2026-04-27 — Documented [shipped]

- **What was done:** Read and documented the full skill. No changes made to the skill itself.
- **Decisions:** Kept separate from obsidian-markdown since Bases have their own YAML format and are distinct from regular .md files.
- **Notes / Caveats:** Duration type from date subtraction does NOT support `.round()` directly — must access `.days` first (e.g. `(date - today()).days.round(0)`).
- **Related:** [[skill-obsidian-markdown]], [[skill-obsidian-vault-workflow]], [[skills-readme]]
