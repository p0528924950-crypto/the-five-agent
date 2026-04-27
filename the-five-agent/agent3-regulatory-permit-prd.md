# PRD: Agent 3 — Regulatory & Permit

**Version:** 0.1 — Draft  
**Date:** 2026-04-27  
**Status:** In Progress

---

## 1. Overview

Agent 3: Regulatory & Permit produces chapters 5.0 and 6.0 of the Standard 19 appraisal — the statutory, planning, and licensing sections. These are the most legally sensitive chapters in the appraisal and require absolute precision: no rounding of areas, no personal interpretation, and explicit legal-cautious language throughout.

- **5.0 המצב התכנוני** — planning status: applicable תב"עות, zoning, rights table, development potential
- **6.0 רישוי ובנייה** — permits and licensing: permit history, תקן 9 area comparison, deviations, enforcement actions, completion certificates

**Token efficiency constraint:** Agent 3 reads source documents **only** from `the-five-agent/current_property_data/`. It must not scan other directories in the workspace.

**Cross-reference requirement:** Before writing chapter 6.2, Agent 3 compares permit areas (from היתר in `current_property_data/`) against Foundation Table שטח רשום (from נסח טאבו). Any discrepancy >1 מ"ר is reported to the CEO as a blocking flag before the pipeline continues.

**Gold Standard reference:** Structure and style based on completed Standard 19.0 appraisal for פרויקט "חצר הנביאים", רחוב מונבז 3, ירושלים; appraiser style: שי בריגה.

---

## 2. Goals

- Produce a legally sound, fact-based planning status chapter (5.0) with no invented zoning data
- Produce a complete permit history chapter (6.0) that explicitly flags any enforcement actions or deviations
- Enforce a "stop and flag" protocol: if critical documents are missing, halt and report before writing
- Cross-reference היתר areas vs. טאבו areas per תקן 9; surface any discrepancy >1 מ"ר to CEO
- Use legal-cautious phrasing throughout (e.g. "מבדיקה במערכת המידע ההנדסי עולה כי...")

---

## 3. Path Constraint (Token Efficiency)

**Agent 3 reads source documents exclusively from:**
```
the-five-agent/current_property_data/
```

Expected files in this directory:
| File | Content |
|---|---|
| `taba.pdf` / `taba.txt` | נסח טאבו — גוש, חלקה, שטח, זכויות |
| `tavit/*.pdf` | תב"ע תקנון and תשריטים |
| `heter_bniya.pdf` | היתר בנייה אחרון |
| `tovar_4.pdf` | טופס 4 / תעודת גמר |
| `enforcement/` | תיקי פיקוח / צווים (if any) |

Agent 3 must **not** scan `vault/`, `skills/`, `.claude/`, or any other workspace directory.

---

## 4. Flagging Protocol (Pre-Write Check)

Before writing any chapter text, Agent 3 checks for missing critical data. If any of the following are absent, it STOPS and outputs a `## מסמכים חסרים להשלמת השומה` block:

| Condition | Flag text |
|---|---|
| תיק פיקוח פתוח but no explanatory document | "תיק פיקוח [מספר] פתוח — נדרש מסמך המסביר מהות ההפרה" |
| No signed היתר תשריט matching site conditions | "לא נמצא תשריט היתר חתום התואם את מציאות השטח" |
| Building is occupied but no טופס 4 found | "הבניין מאוכלס אך לא אותר טופס 4 / תעודת גמר — נדרש אישור" |
| No תב"ע document found at all | "לא נמצאה תב"ע בתוקף — לא ניתן להשלים פרק 5.0" |

CEO receives this flag list and blocks the pipeline pending user resolution.

---

## 5. Chapter 5.0 — המצב התכנוני

### 5.1 Analysis Protocol

Agent 3 executes the following steps in order for chapter 5.0:

**א) איתור וזיהוי:** Identify all תב"עות applying to the parcel: plan number, name, publication date for validity.

**ב) היררכיה תכנונית:** State the planning jurisdiction and applicable master plan frameworks.

**ג) שימושים וייעודים:** Detail zoning changes and what is permitted at each level (sub-ground, ground floor, upper floors).

**ד) חילוץ זכויות:** Build the rights table with exact primary areas and service areas (above and below ±0.00).

**ה) צפיפות ובינוי:** Extract maximum permitted dwelling units and approved number of floors.

**ו) ניתוח מיצוי:** Compare actual construction (per היתר) against permitted rights; determine if future potential exists.

### 5.0 Required Output Sections

