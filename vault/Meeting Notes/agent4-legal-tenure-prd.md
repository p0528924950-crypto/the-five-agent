---
tags:
  - session
  - prd
  - agent
  - real-estate
---

# Agent 4: Legal & Tenure — PRD

## Overview

PRD and agent.md definition for Agent 4: Legal & Tenure. This is the most complex agent in the pipeline — it combines the expertise of a real estate appraiser and a legal expert in real estate and contracts, operating as a conservative risk manager for a financing body (bank).

**Files:**
- `the-five-agent/agent4-legal-tenure-prd.md` — full PRD
- `the-five-agent/.claude/agents/agent4-legal-tenure.md` — agent definition for Claude Code

**Chapter scope:**
- **7.0 המצב המשפטי והקנייני** — legal and proprietary status

**Output structure (two parts):**
- **Part A:** סיכום מובנה לחוות דעת שמאית — 7.1 executive summary + 7.2 Data Sheet (13-field table)
- **Part B:** ניתוח סיכונים — 7.3 Red Flags (🔴/🟡/🟢) + 7.4 Actionable Checklist

**Key characteristics:**
- **Persona:** Senior conservative professional — risk manager for a bank, not just a describer
- **Property classification:** First classifies property (מגורים/קרקע/מסחרי/ציבורי), then applies type-specific due diligence checklists
- **Cross-reference gate:** Compares נסח טאבו vs. חוזה מכר on area, attachments, owner, and encumbrances. Any contradiction → blocking flag to CEO
- **Mandatory disclaimer:** Every output ends with the professional liability disclaimer
- **Token efficiency:** Reads only from `the-five-agent/current_property_data/`

**Gold Standard reference:** Structure and conservative style based on completed Standard 19.0 appraisal for פרויקט "חצר הנביאים", רחוב מונבז 3, ירושלים.

## Open Questions

- האם Agent 4 מייצר פלט נפרד לכל מסמך (נסח, חוזה, תקנון) או פלט אחד משולב?
- מה הטיפול במקרה של חוזה מכר חסר — האם Agent 4 מנתח את הנסח בלבד?
- האם פרק 7.0 כולל גם ניתוח תקנון בית משותף, או שזה נפרד?

## Session Log

### 2026-04-27 — Initial PRD + agent.md created [shipped]

- **What was done:** Created full PRD specifying chapter 7.0 with two-part output structure (executive summary + data sheet / risk analysis + checklist). Created agent.md embedding the user's professional persona verbatim — conservative bank risk manager combining appraiser + legal expert. Implemented: property classification step (4 types, type-specific checklists), due diligence protocol (preliminary checks + contractual mechanisms + type-specific checks), cross-reference gate (נסח vs. חוזה on 4 data points), mandatory disclaimer as final element. Updated CEO agent.md: Agent 4 at position 5 in execution order, routing table (replaced old Legal/Regulatory Agent placeholder with Agent 4 keywords), contradiction gate (blocking flag on טאבו/contract mismatch), 7 VERIFY checks, data directory handoff, report assembly template (7.0 section).
- **Decisions:** Agent 4 replaces the old "Legal/Regulatory Agent" placeholder in the routing table — these are the same role. The cross-reference gate is CEO-level (not mid-agent like Agent 3's area check) because a contract/נסח contradiction is a transaction-level risk requiring user decision, not just a data accuracy issue. The mandatory disclaimer is enforced by the CEO's VERIFY step — if it's missing, the output is rejected.
- **Notes / Caveats:** Three open questions remain (see above). The `current_property_data/` directory needs to contain `contract.pdf` and `taba.pdf` at minimum for Agent 4 to function. If חוזה מכר is absent, Agent 4 should note this in 7.4 as a required verification task rather than halting.
- **Related:** [[ceo-agent-prd]], [[agent3-regulatory-permit-prd]], [[project-file-documentation]]
