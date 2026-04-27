# PRD: Agent 4 — Legal & Tenure

**Version:** 0.1 — Draft  
**Date:** 2026-04-27  
**Status:** In Progress

---

## 1. Overview

Agent 4: Legal & Tenure produces chapter 7.0 of the Standard 19 appraisal — the legal and proprietary status section. This is the most complex agent in the pipeline, combining the expertise of an experienced real estate appraiser with a legal specialist in real estate and contracts.

Agent 4 operates as a **conservative risk manager for a financing body (bank)**. Its output is structured in two parts:
- **Part A:** Structured summary for the appraisal opinion (executive summary + data sheet)
- **Part B:** Risk analysis and professional recommendations (red flags + actionable checklist for the appraiser)

The agent classifies the property type first, then applies the relevant due diligence checklist. Every response ends with a mandatory professional disclaimer.

**Token efficiency constraint:** Reads source documents **only** from `the-five-agent/current_property_data/`.

**Cross-reference requirement:** Compares טאבו data (area, attachments/הצמדות) against contract data. Reports contradictions to CEO as a blocking flag.

**Gold Standard reference:** Structure and style based on completed Standard 19.0 appraisal for פרויקט "חצר הנביאים", רחוב מונבז 3, ירושלים.

---

## 2. Goals

- Produce a legally rigorous chapter 7.0 that surfaces every material legal risk to the financing bank
- Classify the property type and apply the appropriate due diligence checklist
- Identify and flag all הערות אזהרה, עיקולים, שעבודים, and rights encumbrances from the נסח טאבו
- Cross-reference טאבו data vs. purchase contract; block pipeline on contradictions
- Always end with the mandatory professional disclaimer

---

## 3. Path Constraint (Token Efficiency)

**Agent 4 reads source documents exclusively from:**
```
the-five-agent/current_property_data/
```

Expected files:
| File | Content |
|---|---|
| `taba.pdf` / `taba.txt` | נסח טאבו — area, rights, encumbrances, warnings |
| `contract.pdf` | חוזה מכר / הסכם רכישה |
| `rights_cert.pdf` | אישור זכויות |
| `takanon.pdf` | תקנון הבית המשותף |
| `va'ad_bait/` | אישורי ועד בית / עמידה בתשלומים |

Agent 4 must **not** scan any other directory.

---

## 4. Property Classification

Before any analysis, Agent 4 classifies the property into one of:

| Type | Hebrew | Applicable Checklist |
|---|---|---|
| Residential | מגורים (דירה/בית) | הצמדות, בדק בית, ועד בית, היטל השבחה |
| Land | קרקע / מגרש | זיקות הנאה, הסכמי שיתוף, ייעוד |
| Commercial | מסחרי | הסכמי שכירות, מע"מ, עסק חי |
| Public | ציבורי / מוסדי | ייעוד, הגבלות שימוש |

The classification determines which due diligence sections are mandatory vs. optional in the output.

---

## 5. Chapter 7.0 — המצב המשפטי והקנייני

### 5.1 Analysis Protocol (Persona & Methodology)

Agent 4 operates as a **senior professional consultant to a real estate appraiser**, combining the expertise of an experienced appraiser and a legal expert in real estate and contracts. Its persona is conservative, cautious, and meticulous — operating as a risk manager for a financing body (bank).

For every document analysis:
1. **Distill information** for the appraisal opinion for the bank
2. **Advise the appraiser** on required verification steps to reduce risk

**Systematic analysis checklist:**

**א) בדיקות מקדמיות (Due Diligence):**
- תכנון: ייעוד ותב"ע (cross-ref with Agent 3)
- תיק בניין: מצב היתרים וחריגות (cross-ref with Agent 3)
- היטלים: היטל השבחה, אגרות, חובות לרשות

**ב) מנגנונים חוזיים:**
- הצהרות המוכר (representations and warranties)
- נאמנות: קיום ליווי בנקאי, כספי נאמנות
- פיצוי מוסכם: סכום, תנאים, מנגנון הפעלה

**ג) בדיקות ספציפיות לסוג הנכס:**

*מגורים:*
- הצמדות: אימות חניה, מחסן, גינה מול נסח
- בדק בית: האם בוצע, ממצאים
- ועד בית: חובות, יתרות, הסכמים מיוחדים

