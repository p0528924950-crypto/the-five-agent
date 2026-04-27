---
tags:
  - session
  - prd
  - agent
  - real-estate
---

# Agent 5: Market & Valuation — PRD

## Overview

PRD and agent.md definition for Agent 5: Market & Valuation. This is the economic core of the pipeline — it produces the final property value, which is the primary deliverable of the entire Standard 19 appraisal.

**Files:**
- `the-five-agent/agent5-market-valuation-prd.md` — full PRD
- `the-five-agent/.claude/agents/agent5-market-valuation.md` — agent definition for Claude Code

**Chapter scope:**
- **8.0 עקרונות השומה** — appraisal method, basis of value, date, assumptions, תקן 9 declaration
- **9.0 המצב הכלכלי והשוק** — 9.1 macro, 9.2 local market, 9.3 competing projects, 9.4 market conclusion
- **10.0 תחשיב השווי** — 10.1 equivalent area table (תקן 9), 10.2 comparison transactions + adjustments, 10.3 value derivation, 10.4 leasehold discount (conditional), 10.5 final value

**Key characteristics:**
- **Data sync:** Receives physical data from Agent 2 (4.4 + 4.5) and legal constraints from Agent 4 (7.0) — does not re-read source documents
- **תקן 9 coefficients:** Primary 1.00 | ממ"ד 1.00 | מרפסת שמש 0.35 | מרפסת מקורה 0.50 | מרפסת שירות 0.25 | חניה תת-קרקעית 0.30 | חניה חיצונית 0.20 | מחסן 0.25
- **Comparison adjustments:** Time factor, floor, view, rights status, condition, attachments — each documented explicitly with %
- **Leasehold trigger:** If Agent 4 reported capitalized/fixed-term lease → section 10.4 with discount methodology
- **Rounding rule:** Final value rounded to nearest ₪5,000; never a perfectly round million
- **Token efficiency:** Market data read only from `the-five-agent/current_property_data/`

**Gold Standard reference:** Methodology based on completed appraisal for פרויקט "חצר הנביאים", ירושלים (value: ₪5,460,000).

## Open Questions

- מה שיעור ההפחתה המדויק לחכירה מהוונת עד 2110 — לפי מודל ה-Gold Standard?
- כמה עסקאות השוואה נדרשות מינימום (3 או 5)?
- האם נדרשת גישת הכנסה כבדיקה נגדית, או שגישת ההשוואה מספיקה לדירת מגורים?
- האם Agent 5 מייצר ניתוח רגישות (sensitivity analysis) לטווח שווי?

## Session Log

### 2026-04-27 — Initial PRD + agent.md created [shipped]

- **What was done:** Created full PRD and agent.md for the economic core of the pipeline. Chapter 8.0: method declaration + assumptions. Chapter 9.0: 4 sub-sections (macro, local, competing projects, conclusion). Chapter 10.0: full תקן 9 equivalent area table with 8 component types and standard coefficients, comparison transaction table with 6 documented adjustment categories, weighted average derivation, conditional leasehold discount (section 10.4, triggered by Agent 4 output), and final value in numbers + words. CEO update: Agent 5 at position 6, routing table, data-sync handoff explicitly naming Agent 2 + Agent 4 outputs as inputs, lease trigger flag from Agent 4 to Agent 5, 8 VERIFY checks, report assembly template (8.0/9.0/10.0 sections).
- **Decisions:** Agent 5 is the only agent that does not read raw source documents — it consumes prior agents' verified outputs. This is a deliberate design choice: the physical and legal facts are locked by Agents 2 and 4; Agent 5's job is to value, not re-verify. The leasehold trigger is CEO-level (CEO flags to Agent 5) rather than Agent 5 detecting it autonomously, to keep the audit trail explicit.
- **Notes / Caveats:** The `current_property_data/transactions.xlsx` file must exist and contain recent comparable transactions from the area for Agent 5 to produce a valid chapter 10. Without it, the agent can describe the market (chapter 9) but cannot complete the valuation (chapter 10).
- **Related:** [[ceo-agent-prd]], [[agent4-legal-tenure-prd]], [[agent2-physical-env-prd]], [[project-file-documentation]]
