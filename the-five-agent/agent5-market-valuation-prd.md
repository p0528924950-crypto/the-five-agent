# PRD: Agent 5 — Market & Valuation

**Version:** 0.1 — Draft  
**Date:** 2026-04-27  
**Status:** In Progress

---

## 1. Overview

Agent 5: Market & Valuation is the economic core of the appraisal pipeline. It produces three chapters:

- **8.0 עקרונות השומה** — appraisal principles: method, basis of value, date, assumptions
- **9.0 תיאור המצב הכלכלי והשוק** — market conditions: price trends, supply/demand, competing projects
- **10.0 תחשיב השווי** — valuation calculation: equivalent area table, comparison transaction table with adjustments, final value in numbers and words

Agent 5 is the only agent that performs **quantitative calculations**. It receives synthesized data from two prior agents:
- **Agent 2** (Physical & Environment) → physical parameters: area, attachments, floor, orientation
- **Agent 4** (Legal & Tenure) → legal constraints: rights type, lease terms, encumbrances

The final value produced by Agent 5 is the central output of the entire appraisal.

**Token efficiency constraint:** Reads transaction tables, market reports, and comparable data **only** from `the-five-agent/current_property_data/`.

**Gold Standard reference:** Methodology and output format based on completed Standard 19.0 appraisal for פרויקט "חצר הנביאים", רחוב מונבז 3, דירה 101, ירושלים (value: ₪5,460,000).

---

## 2. Goals

- Produce a rigorous market analysis grounded in real transaction data
- Calculate the equivalent area using תקן 9 coefficients
- Build a comparison transaction table with documented appraisal adjustments
- Apply a leasehold discount if Agent 4 reported a capitalized/fixed-term lease
- Output the final value clearly in both numbers and words
- Never produce a round number — round to the nearest ₪5,000 (Israeli appraisal convention)

---

## 3. Path Constraint (Token Efficiency)

**Agent 5 reads market data exclusively from:**
```
the-five-agent/current_property_data/
```

Expected files:
| File | Content |
|---|---|
| `transactions.xlsx` / `transactions.pdf` | רשות המיסים — comparison transactions |
| `market_report.pdf` | דוח שוק עדכני (מדלן / קנדו / אחר) |
| `madlan_data.json` | מחירי שוק שכונתיים |
| `competing_projects.pdf` | פרויקטים תחרותיים |

Agent 5 must **not** scan any other directory.

---

## 4. Data Sync — Inputs from Prior Agents

The CEO passes the following to Agent 5:

| Input | Source Agent | Data |
|---|---|---|
| Foundation Table | Research Agent | שטח רשום, גוש, חלקה, כתובת |
| Physical parameters | Agent 2 (4.4 + 4.5) | שטח עיקרי, ממ"ד, מרפסות, חניה, מחסן, קומה, כיוון |
| Legal constraints | Agent 4 (7.0) | סוג זכות, פרטי חכירה, הערות אזהרה, עיקולים |
| Market data files | current_property_data/ | עסקאות, דוחות שוק |

Agent 5 **must not** re-read documents already processed by prior agents. It uses their verified outputs as its data inputs.

---

## 5. Chapter 8.0 — עקרונות השומה

A brief structured chapter (1–2 pages) stating the appraisal framework:

### Required Sections

| Section | Content |
|---|---|
| **שיטת השומה** | Method used: שיטת ההשוואה / גישת ההכנסה / עלות הבנייה + identify which method for this property |
| **בסיס הערכה** | שווי שוק (market value) as defined in Standard 19 |
| **מועד קובע** | Date of inspection (cross-ref with Agent 1 section 2.3) |
| **הנחות ומגבלות** | List of assumptions underpinning the valuation |
| **תקן 9** | Statement that area calculations follow תקן 9 |

---

## 6. Chapter 9.0 — תיאור המצב הכלכלי והשוק

### 9.1 מאקרו כלכלי
- ריבית בנק ישראל (current rate and trend)
- מדד מחירי הדיור לאומי (direction, % change YoY)
- תנאי מימון: LTV, ריבית משכנתא ממוצעת

