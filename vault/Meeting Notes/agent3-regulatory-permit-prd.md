---
tags:
  - session
  - prd
  - agent
  - real-estate
---

# Agent 3: Regulatory & Permit — PRD

## Overview

PRD and agent.md definition for Agent 3: Regulatory & Permit. This agent runs after Agent 2 (Physical & Environment) and produces chapters 5.0 and 6.0 — the most legally sensitive chapters of the Standard 19 appraisal.

**Files:**
- `the-five-agent/agent3-regulatory-permit-prd.md` — full PRD
- `the-five-agent/.claude/agents/agent3-regulatory-permit.md` — agent definition for Claude Code

**Chapter scope:**
- **5.0 המצב התכנוני** — 5.1 תב"עות בתוקף, 5.1.1 ייעודי קרקע, טבלת זכויות בנייה, הוראות בינוי, 5.2 פוטנציאל תכנוני, 5.3 סיכום
- **6.0 רישוי ובנייה** — 6.1 היתרים, 6.2 שטחי תקן 9, 6.3 חריגות, 6.5–6.6 הליכים וצווים, 6.7 טופס 4, 6.8 זיהום קרקע, 6.9 תשריט

**Key characteristics:**
- **Token efficiency:** reads only from `the-five-agent/current_property_data/` — no other directory scans
- **Flagging protocol:** halts before writing if critical documents are missing; presents CEO with a `מסמכים חסרים` list
- **Cross-reference gate:** compares היתר areas vs. Foundation Table שטח רשום (תקן 9); any delta >1 מ"ר triggers a blocking flag to CEO/user before chapter 6.2 is written
- **Style:** appraiser style of שי בריגה — legal-cautious language, no rounding, no personal interpretation

**Gold Standard reference:** Style derived from completed Standard 19.0 appraisal for פרויקט "חצר הנביאים", רחוב מונבז 3, ירושלים.

## Open Questions

- האם סעיף 6.4 קיים ב-Gold Standard? (הספרור קופץ מ-6.3 ל-6.5)
- האם Agent 3 ניגש ל-APIs של מערכות המידע ההנדסי בזמן אמת, או רק לקבצים ב-`current_property_data/`?
- מה הטיפול בחריגת שטח שמשתמש בוחר להתעלם ממנה — האם נרשמת בדוח הסופי?

## Session Log

### 2026-04-27 — Initial PRD + agent.md created [shipped]

- **What was done:** Created full PRD specifying chapters 5.0 and 6.0 with exact section lists. Created agent.md embedding both professional prompts verbatim as the core instruction sets (chapter 5.0 planning prompt + chapter 6.0 "שי בריגה" permit prompt). Implemented path constraint (`current_property_data/` only), flagging protocol (4 missing-document conditions), and cross-reference gate (תקן 9: היתר vs. טאבו, delta >1 מ"ר triggers block). Updated CEO agent.md: Agent 3 at position 4 in execution order, routing table (replaced old Planning Status Agent row), two new CEO gates (missing-documents gate + area-discrepancy gate), Agent 3-specific VERIFY checks (5 checks), data directory handoff, and report assembly template (5.0 + 6.0 sections).
- **Decisions:** Agent 3 is the only agent with a pre-write flagging step (Step 0) — it checks for missing documents before writing a single word. This is necessary because a legally incorrect planning/permit chapter is worse than a missing one. The cross-reference gate (תקן 9) runs between chapters 5.0 and 6.0 — it's a mid-agent pause, not a CEO-level pause, to keep the flow clean.
- **Notes / Caveats:** Section 6.4 gap (numbering jumps from 6.3 to 6.5) is an open question pending Gold Standard clarification. The `current_property_data/` directory does not yet exist — CEO or user must create it and populate it with the property's source documents before Agent 3 runs.
- **Related:** [[ceo-agent-prd]], [[agent2-physical-env-prd]], [[project-file-documentation]]
