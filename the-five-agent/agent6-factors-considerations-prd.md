# PRD: Agent 6 — Factors & Considerations

**Version:** 0.1 — Draft  
**Date:** 2026-04-27  
**Status:** In Progress

---

## 1. Overview

Agent 6: Factors & Considerations produces chapter 11.0 of the Standard 19 appraisal — the analytical synthesis chapter that connects all prior findings into a coherent, professionally argued narrative. It is the penultimate chapter before the QC agent, and its purpose is to explain *why* the property is worth what Agent 5 determined.

Agent 6 is a **synthesizer**, not a data gatherer. It receives no raw documents — only the verified outputs of all prior agents. Its output is flowing professional Hebrew prose, divided into sub-sections per the Gold Standard chapter 11 structure.

**Handoff contract:** The CEO passes to Agent 6:
- Agent 4's red flags (section 7.3) — legal risks and encumbrances
- Agent 5's market conclusion (section 9.4) and valuation highlights (sections 10.2–10.3)
- All other prior verified chapter outputs as context

**Gold Standard reference:** Structure based on chapter 11 of the completed Standard 19.0 appraisal for פרויקט "חצר הנביאים", רחוב מונבז 3, ירושלים.

---

## 2. Goals

- Synthesize all prior agent outputs into a unified, logically consistent factors chapter
- Explicitly list and weigh positive factors (value enhancers) against negative factors (risks/discounts)
- Justify the chosen appraisal method and the key adjustment coefficients Agent 5 applied
- Flag uncertainty factors that could affect value going forward
- Conclude with a narrative rationale that supports the final value stated in chapter 10.0

---

## 3. No Path Constraint — Synthesis Agent

Agent 6 **does not read files from disk**. It works exclusively from:
- Prior verified chapter outputs passed by the CEO
- Specifically: Agent 4 section 7.3 (Red Flags) + Agent 5 sections 9.4 + 10.2 + 10.3

No directory access required. This is the most token-efficient agent in the pipeline.

---

## 4. Input Contract — Data from CEO

The CEO passes the following to Agent 6:

| Input | Source | Specific Section |
|---|---|---|
| Legal Red Flags | Agent 4 output | Section 7.3 (🔴/🟡/🟢 list) |
| Market conclusion | Agent 5 output | Section 9.4 |
| Comparison adjustments | Agent 5 output | Section 10.2 (adjustment table) |
| Value derivation | Agent 5 output | Section 10.3 (weighted average) |
| Final value | Agent 5 output | Section 10.5 |
| Physical parameters | Agent 2 output | Sections 4.4 + 4.5 |
| Planning status | Agent 3 output | Sections 5.2 + 5.3 |
| All prior chapter summaries | All agents | Key findings only |

Agent 6 synthesizes this data — it does NOT perform new lookups or re-analyze source documents.

---

## 5. Chapter 11.0 Structure — Gold Standard Pattern

### 5.1 Required Sub-sections

**11.1 — גורמים חיוביים (Value Enhancers)**

List and explain each positive factor affecting the property's value. Examples:
- מיקום ונגישות (proximity to light rail, urban center, amenities)
- מאפיינים פיזיים (floor level, orientation, מרפסת, parking — from Agent 2)
- סביבה (neighborhood quality, competing projects status — from Agent 2)
- מצב תכנוני חיובי (unused development potential, favorable zoning — from Agent 3)
- שוק (high demand environment, rising prices — from Agent 5)
- משפטי (clear title, no encumbrances — from Agent 4, if clean)

**11.2 — גורמים שליליים וסיכונים (Value Detractors & Risks)**

List and explain each negative factor or risk:
- מגבלות משפטיות (🔴/🟡 Red Flags from Agent 4: leasehold terms, encumbrances, enforcement proceedings)
- מגבלות פיזיות (floor, view obstruction, aging building — from Agent 2)
- מגבלות תכנוניות (building deviations, rights fully utilized — from Agent 3)
- שוק (market cooling signs, competing supply — from Agent 5)
- אי-ודאות (pending plans, open enforcement files)

**11.3 — נימוק שיטת השומה**

Explain why the chosen method (from Agent 5 chapter 8.0) is appropriate for this property:
- Why שיטת ההשוואה was selected (or income/cost if used)
- Why the specific comparables were chosen and what makes them most similar
- Justification for the main adjustment coefficients applied (time, floor, rights, condition)

**11.4 — הסבר על ההתאמות העיקריות**

Narrative explanation of the most significant adjustments from Agent 5's comparison table:
- Quantify the most material adjustments and explain their rationale
- If a leasehold discount was applied (Agent 5 section 10.4): explain the methodology and percentage
- Cross-reference to Foundation Table values that anchored the calculation

**11.5 — גורמי אי-ודאות**

Document factors that could affect value beyond the valuation date:
- תכניות בהפקדה (plans in deposit) that could change zoning
- הליכים משפטיים תלויים ועומדים (pending legal proceedings from Agent 4)
- שינויי שוק (market interest rate trajectory, monetary policy)
- תלויות תכנוניות (pending municipal decisions)

If no material uncertainties exist: "לא זוהו גורמי אי-ודאות מהותיים המשפיעים על השווי."

**11.6 — מסקנה: נימוק לשווי**

A closing paragraph that ties the chapter together:
- Summarize the balance of positive vs. negative factors
- State the final value from Agent 5 as the justified conclusion of this analysis
- Confirm consistency with the market evidence presented

---

## 6. Style Requirements

| Requirement | Detail |
|---|---|
| Language | Continuous Hebrew prose — NOT bullet lists in the final output |
| Tone | Senior appraiser: authoritative, balanced, professionally argued |
| Structure | Sub-section headers per Gold Standard pattern |
| Length | 11.1–11.4: 2–4 paragraphs each; 11.5: 1–2 paragraphs; 11.6: 1 paragraph |
| Citations | Reference specific prior chapter sections ("כמפורט בפרק 7.3", "כאמור בפרק 9.4") |
| Consistency | All values and facts must match prior agent outputs exactly |

**Prohibited:**
- Introducing new facts not present in prior agent outputs
- Contradicting values stated by prior agents
- Using bullet lists as the primary output format (headers + prose only)

---

## 7. CEO Verification Checks

| Check | Failure action |
|---|---|
| All 6 sub-sections (11.1–11.6) present | Block |
| Section 11.1 references ≥3 positive factors | Block |
| Section 11.2 references ≥1 factor from Agent 4 Red Flags | Block if Agent 4 had red flags |
| Section 11.3 names the appraisal method (matches Agent 5 chapter 8.0) | Block |
| Section 11.4 explains ≥2 adjustment coefficients from Agent 5 | Block |
| Section 11.6 states the final value (matches Agent 5 section 10.5) | Block on mismatch |
| No new facts introduced that weren't in prior agent outputs | Flag for review |
| Output is prose, not bullet lists | Flag for review |

---

## 8. Open Questions

- כמה גורמים חיוביים ושליליים נדרשים מינימום לפי ה-Gold Standard?
- האם פרק 11 מחולק לנקודות בשומת ה-Gold Standard, או שהוא פרוזה רצופה בלבד?
- האם סעיף 11.5 (אי-ודאות) קיים ב-Gold Standard, או שהוא מוטמע בסעיפים אחרים?