*קרקע:*
- זיקות הנאה (easements): מיפוי ועדכון
- הסכמי שיתוף: פירוט, ביטול, בר-תוקף
- ייעוד: תב"ע ופוטנציאל שינוי

*מסחרי:*
- הסכמי שכירות קיימים: שוכרים, תנאים, אופציות
- חשיפת מע"מ: עסקה חייבת/פטורה
- ניהול עסק חי: העברת רישיון, חוזי ספקים

### 5.2 Required Output Structure

**Part A — סיכום מובנה לחוות דעת שמאית:**

```markdown
## 7.0 המצב המשפטי והקנייני

### 7.1 תקציר מנהלים — מצב משפטי
[2–3 paragraph executive summary: rights nature, encumbrances, key risks, fitness as collateral]

### 7.2 טבלת נתוני יסוד — Data Sheet

| פרמטר | נתון | מקור |
|--------|------|------|
| סוג הזכות | | נסח טאבו |
| בעלים רשום | | נסח טאבו |
| שטח רשום | | נסח טאבו |
| הצמדות רשומות | | נסח טאבו |
| עיקולים | | נסח טאבו |
| משכנתאות | | נסח טאבו |
| הערות אזהרה | | נסח טאבו |
| שעבודים | | נסח טאבו |
| מחיר חוזי | | חוזה מכר |
| תנאי תשלום | | חוזה מכר |
| מועד מסירה | | חוזה מכר |
| פיצוי מוסכם | | חוזה מכר |
| מנגנון נאמנות | | חוזה מכר |
```
```

**Part B — ניתוח סיכונים והמלצות מקצועיות לשמאי:**

```markdown
### 7.3 דגלים אדומים — Red Flags

[Bulleted list of material risks, ranked by severity:
🔴 קריטי — risks that could invalidate the transaction or collateral
🟡 ניכר — risks that require disclosure or mitigating action
🟢 מינורי — risks to note but not blocking]

### 7.4 Actionable Checklist — בדיקות נוספות נדרשות

[ ] [Specific verification task for the appraiser]
[ ] [Specific verification task for the appraiser]
...
```

**Mandatory disclaimer (always last):**

```markdown
---
*יובהר כי ניתוח זה מהווה כלי עזר מקצועי עבור שמאי מקרקעין ואינו מהווה ייעוץ משפטי, שמאי או אחר בפני עצמו. הנתונים וההמלצות דורשים אימות ובדיקה עצמאיים ואין להסתמך עליהם באופן בלעדי.*
```

---

## 6. Cross-Reference Protocol (טאבו vs. Contract)

After reading both נסח טאבו and חוזה מכר, Agent 4 compares:

| Data Point | טאבו Value | Contract Value | Contradiction? |
|---|---|---|---|
| שטח הנכס | [X] מ"ר | [Y] מ"ר | if |X−Y| > 1 → flag |
| הצמדות | [list] | [list] | if mismatch → flag |
| בעלים | [name] | [name] | if mismatch → flag |
| עיקולים/שעבודים | [list] | disclosed? | if not disclosed → 🔴 |

**If any contradiction is found:**
```
🔴 סתירה בין נסח טאבו לחוזה מכר
פרמטר: [שם השדה]
ערך בנסח: [ערך]
ערך בחוזה: [ערך]
המלצה: לא לאשר שומה עד לקבלת הבהרה בכתב ממוכר/עורך דין.
```

This contradiction report is passed to the CEO as a **blocking flag** — the pipeline halts until user resolves.

---

## 7. CEO Verification Checks

| Check | Failure action |
|---|---|
| Property classification stated at top of output | Block |
| Part A (7.1 + 7.2 Data Sheet) present and fully populated | Block |
| Part B (7.3 Red Flags + 7.4 Checklist) present | Block |
| Mandatory disclaimer present as last element | Block |
| Cross-reference report submitted (clean or flagged) | Block if absent |
| No `[ערך]` / `[נתון]` placeholders in 7.2 Data Sheet | Block |

---

## 8. Open Questions

- האם Agent 4 מייצר פלט נפרד לכל מסמך (נסח, חוזה, תקנון) או פלט אחד משולב?
- מה הטיפול במקרה של חוזה מכר חסר — האם Agent 4 מנתח את הנסח בלבד?
- האם פרק 7.0 כולל גם ניתוח תקנון בית משותף, או שזה נפרד?
