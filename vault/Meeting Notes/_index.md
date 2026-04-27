# Meeting Notes — Index

Architecture, code, and session documentation for the-five-agent project.

**מצב מערכת:** ✅ Final Build — מוכנה להרצה (2026-04-27)

## Pipeline Architecture

```
Research Agent
    ↓ טבלת נתוני יסוד
Agent 1: Setup & ID          → נתוני_בסיס_וזיהוי/        (פרקים 1.0, 2.0, 3.0)
    ↓
Agent 2: Physical & Env      → תיאור_פיזי_וסביבה/         (פרקים 4.1, 4.4, 4.5)
    ↓
Agent 3: Regulatory & Permit → מצב_תכנוני_ורישוי/          (פרקים 5.0, 6.0)
    ↓
Agent 4: Legal & Tenure      → מצב_משפטי_וקנייני/          (פרק 7.0)
    ↓
Agent 5: Market & Valuation  → ניתוח_שוק_ותחשיבים/         (פרקים 8.0, 9.0, 10.0)
    ↓
Agent 6: Factors & Consid.   → סיכום_ובקרת_איכות/          (פרק 11.0 — synthesis only)
    ↓
QC Agent                     → סיכום_ובקרת_איכות/          (בקרת עקביות רוחבית)
    ↓
Final Report (Markdown)
```

## Topics

- [[claude-md]] — Project guidance file that Claude Code reads at the start of every session
- [[gitignore]] — Git ignore configuration for the repository
- [[claude-settings]] — Project-level Claude Code permissions and hooks (shared via git)
- [[claude-settings-local]] — Personal local Claude Code settings (gitignored)
- [[claude-commands-example]] — Template for custom slash commands in .claude/commands/
- [[claude-agents-example]] — Template for sub-agent definitions in .claude/agents/
- [[skills-readme]] — Overview of the skills/ directory for developing custom commands
- [[skill-obsidian-bases]] — Skill for creating Obsidian Bases (.base files)
- [[skill-obsidian-markdown]] — Skill for Obsidian Flavored Markdown syntax
- [[skill-obsidian-vault-workflow]] — Core vault read/write protocol skill (mandatory on every task)
- [[project-file-documentation]] — Session log for initial documentation of all project files
- [[ceo-agent-prd]] — PRD + agent.md for the CEO orchestrator agent (Standard 19 real estate appraisal system)
- [[skill-creator-install]] — Installation of Anthropic's official skill-creator skill from GitHub
- [[agent1-setup-id-prd]] — PRD + agent.md for Agent 1: Setup & ID (chapters 1.0, 2.0, 3.0)
- [[agent2-physical-env-prd]] — PRD + agent.md for Agent 2: Physical & Environment (chapters 4.1, 4.4, 4.5)
- [[agent3-regulatory-permit-prd]] — PRD + agent.md for Agent 3: Regulatory & Permit (chapters 5.0 + 6.0)
- [[agent4-legal-tenure-prd]] — PRD + agent.md for Agent 4: Legal & Tenure (chapter 7.0)
- [[agent5-market-valuation-prd]] — PRD + agent.md for Agent 5: Market & Valuation (chapters 8.0, 9.0, 10.0)
- [[agent6-factors-considerations-prd]] — PRD + agent.md for Agent 6: Factors & Considerations (chapter 11.0)
