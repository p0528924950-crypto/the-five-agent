# PRD: Agent 2 — Physical & Environment Description

**Version:** 0.1 — Draft  
**Date:** 2026-04-27  
**Status:** In Progress

---

## 1. Overview

Agent 2: Physical & Environment Description produces chapter 4.0 of the Standard 19 appraisal — the combined physical and environmental description section. It covers three sub-chapters:

- **4.1 תיאור הסביבה** — neighborhood context, demographics, infrastructure, planning status
- **4.4 תיאור הבניין** — physical building characteristics
- **4.5 תיאור הדירה** — individual unit characteristics

Agent 2 runs after Agent 1 (Setup & ID) and receives the property address, project name, and Foundation Data Table from the CEO. It is the first agent that actively uses web search tools to gather real-world data — specifically for the environment description in 4.1.

**Gold Standard reference:** Structure derived from the completed Standard 19.0 appraisal for פרויקט "חצר הנביאים", רחוב מונבז 3, דירה 101, ירושלים.

---

## 2. Goals

- Write a factually accurate neighborhood environment description (4.1) using real web-sourced data — no fabricated street names, institutions, or projects
- Describe the building and apartment unit (4.4, 4.5) from site visit data and Foundation Table
- Use professional appraisal terminology (טרמינולוגיה שמאית)
- Output Markdown that drops directly into the final report
- Flag any missing field with `[חסר — נדרש השלמה]`

---

## 3. Inputs

The CEO provides Agent 2 with:

| Input | Source | Required |
|---|---|---|
| Foundation Data Table (טבלת נתוני יסוד) | Research Agent | Yes |
| כתובת מלאה (רחוב, מספר, עיר) | Foundation Table / Agent 1 output | Yes |
| שם הפרויקט | Agent 1 output (section 1.0) | Recommended |
| גוש / חלקה / תת-חלקה | Foundation Table | Yes |
| שטח דירה (מ"ר) | Foundation Table | Yes |
| הצמדות (חניה, מחסן, גינה) | Foundation Table / Agent 1 output | Yes |
| מספר חדרים | User input / site visit | Yes |
| קומה | User input / site visit | Yes |
| פרטי ביקור בנכס | Agent 1 output (section 2.4) | Yes |
| מצב הדירה והגימורים | User input / site visit | Yes |
| שנת בנייה / מאפייני מבנה | User input / site visit | Yes |

---

## 4. Output — Three Sub-chapters

### 4.1 תיאור הסביבה

Agent 2 writes a professional environment description using real web-sourced data. **Eight required sub-sections:**

1. **מיקום וגבולות** — exact location of the property and neighborhood; bordering areas/streets
2. **אופי הבינוי** — building types: historic/institutional/new urban renewal projects
3. **חתך דמוגרפי** — population profile (secular/religious/ultra-orthodox, foreign residents, students)
4. **תשתיות ומוסדות** — education, religion, health, commercial/retail nearby
5. **תחבורה ונגישות** — main traffic routes, light rail/bus proximity, walking distances to points of interest
6. **שטחים פתוחים** — parks, gardens, public squares nearby
7. **סטטוס תכנוני ופיתוח** — municipal planning policy (e.g. densification along transit corridors), competing projects under construction or planning
8. **מצוקת חניה** — daytime/nighttime parking assessment

**Data requirement:** All facts sourced from maps, municipal websites, and local real estate news. No fabrication.

### 4.4 תיאור הבניין

Physical building description from site visit and user input:

| Field | Source |
|---|---|
| שנת בנייה / גיל הבניין | User input |
| מספר קומות | User input |
| מספר יחידות דיור | User input |
| חומרי בנייה | User input (בטון / לבנה / אחר) |
| מצב תחזוקה | Site visit (טוב / בינוני / ירוד) |
| מעלית | Yes/No |
| ממ"ד בבניין | Yes/No |
| חנייה (מספר מקומות, סוג) | User input |
| שטחים משותפים / גינה | User input |
| שיפוצים / התחדשות עירונית | תמ"א 38 / פינוי-בינוי — status |

### 4.5 תיאור הדירה

Individual unit description:

| Field | Source |
|---|---|
| קומה | Foundation Table / User input |
| כיווני אוויר | Site visit |
| מספר חדרים | User input |
| שטח עיקרי (מ"ר) | Foundation Table |
| שטח שירות (מ"ר) | Foundation Table / User input |
| ממ"ד | Yes/No + מ"ר |
| מרפסת | Yes/No + מ"ר + סוג |
| חנייה צמודה | Yes/No (from הצמדות) |
| מחסן | Yes/No (from הצמדות) |
| מצב הדירה | חדשה / משופצת / ישנה / דרוש שיפוץ |
| גימורים | סטנדרטי / יוקרתי / ישן |
| הערות מיוחדות | Any notable features from site visit |

---

## 5. Professional Terminology Requirements

Agent 2 must use the following appraisal terms where appropriate:

| Term | Context |
|---|---|
| בינוי רווי | Dense residential/commercial area |
| עירוב שימושים | Mixed-use zoning |
| ציר עורקי | Main arterial road |
| מע"ר (מרכז עירוני ראשי) | Primary urban center designation |
| התחדשות עירונית | Urban renewal |
| ציפוף | Densification policy |
| קרבת-רכבת קלה | Light rail proximity (added value factor) |

---

## 6. Constraints

- Section 4.1: **must not fabricate** street names, institutions, or project names — use web search tools
- Sections 4.4 and 4.5: **must not override** Foundation Table values for area, gush/helka, or rights
- All three sections must be written in formal Hebrew
- Chapter headings must exactly match Gold Standard Hebrew headers

---

## 7. CEO Handoff Contract

The CEO passes to Agent 2:
- Foundation Table (read-only)
- כתובת מלאה + שם הפרויקט extracted from Agent 1's chapter 1.0 output
- Site visit details from Agent 1's chapter 2.4 output

The CEO verifies Agent 2's output:

| Check | Failure action |
|---|---|
| All 8 sub-sections of 4.1 present | Block, report missing sections |
| 4.1 contains no fabricated names (basic plausibility check) | Flag for user review |
| 4.4 all required fields populated | Block if more than 2 are `[חסר]` |
| 4.5 שטח and הצמדות match Foundation Table | Block on mismatch |

---

## 8. Open Questions

- האם סעיף 4.2 ו-4.3 קיימים ב-Gold Standard, או שהספרור קופץ מ-4.1 ל-4.4?
- האם Agent 2 אמור לבצע חיפוש אינטרנטי אוטונומי, או שהמשתמש מספק את נתוני הסביבה?
- מה רמת הפירוט הנדרשת בסעיף 4.5 — פסקת תיאור רצוף, או טבלה?
