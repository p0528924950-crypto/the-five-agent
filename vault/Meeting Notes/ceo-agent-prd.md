---
tags:
  - session
  - prd
  - agent
  - real-estate
---

# CEO Agent PRD

## Overview

PRD and agent.md definition for the CEO orchestrator agent of the Standard 19 real estate appraisal system. The CEO is the single entry point for all appraisal work — it routes tasks to 8 specialized chapter agents, enforces a Foundation Data Table gate (טבלת נתוני יסוד) as a single source of truth, and assembles the final report. The Research Agent runs first and is a hard prerequisite for all chapter agents.

**Files:**
- `the-five-agent/ceo-agent-prd.md` — full PRD
- `the-five-agent/.claude/agents/ceo-agent.md` — agent definition for Claude Code

## Open Questions

- Is the QC Agent blocking (must pass) or advisory (report + continue)?
- Output format: single MD file, per-chapter files, or both?
- How does the CEO handle a partially failed chapter agent?
- Fallback if GovMap / רשות המיסים APIs are unavailable?
- Does Research Agent access APIs in real-time or only works on user-uploaded PDFs?

## Session Log

### 2026-04-27 — Upgraded to Supervisor model (v0.2) [shipped]

- **What was done:** Rewrote CEO PRD to v0.2 and updated `ceo-agent.md` to implement the Supervisor (מפקח עבודה) model. The CEO now runs agents strictly sequentially, verifies each output via a SPAWN→VERIFY→GATE→PROCEED loop, and maintains an audit trail. Added per-agent verification gate (4 checks), error recovery dialog (3 user options), and audit log format. Added Agent 1: Setup & ID to the routing table and execution order. Sub-agents inventory updated: Agent 1 now "In Progress".
- **Decisions:** The CEO is no longer a passive router — it actively inspects every chapter output before the pipeline proceeds. Contradictions with the Foundation Table cause a hard block. The user always chooses the recovery path (re-run / correct / skip) rather than the CEO deciding autonomously.
- **Notes / Caveats:** The 3-option recovery dialog was designed so the CEO never silently swallows a bad output. The "skip" option marks the section `[חסר]` in the final report, making gaps visible rather than hidden.
- **Related:** [[agent1-setup-id-prd]], [[claude-md]], [[project-file-documentation]]

### 2026-04-27 — Initial PRD + agent.md created [shipped]

- **What was done:** Created full PRD covering: input spec, keyword routing table, Standard 19 execution order, Research Agent enhanced spec (Hebrew PDF ingestion, 4 Israeli data sources, טבלת נתוני יסוד schema), CEO workflow controls (gate check, data consistency rule, QC validation), and sub-agents inventory. Created agent.md with full orchestration protocol in `.claude/agents/`.
- **Decisions:** Research Agent is a hard gate — no chapter agent starts without a complete Foundation Data Table. All chapter agents read from the table only; no independent lookups allowed. This prevents data contradictions across appraisal sections.
- **Notes / Caveats:** 8 sub-agents planned but none implemented yet. The `ceo_agent.md` stub at `.claude/ceo_agent.md` was left in place; the real definition is in `.claude/agents/ceo-agent.md`. CLAUDE.md already instructs loading the CEO agent always.
- **Related:** [[claude-md]], [[claude-agents-example]], [[project-file-documentation]]
