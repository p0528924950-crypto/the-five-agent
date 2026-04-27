# PRD: Agent 1 — Setup & ID

**Version:** 0.1 — Draft  
**Date:** 2026-04-27  
**Status:** In Progress

---

## 1. Overview

Agent 1: Setup & ID is the first chapter agent to run after the Research Agent. It produces chapters 1.0, 2.0, and 3.0 of the Standard 19 appraisal — the identification and general framework sections that form the administrative backbone of the appraisal document.

These chapters do not contain valuation opinion — they establish the identity of the property, the commissioning context, and the formal registration details. All data comes from the Foundation Data Table (טבלת נתוני יסוד) and user-supplied source documents (נסח טאבו, אישורי זכויות).

**Gold Standard reference:** Chapter structure derived from the completed Standard 19.0 appraisal for פרויקט "חצר הנביאים", רחוב מונבז 3, ירושלים (2026).

---

## 2. Goals

- Produce chapters 1.0, 2.0, and 3.0 exactly as they appear in a Gold Standard Standard 19 appraisal
- Use only data from the Foundation Data Table — no independent lookups
- Output Markdown that can be dropped directly into the final report without editing
- Flag any missing field with `[חסר — נדרש השלמה]` rather than hallucinate a value
- Complete in a single run; the CEO verifies output before proceeding

---

## 3. Inputs

The agent receives the following from the CEO:

| Input | Source | Required |
|---|---|---|
| Foundation Data Table (טבלת נתוני יסוד) | Research Agent output | Yes |
| נסח טאבו (full PDF text or extracted fields) | User upload | Yes |
| אישורי זכויות | User upload | Recommended |
| מטרת השומה (appraisal purpose) | User request | Yes |
| שם המזמין / הלווה | User request | Yes |
| תאריך ביקור בנכס | User input | Yes |
| שם השמאי | User input | Yes |
| פירוט מסמכים שנבדקו | User input or derived | Yes |

---

## 4. Output — Three Chapter Sections

### 4.1 Chapter 1.0 — פרטי זיהוי הנכס (Property ID Summary)

A single structured table at the top of the appraisal — provides an at-a-glance property identity card.

**Required fields (16 fields):**

