---
tags:
  - project-file
  - skill
  - obsidian
  - core
aliases:
  - obsidian-vault-workflow
  - SKILL.md (obsidian-vault-workflow)
---

# Skill: obsidian-vault-workflow

## Overview

The core project skill that enforces a mandatory two-phase read/write protocol for `vault/`. Must be invoked at the **start** of every task (Phase 1: find and read the topic file + recent Meeting Notes/Content Briefs/Brand Guidelines for context) and at the **end** of every task (Phase 2: write or update the topic file with a dated session log entry). Organizes the vault as one file per topic using four canonical folders. Every session entry must include wikilinks to related notes.

**Path:** `the-five-agent/skills/obsidian-vault-workflow/SKILL.md`
**Frontmatter name:** `obsidian-vault-workflow`
**Vault folders:** `vault/Meeting Notes/`, `vault/Content Briefs/`, `vault/Publishing Log/`, `vault/Brand Guidelines/`

## Open Questions

- Should the vault live inside `the-five-agent/vault/` or at workspace root `vault/`?

## Session Log

### 2026-04-27 — Documented and applied [shipped]

- **What was done:** Read the full skill, then applied it to document all project files — this session IS the first application of the workflow.
- **Decisions:** Created vault at workspace root (`vault/`) since the git repo is initialized there. Vault uses Meeting Notes folder for all file documentation (architecture/code category).
- **Notes / Caveats:** The skill mandates Phase 1 context loading before every task — even when no topic file exists yet (as was the case here). The checklist at the end of the skill file is the authoritative "done" definition.
- **Related:** [[skill-obsidian-markdown]], [[skill-obsidian-bases]], [[claude-commands-example]], [[project-file-documentation]]
