---
type: reference
tags: [finance, uk-relocation, savings, earnings]
created: 2026-07-17
source: UK Relocation Savings Comparison Google Sheet
---

# UK Relocation Savings Comparison

> Wiki companion to the **[UK Relocation Savings Comparison Google Sheet](https://docs.google.com/spreadsheets/d/1HuBwQvRizmtNmi0CRXHA9R4HC1qPGGxjqzvgt-yD0LM/edit)** (file ID: 1HuBwQvRizmtNmi0CRXHA9R4HC1qPGGxjqzvgt-yD0LM). The Google Sheet is the live visual output surface for the earnings and savings comparison. This file logs structural changes to the sheet so any agent can understand what it contains and how it has evolved.

**All source data, assumptions, and detailed model workings live in [[uk-relocation-cashflows]], not here.**

---

## What the Sheet Contains

The sheet is the paste-in output of the earnings model built from the [[uk-relocation-cashflows]] wiki file and the [Relocation Cash Flows Google Sheet](https://docs.google.com/spreadsheets/d/1HP-4Gm7TUqftlnCiXFqe34Wpp4torBt3NOZOb9BG4U4/edit). It holds four sections:

| Section | Content |
|---|---|
| Cashflow summary | Monthly and annual HKD cashflow by location (London / Malvern / HK). Source: Relocation Cash Flows sheet row 177. |
| Salary, tax and savings | 9-column table: gross salary (GBP + HKD), income tax, NI, effective rate, net take-home, annual cashflow, annual net savings. Columns: London Low / Med / High, Malvern Low / Med / High, HK Low / Med / High. |
| 10-year cumulative | Y1-Y10 cumulative savings for all 9 columns. |
| Assumptions | Exchange rate, UK 2026/27 tax bands, HK salaries tax, salary band sources, modelling constraints. |
| Why London savings look poor | Narrative analysis: London cashflow penalty (Cecil Road foregone rent + higher bills) and UK tax differential vs HK. |

---

## Change Log

| Date | What changed |
|---|---|
| 2026-07-17 | Added a Hong Kong conclusion to the Sheet: if HK work is available, HK is financially much better; the management issue is explaining and controlling why HK actual spending has been high. |
| 2026-07-17 | Added a bottom-line conclusion to the Sheet: London does not stack up financially unless high bracket London work is materially easier to land than lower bracket work in Malvern or Hong Kong. |
| 2026-07-17 | Replaced the Sheet's long Honest Read with four one-line summaries: HK Low beats London High; Malvern Low nearly matches London High; London has broader job-market upside while HK Low equals London Median gross; Malvern High is near HK Median. |
| 2026-07-17 | Revised HK Low from HKD 1,000,000 / GBP 100k to HKD 1,100,000 / GBP 110k so it matches London Medium gross for direct comparison. |
| 2026-07-17 | Added explicit summary line to the Google Sheet: Malvern Low savings nearly equal London High savings (HKD 237,078 vs 242,876/yr). |
| 2026-07-17 | Corrected the Google Sheet's bottom explanatory block (`WHY LONDON SAVINGS LOOK POOR`) using [[uk-relocation-savings-comparison-number-check-2026-07-17]]. |
| 2026-07-17 | Number audit created: [[uk-relocation-savings-comparison-number-check-2026-07-17]]. Core calculation tables pass; bottom explanatory block has stale numbers and should not be relied on until corrected. |
| 2026-07-17 | Initial sheet created. Model data pasted from Claude session: Section 1 cashflow, Section 2 salary/tax/savings, Section 3 10-year cumulative, assumptions, and a "Why London savings look poor" explanatory analysis. Cashflow figures sourced from Relocation Cash Flows sheet row 177 (Malvern includes hotel HKD 2,000/mo + rail HKD 2,000/mo). |

---

## How to Update

When you make structural changes to the sheet (add a section, add a scenario, change the column layout, or update source figures), add a row to the Change Log above. Data-only refreshes (pasting updated numbers into an existing structure) do not need a log entry - the change log is for structure, not content.

When updating numbers:
1. Check the [Relocation Cash Flows sheet](https://docs.google.com/spreadsheets/d/1HP-4Gm7TUqftlnCiXFqe34Wpp4torBt3NOZOb9BG4U4/edit) row 177 for the latest cashflow figures.
2. Recalculate via [[uk-relocation-cashflows]] (update that file's sections too, and add a change log row there).
3. Paste the updated tables into this Google Sheet.
4. Add a row here only if the structure changed.

---

## Related

- [[uk-relocation-cashflows]] - Source of truth for all figures, assumptions, and model workings
- [[uk-relocation-decision]] - The project this feeds
- [[uk-move-financial-model]] - Runway and pot modelling (burn rates in section 0 superseded by the Relocation Cash Flows sheet)