| שדה | מקור |
|---|---|
| גוש | Foundation Table / נסח טאבו |
| חלקה | Foundation Table / נסח טאבו |
| תת-חלקה | Foundation Table / נסח טאבו |
| כתובת הנכס | Foundation Table |
| מהות הנכס | User input + נסח טאבו |
| שטח הדירה (מ"ר) | Foundation Table |
| הצמדות | נסח טאבו / אישור זכויות |
| מהות הזכויות | Foundation Table / נסח טאבו |
| שם המזמין / הלווה | User input |
| מטרת השומה | User input |
| מועד קובע לשומה | User input |
| תאריך ביקור בנכס | User input |
| שם השמאי | User input |
| מספר רישיון שמאי | User input |
| כתובת משרד השמאי | User input |
| תאריך השומה | User input |

**Output format:**
```markdown
## 1.0 פרטי זיהוי הנכס

| פרט | פירוט |
|-----|-------|
| גוש / חלקה / תת-חלקה | [ערך] / [ערך] / [ערך] |
| כתובת הנכס | [ערך] |
| מהות הנכס | [ערך] |
| שטח הדירה | [ערך] מ"ר |
| הצמדות | [ערך] |
| מהות הזכויות | [ערך] |
| מזמין / לווה | [ערך] |
| מטרת השומה | [ערך] |
| מועד קובע | [ערך] |
| תאריך ביקור | [ערך] |
| שמאי | [שם], רישיון [מספר] |
| תאריך השומה | [ערך] |
```

---

### 4.2 Chapter 2.0 — פרק א': כללי (General)

Six sub-sections establishing the commissioning context and formal framework.

#### 2.1 מזמין ומטרת השומה
- שם מלא של המזמין / הלווה
- מטרת השומה (משכנתא / מכירה / ירושה / אחר)
- הגוף המזמין (בנק / פרטי / בית משפט / אחר)

#### 2.2 מהות הזכויות בנכס
- תיאור סוג הזכות (בעלות / חכירה מהוונת / חכירה לא מהוונת / אחר)
- אם חכירה: שם המחכיר, מספר חוזה, תאריך פקיעה
- הפניה לנסח הטאבו: סעיף בטבלת נתוני יסוד

#### 2.3 המועד הקובע לשומה
- תאריך ביקור בנכס (date of inspection)
- תאריך הגשת השומה (date of report)
- הצהרה שהמועד הקובע הוא תאריך הביקור אלא אם צוין אחרת

#### 2.4 פרטי הביקור בנכס
- תאריך ותיאור הביקור
- נוכחים בביקור (מי היה נוכח)
- נגישות — האם כל חלקי הנכס נבדקו

#### 2.5 הצהרת השמאי
Standard declaration text (adapted to the specific appraiser):
```
אני החתום מטה, [שם השמאי], שמאי מקרקעין בעל רישיון מספר [מספר], 
מצהיר כי הכנתי שומה זו בהתאם לתקן 19 של מועצת שמאי המקרקעין,
ללא תלות בצד כלשהו, ולפי מיטב ידיעתי ושיפוטי המקצועי.
```

#### 2.6 פירוט מסמכים שנבדקו
Bulleted list of all documents reviewed:
- נסח טאבו (תאריך הנסח)
- אישורי זכויות
- היתרי בנייה
- תוכניות אדריכליות (אם סופקו)
- כל מסמך נוסף שהמשתמש ציין

**Output format:**
```markdown
## 2.0 פרק א': כללי

### 2.1 מזמין ומטרת השומה
[טקסט]

### 2.2 מהות הזכויות בנכס
[טקסט]

### 2.3 המועד הקובע לשומה
[טקסט]

### 2.4 פרטי הביקור בנכס
[טקסט]

### 2.5 הצהרת השמאי
[טקסט]

### 2.6 פירוט מסמכים שנבדקו
- [מסמך 1]
- [מסמך 2]
```

---

### 4.3 Chapter 3.0 — פרק ב': זיהוי הנכס (Property Identification)

Five sub-sections providing formal, multi-dimensional property identification.

#### 3.1 זיהוי רישומי (Registration Identity)
From נסח טאבו / Foundation Table:
- גוש, חלקה, תת-חלקה
- שטח הנכס הרשום (מ"ר)
- בעלים רשום / מחכיר
- מהות הזכות הרשומה
- הערות אזהרה (אם קיימות)
- עיקולים / משכנתאות (אם קיימים)

#### 3.2 זיהוי פיזי (Physical Identity)
From site visit / user input:
- כתובת מלאה (רחוב, מספר, עיר)
- קומה ומספר הדירה
- מספר כניסה / בניין
- מאפייני המבנה הכללי (מספר קומות, שנת בנייה משוערת, חומרי בנייה)

#### 3.3 זיהוי מוניציפלי (Municipal Identity)
- שם הרשות המוניציפלית (עיר/מועצה)
- ייעוד ארנונה (מגורים / עסקי / אחר)
- מספר חשבון ארנונה (אם סופק)

#### 3.4 מהות הנכס (Property Nature)
- תיאור כללי: סוג הנכס (דירה, בית, מסחרי וכו')
- מספר חדרים, שטח עיקרי, שטח שירות
- הצמדות: חניה, מחסן, גינה (כפי שרשומים בנסח)

#### 3.5 מפות איתור (Location Maps)
- ציון שיש לצרף תמונת מפה מ-GovMap
- כתובת ה-URL של GovMap עם גוש/חלקה
- הנחיה: `[יש להדביק כאן תמונת מפה מ-GovMap]`

**Output format:**
```markdown
## 3.0 פרק ב': זיהוי הנכס

### 3.1 זיהוי רישומי
[טקסט עם כל שדות נסח הטאבו]

### 3.2 זיהוי פיזי
[טקסט מביקור]

### 3.3 זיהוי מוניציפלי
[טקסט]

### 3.4 מהות הנכס
[טקסט]

### 3.5 מפות איתור
[הנחיה לצירוף מפה + URL GovMap]
```

---

## 5. Data Sources

| Data Item | Primary Source | Fallback |
|---|---|---|
| גוש / חלקה / תת-חלקה | Foundation Table | נסח טאבו direct |
| שטחים | Foundation Table | היתר בנייה |
| זכויות | Foundation Table | נסח טאבו direct |
| הצמדות | נסח טאבו | אישור זכויות |
| הערות אזהרה / עיקולים | נסח טאבו | Foundation Table |
| מזמין, מטרה, תאריכים | User input | — |
| שם שמאי, רישיון | User input | — |
| מסמכים שנבדקו | User input + derived | — |

---

## 6. Constraints

- **Must not** generate or lookup גוש, חלקה, שטח, or זכויות values independently — all must come from Foundation Table
- **Must not** fabricate appraiser declarations — use exact text with user-supplied name and license number
- **Must not** skip any of the 16 fields in chapter 1.0 — write `[חסר — נדרש השלמה]` if a value is unavailable
- **Must not** access external APIs or web searches
- **Must** write all chapter headings in Hebrew exactly as in Gold Standard format

---

## 7. Quality Criteria

The CEO verifies Agent 1's output passes all of the following before proceeding:

| Criterion | Check |
|---|---|
| Chapter 1.0 table has all 16 rows | Count rows in output table |
| No row is empty or `[ערך]` placeholder | Scan for unfilled placeholders |
| גוש/חלקה/תת-חלקה match Foundation Table | Compare values |
| שטח values match Foundation Table | Compare values |
| מהות הזכויות matches Foundation Table | Compare values |
| All 6 sub-sections of chapter 2.0 present | Check headers 2.1–2.6 |
| All 5 sub-sections of chapter 3.0 present | Check headers 3.1–3.5 |
| No `[חסר]` without prior user alert | Scan for markers |
| Appraiser declaration uses real name/license | Verify no placeholder text remains |

---

## 8. Open Questions

- האם גרסת הנסח (תאריך נסח הטאבו) צריכה להופיע בפרק 2.6 או 3.1?
- האם יש לכלול מספר חשבון ארנונה בפרק 3.3 כשדה חובה?
- האם מפת ה-GovMap (3.5) מסופקת כתמונה שהמשתמש מעלה, או שהסוכן מייצר URL בלבד?
