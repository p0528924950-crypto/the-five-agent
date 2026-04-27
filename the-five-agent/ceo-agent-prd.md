# PRD: CEO Agent — Real Estate Appraisal Supervisor (Standard 19)

**Version:** 0.2 — Draft  
**Date:** 2026-04-27  
**Status:** Planned

---

## 1. Overview

The CEO Agent is the single entry point and active **supervisor** (מפקח עבודה) for all AI-powered real estate appraisal work. It receives an appraisal request, runs chapter agents in strict sequential order, **verifies each agent's output before proceeding**, maintains a single Source of Truth (טבלת נתוני יסוד), and assembles the final Standard 19 (תקן 19) report.

**Key change from v0.1:** The CEO is no longer a passive router. It actively inspects each chapter output, blocks the pipeline on inconsistencies, and holds the user-facing audit trail. No agent's output enters the report until the CEO has explicitly verified it.

CLAUDE.md instructs every Claude session to always load and operate through this agent. No chapter agent may be invoked directly by the user — all requests flow through the CEO.

---

## 2. Goals

- Accept a raw appraisal request (address, property type, appraisal purpose)
- Run the Research Agent first and gate all subsequent work on its output
- Execute chapter agents in sequential order — one at a time
- **Verify each chapter output** before proceeding to the next (supervisor gate)
- Enforce a single Source of Truth (טבלת נתוני יסוד) across all agents
- Block the pipeline and alert the user on any contradiction or missing data
- Maintain an audit trail of all agent runs and verification results
- Assemble verified chapter outputs into a coherent, Standards-compliant report

---

## 3. User Stories

| As a… | I want to… | So that… |
|---|---|---|
| Appraiser | Provide an address and get a complete Standard 19 report | I save hours of manual writing |
| Appraiser | Ask for a single chapter only | I can update one section without rerunning the full workflow |
| Appraiser | Be notified immediately if any chapter output contradicts the source data | I don't submit an appraisal with internal inconsistencies |
| Developer | Add a new chapter agent | The CEO routes to it without core changes — only the routing table updates |

---

## 4. Functional Requirements

### 4.1 Input

```
- כתובת הנכס (מלאה)
- סוג הנכס: דירה | בית פרטי | מסחרי | קרקע | אחר
- מטרת השומה: מכירה | משכנתא | ירושה | מס | אחר
- מסמכים מצורפים (אופציונלי): נסח טאבו PDF, היתרי בנייה PDF, אישורי זכויות PDF
- פרקים מבוקשים (אופציונלי): ברירת מחדל = שומה מלאה
```

### 4.2 Routing Logic

| מילות מפתח (Hebrew) | סוכן יעד |
|---|---|
| מחקר, נתונים, איסוף, מידע | Research Agent |
| זיהוי, פרטי זיהוי, כללי, מזמין, מועד, ביקור, הצהרה, מסמכים | Agent 1: Setup & ID |
| תיאור נכס, נכס, דירה, בית, שטח, קומה, מבנה | Property Description Agent |
| סביבה, שכונה, אזור, מיקום, תשתיות, נגישות | Environment Description Agent |
| שוק, עסקאות, מחירים, השוואה, מדד | Market Analysis Agent |
| משפטי, רגולטורי, רישום, טאבו, זכויות, חכירה | Legal/Regulatory Agent |
| תכנון, תב"ע, היתר, בנייה, ייעוד, תוכנית | Planning Status Agent |
| גורמים, שיקולים, השפעות, ניתוח ערך | Factors & Considerations Agent |
| בקרה, אימות, בדיקה, סיכום, עקביות | Quality Control Agent |

**Routing rules:**
1. **שומה מלאה (default):** Research → Agent 1 → כל פרקי הגוף בסדר → QC
2. **פרק בודד:** Research + הפרק המבוקש בלבד
3. **כמה מילות מפתח:** הפעל את כל הסוכנים המתאימים בסדר
4. **אין מילות מפתח:** הנח שומה מלאה, בקש אישור מהמשתמש

### 4.3 Sequential Supervisor Protocol

The CEO executes agents one at a time in Standard 19 sequence. After each agent completes, the CEO verifies the output before spawning the next agent.

