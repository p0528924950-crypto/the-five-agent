---
tags:
  - project-file
  - skill
  - obsidian
aliases:
  - obsidian-markdown
  - SKILL.md (obsidian-markdown)
---

# Skill: obsidian-markdown

## Overview

Skill definition for Obsidian Flavored Markdown — the Obsidian-specific extensions on top of CommonMark and GFM. Covers wikilinks (`[[Note]]`), embeds (`![[file]]`), callouts (`> [!type]`), frontmatter properties, inline tags (`#tag`), Obsidian comments (`%%`), highlight syntax (`==`), LaTeX math, and Mermaid diagrams. Activates when creating or editing `.md` files in an Obsidian vault context.

**Path:** `the-five-agent/skills/obsidian-markdown/SKILL.md`
**Frontmatter name:** `obsidian-markdown`

## Open Questions

- none

## Session Log

### 2026-04-27 — Documented [shipped]

- **What was done:** Read and documented the full skill.
- **Decisions:** This skill complements obsidian-vault-workflow; the workflow skill handles WHEN/WHERE to write, this skill handles HOW to format the content.
- **Notes / Caveats:** Always use `[[wikilinks]]` for intra-vault note references — never `[text](file.md)` markdown links; Obsidian tracks renames automatically only for wikilinks.
- **Related:** [[skill-obsidian-bases]], [[skill-obsidian-vault-workflow]], [[skills-readme]]
