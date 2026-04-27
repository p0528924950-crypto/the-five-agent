---
tags:
  - session
  - skill
  - install
---

# skill-creator Installation

## Overview

Installation of the official Anthropic `skill-creator` skill from the `anthropics/skills` GitHub repository. This skill enables creating, iterating, and evaluating new Claude Code skills through a structured draft → test → review → improve loop, with quantitative benchmarking and blind comparison capabilities.

**Source:** https://github.com/anthropics/skills/tree/main/skills/skill-creator
**Installed at:** `the-five-agent/skills/skill-creator/`
**Active as:** `/skill-creator` (via `.claude/commands/skill-creator.md`)

## Open Questions

- The `assets/`, `eval-viewer/`, and `scripts/` directories were not installed — they contain Python scripts needed for benchmarking and the eval viewer. Install them if the full eval pipeline is needed.

## Session Log

### 2026-04-27 — Installed skill-creator from Anthropic GitHub [shipped]

- **What was done:** Downloaded SKILL.md + 3 agent files (analyzer, comparator, grader) + references/schemas.md from the official Anthropics skills repo via PowerShell. Created the full directory structure at `skills/skill-creator/`. Copied SKILL.md to `.claude/commands/skill-creator.md` to activate as slash command.
- **Decisions:** Installed only the markdown files (SKILL.md, agents/, references/). The Python scripts in `scripts/`, `eval-viewer/`, and `assets/` were not installed because they require a Python environment and are only needed for the advanced quantitative benchmarking pipeline — the core skill creation workflow works without them.
- **Notes / Caveats:** The `eval-viewer/generate_review.py` script referenced in SKILL.md won't work until the `eval-viewer/` and `scripts/` directories are installed from the repo. The skill will still function for the manual/qualitative workflow.
- **Related:** [[skills-readme]], [[claude-commands-example]], [[skill-obsidian-vault-workflow]]