```
For each agent in [Research → Agent1 → Agent2 → ... → QC]:

  SPAWN  — provide: Foundation Table (read-only) + all prior verified outputs
  RECEIVE — agent returns its chapter output
  VERIFY — CEO checks:
    (a) All required sections present and non-empty
    (b) No values contradict Foundation Table (גוש, חלקה, שטח, זכויות, ייעוד)
    (c) No [חסר] markers unless user was pre-alerted
    (d) No evidence of independent data lookups that bypass the Foundation Table
  GATE:
    • PASS → append output to report buffer → proceed to next agent
    • FAIL → STOP, report discrepancy to user, await decision: re-run / correct / skip
  LOG — record agent name, verification result, and any flags in the audit trail
```

**Execution order (Standard 19 sequence):**
```
1. Research Agent          ← חובה, תמיד ראשון
2. Agent 1: Setup & ID     ← פרקים 1.0, 2.0, 3.0
3. Property Description    ← פרק ד': תיאור הנכס
4. Environment Description ← פרק ה': תיאור סביבה
5. Legal/Regulatory        ← פרק ו': ניתוח משפטי/רגולטורי
6. Planning Status         ← פרק ז': מצב תכנוני
7. Market Analysis         ← פרק ח': ניתוח שוק
8. Factors & Considerations← פרק ט': גורמים ושיקולים
9. Quality Control         ← חובה, תמיד אחרון
```

### 4.4 Output

- קובץ Markdown יחיד: `appraisal-<address>-<date>.md`
- מבנה לפי תקן 19
- כל פרק נכתב ע"י הסוכן המתאים ועבר אימות מנכ"ל
- קובץ audit log נלווה: `appraisal-<address>-<date>-audit.md`

---

## 5. Research Agent — Enhanced Spec

### 5.1 תפקיד

הסוכן הראשון שרץ בכל שומה. אוסף ומעבד את כל הנתונים הגולמיים לפני שאיזה שהוא סוכן פרק מתחיל לכתוב. מייצר **טבלת נתוני יסוד** שהיא מקור האמת היחיד למערכת.

### 5.2 קליטת מסמכים (Hebrew PDF)

