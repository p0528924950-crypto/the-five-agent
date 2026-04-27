---
tags:
  - session
  - prd
  - agent
  - real-estate
---

# Agent 6: Factors & Considerations — PRD

## Overview

PRD and agent.md definition for Agent 6: Factors & Considerations. This is the synthesis chapter of the pipeline — it connects all prior findings into a coherent, professionally argued narrative. It runs after Agent 5 and before QC.

**Files:**
- `the-five-agent/agent6-factors-considerations-prd.md` — full PRD
- `the-five-agent/.claude/agents/agent6-factors-considerations.md` — agent definition for Claude Code

**Chapter scope:**
- **11.0 גורמים ושיקולים לעריכת השומה** — 6 sub-sections:
  - 11.1 גורמים חיוביים (≥3 positive value-enhancing factors)
  - 11.2 גורמים שליליים וסיכונים (must cite Agent 4 section 7.3 red flags)
  - 11.3 נימוק שיטת השומה (method justification — must match Agent 5 chapter 8.0)
  - 11.4 הסבר על ההתאמות העיקריות (≥2 adjustment coefficients from Agent 5 section 10.2)
  - 11.5 גורמי אי-ודאות (forward-looking risk factors)
  - 11.6 מסקנה — must state final value exactly as Agent 5 section 10.5

**Key characteristics:**
- **Synthesis-only:** no file access — works exclusively from prior verified outputs passed by CEO
- **Prose output:** all sub-sections must be continuous Hebrew paragraphs (no bullet lists)
- **Citation discipline:** every material claim must explicitly reference its source chapter
- **Value lock:** final value in 11.6 must match Agent 5 section 10.5 to the shekel
- **Token efficiency:** most efficient agent in the pipeline (no disk reads)

**Gold Standard reference:** Chapter 11 of completed Standard 19.0 appraisal for פרויקט "חצר הנביאים", רחוב מונבז 3, ירושלים.

## Input Contract (from CEO)

| Input | Source | Specific Section |
|---|---|---|
| Legal Red Flags | Agent 4 output | Section 7.3 (🔴/🟡/🟢 list) |
| Market conclusion | Agent 5 output | Section 9.4 |
| Comparison adjustments | Agent 5 output | Section 10.2 (adjustment table) |
| Value derivation | Agent 5 output | Section 10.3 (weighted average) |
| Final value | Agent 5 output | Section 10.5 |
| Physical parameters | Agent 2 output | Sections 4.4 + 4.5 |
| Planning status + potential | Agent 3 output | Sections 5.2 + 5.3 |

## Open Questions

- כמה גורמים חיוביים ושליליים נדרשים מינימום לפי ה-Gold Standard?
- האם פרק 11 מחולק לנקודות בשומת ה-Gold Standard, או שהוא פרוזה רצופה בלבד?
- האם סעיף 11.5 (אי-ודאות) קיים ב-Gold Standard, או שהוא מוטמע בסעיפים אחרים?

## Session Log

### 2026-04-27 — PRD + agent.md created, CEO updated, vault synced [shipped]

- **What was done:** Created full PRD and agent.md for the synthesis chapter. Chapter 11.0 has 6 sub-sections (11.1–11.6) in flowing Hebrew prose. Agent 6 is the only agent in the pipeline with no disk access — it receives all data from CEO. CEO updated: execution order position 7, Agent 6 handoff block (no-disk note + input list), 8 VERIFY checks, routing table updated, report assembly block updated (stale Planning/Market placeholder sections removed, replaced with `## 11.0 גורמים ושיקולים`).
- **Decisions:** Agent 6 deliberately has no tool access — it is the most token-efficient agent in the pipeline. The synthesis constraint (no new facts) is enforced both by the agent's persona instructions and by the CEO's VERIFY checks. The final value lock (11.6 must match Agent 5 section 10.5 exactly) is a hard block in CEO verification.
- **Notes / Caveats:** Quality of Agent 6 output is entirely dependent on the quality of prior agent outputs. If Agent 5's comparison table is thin (e.g., only 3 transactions), Agent 6 will have limited material to explain in section 11.4. Consider instructing CEO to flag this condition before spawning Agent 6.
- **Related:** [[ceo-agent-prd]], [[agent5-market-valuation-prd]], [[agent4-legal-tenure-prd]]