### 9.2 שוק מקומי — ניתוח סביבה
- מגמות מחירים בשנה האחרונה (₪/מ"ר, % שינוי)
- רמת הביקוש: תאפיין רמת ביקוש (גבוה / בינוני / נמוך) עם ראיות
- רמת היצע: בנייה חדשה, מלאי פנוי, ימי שיווק ממוצעים

### 9.3 פרויקטים תחרותיים
- רשימת פרויקטים חדשים או מחודשים בסביבה הישירה
- טבלת מחירים שיווקיים להשוואה

### 9.4 מסקנת שוק
- האם שוק יציב, עולה, או יורד?
- ציפיות לטווח קצר (6–12 חודשים)

---

## 7. Chapter 10.0 — תחשיב השווי

### 7.1 שלב א': חישוב שטח אקוויוולנטי (תקן 9)

Agent 5 calculates the equivalent area using the following standard coefficients:

| רכיב | מקדם תקן 9 | שטח בפועל (מ"ר) | שטח אקוויוולנטי (מ"ר) |
|------|------------|-----------------|----------------------|
| שטח עיקרי | 1.00 | [from Agent 2] | [calculated] |
| ממ"ד | 1.00 | [from Agent 2] | [calculated] |
| מרפסת שמש | 0.35 | [from Agent 2] | [calculated] |
| מרפסת מקורה | 0.50 | [from Agent 2] | [calculated] |
| מרפסת שירות | 0.25 | [from Agent 2] | [calculated] |
| חניה תת-קרקעית | 0.30 | [from Foundation Table] | [calculated] |
| חניה חיצונית | 0.20 | [from Foundation Table] | [calculated] |
| מחסן | 0.25 | [from Foundation Table] | [calculated] |
| **סה"כ שטח אקוויוולנטי** | | | **[sum]** |

**Rule:** Use exact areas from Agent 2 / Foundation Table. No rounding of individual components — only the final equivalent total is rounded to the nearest 0.5 מ"ר.

### 7.2 שלב ב': טבלת עסקאות השוואה

Build a table of 3–6 comparable transactions from the past 12 months (from `current_property_data/transactions`):

**Required columns:**
| # | כתובת | תאריך עסקה | שטח עיקרי | קומה | כיוון | זכות | מחיר כולל | מחיר ל-מ"ר | מחיר אקוויוולנטי |
|---|--------|------------|-----------|------|-------|------|-----------|------------|-----------------|

**Appraisal adjustments (התאמות שמאיות) per transaction:**

For each comparable, apply and document the following adjustments:

| התאמה | גורם | הסבר |
|---|---|---|
| **מקדם זמן** | +0.5%–2% לחודש (or as per מדד) | Distance from transaction date to valuation date |
| **קומה** | ±1%–2% per floor vs. subject | Adjust up for higher floors, down for lower |
| **כיוון נוף** | ±2%–5% | Premium for park/open view; discount for internal courtyard |
| **זכויות** | ±3%–8% | Discount for חכירה לא מהוונת vs. בעלות; adjust for lease terms |
| **מצב** | ±3%–10% | New vs. renovated vs. requires renovation |
| **הצמדות** | ±amount | Add/subtract value of parking/storage vs. subject |

**Adjusted price per equivalent מ"ר** = base price × (1 + sum of adjustments).

### 7.3 שלב ג': גזירת שווי

After adjustments, calculate the weighted average ₪/equivalent מ"ר:

```
ממוצע משוקלל = Σ(מחיר אקוויוולנטי מותאם × משקל) / Σ(משקל)
```

Final value = ממוצע משוקלל × שטח אקוויוולנטי כולל של הנכס

**Round to nearest ₪5,000** (Israeli appraisal convention).

State final value:
- בספרות: ₪X,XXX,000
- במילים: [X מיליון ו-XXX אלף שקל חדש]

### 7.4 שלב ד': הפחתת חכירה (אם רלוונטי)

**Trigger:** Apply this step only if Agent 4 (chapter 7.0) reported that the rights type is:
- חכירה קצובה (fixed-term lease, not capitalized)
- חכירה כנסייתית (church/patriarchate lease)
- Any non-capitalized leasehold with remaining term < 80 years

**Leasehold discount model (per Gold Standard):**

| קריטריון | פרמטר |
|---|---|
| מהות הזכות | חכירה מהוונת / לא מהוונת |
| שם המחכיר | [from Agent 4] |
| תאריך פקיעה | [from Agent 4] |
| שנים שנותרו | [calculated] |
| שיעור הפחתה | לפי טבלת ה-Gold Standard או שיטת DCF |

Output:
```
שווי בעלות מלאה: ₪X,XXX,000
שיעור הפחתה לחכירה: [X]%
שווי זכות החכירה: ₪Y,YYY,000
```

---

## 8. Output Format — Chapter 10 Summary

```markdown
## 10.0 תחשיב השווי

### 10.1 ריכוז שטחים אקוויוולנטיים (תקן 9)
[table]

### 10.2 עסקאות השוואה ותיאומים
[table with adjustments]

### 10.3 גזירת השווי
ממוצע משוקלל: ₪[X] למ"ר אקוויוולנטי
שטח אקוויוולנטי: [Y] מ"ר
שווי מחושב: ₪[Z]

### 10.4 הפחתת חכירה [if applicable]
[leasehold discount calculation]

### 10.5 שווי הנכס הסופי
**שווי שוק של הנכס נכון ל-[תאריך]:
₪[X,XXX,000] ([X מיליון ו-X אלף שקל חדש])**
```

---

## 9. CEO Verification Checks

| Check | Failure action |
|---|---|
| Chapter 8.0 states appraisal method and valuation date | Block |
| Chapter 9.0 has all 4 sub-sections (9.1–9.4) | Block |
| Equivalent area table present with correct תקן 9 coefficients | Block |
| Comparison table has ≥3 transactions | Block |
| Each comparison has at least 3 documented adjustments | Block |
| Final value stated in both numbers and words | Block |
| If חכירה reported by Agent 4 → leasehold discount section present | Block |
| Final value is a multiple of ₪5,000 | Flag (warning, not block) |

---

## 10. Open Questions

- מה שיעור ההפחתה המדויק לחכירה מהוונת עד 2110 — האם לפי מודל ה-Gold Standard ספציפי?
- כמה עסקאות השוואה נדרשות מינימום (3 או 5)?
- האם תחשיב גישת ההכנסה נדרש כבדיקה נגדית, או שגישת ההשוואה מספיקה?
- האם Agent 5 מייצר הערכת רגישות (sensitivity analysis) לטווח שווי?