| מסמך | שדות לחילוץ |
|---|---|
| נסח טאבו | גוש, חלקה, תת-חלקה, שטח רשום (מ"ר), בעלים, מהות זכות, הערות אזהרה, עיקולים, משכנתאות |
| אישור זכויות | בעלים, חלק, מהות הזכות, תאריך עדכון |
| היתר בנייה | מספר היתר, שטח מאושר (מ"ר), ייעוד, תאריך הנפקה, סטטוס |

**דרישת יכולת:** חילוץ טקסט מ-PDF בעברית + נרמול שדות לפורמט אחיד.

### 5.3 מקורות מידע ישראליים

| מקור | סוג הנתון |
|---|---|
| רשות המיסים — מחירון עסקאות נדל"ן | עסקאות מכר (גוש/חלקה, תאריך, מחיר, שטח) |
| GovMap | שכבות תכנוניות, ייעוד קרקע, תב"ע, מדידות |
| פורטל התכנון הארצי (mavat.iplan.gov.il) | תוכניות תב"ע, סטטוס אישור, הוראות בנייה |
| מדלן | מחירי שוק, מחירי שכירות, עסקאות השוואה |

### 5.4 פלט חובה: טבלת נתוני יסוד

הפלט **היחיד והמחייב** של ה-Research Agent. מתפרסם לפני כל פעולה של סוכני הפרק.

```markdown
## טבלת נתוני יסוד

| שדה | ערך | מקור | תאריך עדכון |
|-----|-----|------|-------------|
| כתובת מלאה | | | |
| גוש | | נסח טאבו | |
| חלקה | | נסח טאבו | |
| תת-חלקה | | נסח טאבו | |
| שטח רשום (מ"ר) | | נסח טאבו | |
| שטח בנוי (מ"ר) | | היתר בנייה | |
| ייעוד תכנוני | | GovMap / תב"ע | |
| זכות בנכס | | נסח טאבו | |
| הערות אזהרה | | נסח טאבו | |
| עסקאות השוואה (3–5) | | רשות המיסים | |
| מחיר שוק ממוצע (₪/מ"ר) | | מדלן / רשות המיסים | |
```

**חוזה נתונים:** אם שדה חסר → יירשם `[חסר — נדרש השלמה]`. המנכ"ל יעצור ויתריע למשתמש לפני המשך.

---

## 6. Supervisor Controls

### 6.1 Per-Agent Verification Gate

לאחר קבלת פלט מכל סוכן, המנכ"ל מריץ את בדיקות האימות הבאות לפני הפעלת הסוכן הבא:

| בדיקה | פעולה בכישלון |
|---|---|
| כל הסעיפים הנדרשים קיימים ולא ריקים | עצור, הצג סעיפים חסרים, המתן לפתרון |
| ערכים תואמים לטבלת נתוני יסוד (שטח, גוש, חלקה, זכויות, ייעוד) | עצור, הצג אי-עקביות ספציפית, המתן לפתרון |
| אין `[חסר]` לא מטופלים | עצור, הצג שדות ריקים, המתן לפתרון |
| אין עדות לחיפוש נתונים עצמאי שסותר את הטבלה | עצור, דווח על מקור סותר, המתן לפתרון |

### 6.2 Missing Data Gate (after Research Agent)

Before spawning any chapter agent:
1. בדוק שטבלת נתוני יסוד קיימת וכוללת את כל השדות
2. סרוק לאיתור `[חסר — נדרש השלמה]`
3. אם נמצא → עצור, הצג למשתמש:
   - מה חסר
   - מאיזה מקור לאסוף
   - איך לספק (העלאת PDF / אימות ידני)
4. המשך רק לאחר אישור משתמש

### 6.3 Error Recovery Options

When a verification gate fails, the CEO presents the user with exactly three options:

```
⚠️ אימות נכשל — [שם הסוכן]
בעיה: [תיאור הסתירה/החסר]
ערך בטבלת נתוני יסוד: [ערך]
ערך שהוחזר ע"י הסוכן: [ערך]

אנא בחר:
[1] הפעל מחדש את הסוכן עם אותם נתונים
[2] תקן את טבלת נתוני יסוד ידנית, לאחר מכן הפעל מחדש
[3] דלג על פרק זה והמשך (יסומן כ-[חסר] בדוח הסופי)
```

### 6.4 Audit Trail

The CEO maintains an audit log throughout execution:

```markdown
## Supervision Audit Log

| # | סוכן | סטטוס | בעיות | החלטת משתמש |
|---|------|--------|-------|--------------|
| 1 | Research Agent | ✅ עבר | — | — |
| 2 | Agent 1: Setup & ID | ✅ עבר | — | — |
| 3 | Property Description | ⚠️ נכשל | שטח סותר טבלה (120 vs 118 מ"ר) | הפעל מחדש |
| ... | | | | |
```

### 6.5 Data Consistency Rule

כל סוכני הפרק חייבים להשתמש אך ורק בנתונים מטבלת נתוני יסוד עבור:
- שטח הנכס (רשום ובנוי)
- ייעוד תכנוני
- זכויות בנכס
- עסקאות השוואה

**אסור** לסוכן פרק לבצע חיפוש עצמאי שעלול לסתור את הטבלה.

---

## 7. Sub-agents Inventory

| סוכן | פרקים | סטטוס |
|---|---|---|
| Research Agent | איסוף נתונים + טבלת נתוני יסוד | Planned |
| Agent 1: Setup & ID | 1.0 פרטי זיהוי, 2.0 כללי, 3.0 זיהוי הנכס | In Progress |
| Property Description Agent | תיאור הנכס | Planned |
| Environment Description Agent | תיאור סביבה | Planned |
| Market Analysis Agent | ניתוח שוק | Planned |
| Legal/Regulatory Agent | ניתוח משפטי/רגולטורי | Planned |
| Planning Status Agent | מצב תכנוני (תב"ע + היתרים) | Planned |
| Factors & Considerations Agent | פרק גורמים ושיקולים | Planned |
| Quality Control Agent | בקרת איכות | Planned |

---

## 8. Open Questions

- האם ה-QC Agent חוסם (חייב לעבור לפני מסירה) או מייעץ (מגיש דוח עם שומה)?
- פורמט הפלט — קובץ MD יחיד, קובץ לכל פרק, או שניהם?
- כיצד המנכ"ל מטפל בכישלון חלקי של סוכן פרק אחרי 3 ניסיונות?
- מה ה-fallback אם GovMap / רשות המיסים לא נגישים?
- האם ה-Research Agent ניגש ל-APIs בזמן אמת או עובד על מסמכים שהמשתמש מספק?