| Section | Content |
|---|---|
| **5.1 תב"עות בתוקף** | Plan number, status, publication date, planning authority |
| **5.1.1 ייעודי קרקע ושימושים** | Per-floor/level zoning breakdown |
| **טבלת זכויות בנייה** | Exact areas — primary and service, above and below ±0.00 |
| **הוראות בינוי** | Max floors, max dwelling units |
| **5.2 פוטנציאל תכנוני** | Conclusion on rights utilization |
| **5.3 סיכום המצב התכנוני** | Final statement on current use vs. zoning |

### 5.0 Precision Rules
- **No rounding:** Use exact figures from the תקנון
- **Transparency:** If one plan overrides another, state this explicitly
- **Factual baseline:** If no potential is found, write: "לא זוהה פוטנציאל תכנוני נוסף בעתיד הנראה לעין"

---

## 6. Chapter 6.0 — רישוי ובנייה

### 6.0 Analysis Protocol

**שלב 1: מיפוי היתרים** — Extract from engineering information systems the list of all building permits issued for the parcel: permit number, file number, issue date, nature.

**שלב 2: יצירת טבלת היתרים** — Consolidate into a table as it appears in the original appraisal.

**שלב 3: זיהוי הנכס בהיתר** — Find the specific apartment in the latest permit plan: apartment number, floor, level.

**שלב 4: בדיקת שטחים** — Compare property areas in the permit against תקן 9 (primary areas vs. service areas).

**שלב 5: בדיקת התאמה (critical)** — Cross-reference the permit plan against site visit notes and photos. Search for unauthorized additions, construction deviations, or significant interior changes.

**שלב 6: סטטוס משפטי-הנדסי** — Search for administrative orders, enforcement/violation files, dangerous structure declarations, and status of טופס 4 and completion certificate.

### 6.0 Required Output Sections

| Section | Content |
|---|---|
| **6.1 פירוט היתרי הבניה** | Professional opening paragraph + consolidated permit table |
| **6.2 פירוט שטחי הנכס** | תקן 9 area table per latest permit |
| **6.3 חריגות בנייה / אי התאמות** | Explicit statement on conformance; list any deviations |
| **6.5–6.6 הליכים וצווים** | Enforcement files, building violations, dangerous structure check |
| **6.7 טופס 4 / תעודת גמר** | Issue dates and certificate numbers |
| **6.8 זיהום קרקע** | Environmental hazards, non-conforming uses |
| **6.9 תשריט היתר הבנייה** | Reference to relevant permit plan sections |

### 6.0 Language Rules
- Use legal-cautious formulations: "מבדיקה במערכת המידע ההנדסי עולה כי..."
- Cite attorney names or clarification letters if presented regarding violations
- Use: "לא אותרו חריגות המשפיעות על הערך למטרת בטוחה" only if confirmed

---

## 7. Cross-Reference Protocol (תקן 9)

After reading both the היתר (from `current_property_data/`) and the Foundation Table:

1. Extract **שטח עיקרי** and **שטח שירות** from the permit
2. Compare against Foundation Table **שטח רשום** (from נסח טאבו)
3. Calculate delta: `|שטח היתר − שטח טאבו|`

**If delta > 1 מ"ר:**
```
🔴 חריגת שטח בין היתר לנסח טאבו
שטח בהיתר: [X] מ"ר | שטח בנסח: [Y] מ"ר | הפרש: [Z] מ"ר
נדרש אישור משתמש לפני המשך.
```

This report is passed to the CEO, which blocks the pipeline until the user resolves the discrepancy.

---

## 8. CEO Verification Checks

The CEO verifies Agent 3's output before proceeding:

| Check | Failure action |
|---|---|
| Section 5.1 present with ≥1 תב"ע identified | Block |
| Rights table present with exact figures (no placeholders) | Block |
| Section 6.1 permit table present with ≥1 row | Block |
| Section 6.2 contains explicit תקן 9 comparison | Block |
| Cross-reference report submitted (pass or flag) | Block if absent |
| No `[ערך]` placeholder text remaining in output | Block |

---

## 9. Open Questions

- האם סעיף 6.4 קיים ב-Gold Standard? (הספרור קופץ מ-6.3 ל-6.5)
- האם Agent 3 ניגש ל-APIs של מערכות המידע ההנדסי בזמן אמת, או רק לקבצים ב-`current_property_data/`?
- מה הטיפול ב-חריגת שטח שמשתמש בוחר להתעלם ממנה — האם נרשם בדוח הסופי?
