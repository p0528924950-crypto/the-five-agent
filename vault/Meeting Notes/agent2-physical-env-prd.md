---
tags:
  - session
  - prd
  - agent
  - real-estate
---

# Agent 2: Physical & Environment Description — PRD

## Overview

PRD and agent.md definition for Agent 2: Physical & Environment Description. This agent runs after Agent 1 (Setup & ID) and produces chapter 4.0 of the Standard 19 appraisal — the combined physical and environmental description section.

**Files:**
- `the-five-agent/agent2-physical-env-prd.md` — full PRD
- `the-five-agent/.claude/agents/agent2-physical-env.md` — agent definition for Claude Code

**Chapter scope:**
- **4.1 תיאור הסביבה** — 8 mandatory sub-sections: מיקום וגבולות, אופי הבינוי, חתך דמוגרפי, תשתיות ומוסדות, תחבורה ונגישות, שטחים פתוחים, סטטוס תכנוני ופיתוח, מצוקת חניה
- **4.4 תיאור הבניין** — physical building characteristics from site visit
- **4.5 תיאור הדירה** — individual unit characteristics from Foundation Table + site visit

**Key characteristic:** Agent 2 is the only chapter agent with explicit web search permission — used for environment research in 4.1. Foundation Table facts (שטח, גוש, חלקה, זכויות) remain locked.

**Gold Standard reference:** Structure derived from completed Standard 19.0 appraisal for פרויקט "חצר הנביאים", רחוב מונבז 3, דירה 101, ירושלים.

## Open Questions

- האם סעיפים 4.2 ו-4.3 קיימים ב-Gold Standard, או שהספרור קופץ מ-4.1 ל-4.4?
- האם Agent 2 מבצע חיפוש אינטרנטי אוטונומי, או שהמשתמש מספק נתוני סביבה?
- מה רמת הפירוט הנדרשת בסעיף 4.5 — פסקת תיאור רצוף, או טבלה?

## Session Log

### 2026-04-27 — Initial PRD + agent.md created [shipped]

- **What was done:** Created full PRD for Agent 2 covering 4.1 (8 mandatory environment sub-sections with professional appraisal terminology requirement), 4.4 (building description), and 4.5 (unit description). Created agent.md with the user-provided professional prompt as the core instruction set for 4.1, extended with 4.4 and 4.5 protocols. Updated CEO agent.md: execution order (Agent 2 at position 3 replacing the old separate Property Description and Environment Description agents), Agent 2 handoff contract (address + project name extracted from Agent 1 chapter 1.0), Agent 2-specific VERIFY checks (8 sub-sections in 4.1, שטח match in 4.5, הצמדות match in 4.5), web search exception in Data Consistency Rule, and updated report assembly template.
- **Decisions:** Agent 2 consolidates what was previously split into two agents (Property Description + Environment Description) into a single chapter 4.0 agent. The web search exception is explicitly scoped to neighborhood/environment facts only — Foundation Table values cannot be overridden. The professional prompt provided by the user was embedded verbatim as the core 4.1 instruction set inside the agent.md.
- **Notes / Caveats:** The chapter numbering gap (4.2, 4.3 not defined) is an open question — waiting for Gold Standard clarification. Section 4.5 output format is prose, not a table, following Gold Standard convention.
- **Related:** [[ceo-agent-prd]], [[agent1-setup-id-prd]], [[project-file-documentation]]
