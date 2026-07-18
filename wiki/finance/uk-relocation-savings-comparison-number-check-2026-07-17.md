---
type: review
tags: [finance, uk-relocation, savings, google-sheets, audit]
created: 2026-07-17
source: UK Relocation Savings Comparison Google Sheet
---

# UK Relocation Savings Comparison Number Check 2026-07-17

> Number audit of the **[UK Relocation Savings Comparison Google Sheet](https://docs.google.com/spreadsheets/d/1HuBwQvRizmtNmi0CRXHA9R4HC1qPGGxjqzvgt-yD0LM/edit)** against [[uk-relocation-savings-comparison]], [[uk-relocation-cashflows]], and the source **[Relocation Cash Flows Google Sheet](https://docs.google.com/spreadsheets/d/1HP-4Gm7TUqftlnCiXFqe34Wpp4torBt3NOZOb9BG4U4/edit)**.

## Key Takeaways

- The core calculation tables are internally consistent: salary, UK tax, NI, HK salaries tax, net take-home, annual savings, and 10-year cumulative savings all tie.
- The cashflow summary ties to the source cashflow sheet row 177, rounded monthly first.
- The explanatory block titled **WHY LONDON SAVINGS LOOK POOR** contained stale numbers, and was corrected in the Google Sheet on 2026-07-17.
- The corrected explanation now captures the key comparison: Malvern Low saves almost the same as London High (HKD 237,078 vs 242,876/yr).
- HK Low was later revised from HKD 1,000,000 / GBP 100k to HKD 1,100,000 / GBP 110k for a like-for-like comparison with London Medium. Revised HK Low annual savings are HKD 261,244.
- The output Sheet is hardcoded, not formula-driven. That is acceptable for a paste-in visual output surface, but it creates drift risk.
- The statement that the UK low band is below London break-even is true, but soft: London cash break-even is roughly GBP 98k gross, not close to GBP 75k.
- The Sheet's Honest Reads now use four one-line summaries, including HK Low beating London High and Malvern High roughly matching HK Median.
- The Sheet now has the explicit bottom-line conclusion: London does not stack up financially unless high bracket London work is materially easier to land than lower bracket work in Malvern or Hong Kong.
- The Sheet now also captures the Hong Kong conclusion: if HK work is available, HK is financially much better; the management issue is explaining and controlling why HK actual spending has been high.

## Source Check

Relocation Cash Flows row 177, labelled **Cashflow total**, currently shows:

| Source column | Scenario | Monthly HKD exact | Rounded monthly HKD used in output |
|---|---:|---:|---:|
| E | HK | 57,683.1667 | 57,683 |
| F | London | 55,832.1667 | 55,832 |
| G | Malvern | 25,291.1667 | 25,291 |

The output Sheet uses the rounded monthly values, then multiplies by 12:

| Scenario | Monthly HKD | Annual HKD in output | Check |
|---|---:|---:|---|
| London | 55,832 | 669,984 | OK |
| Malvern | 25,291 | 303,492 | OK |
| HK | 57,683 | 692,196 | OK |

Using exact monthly values before rounding would add only HKD 2/year per scenario. Immaterial.

## Core Table Check

The salary, tax, and annual savings table ties arithmetically.

| Scenario | Net take-home HKD | Annual cashflow HKD | Annual net savings HKD | Check |
|---|---:|---:|---:|---|
| London Low | 540,570 | 669,984 | -129,414 | OK |
| London Med | 723,570 | 669,984 | 53,586 | OK |
| London High | 912,860 | 669,984 | 242,876 | OK |
| Malvern Low | 540,570 | 303,492 | 237,078 | OK |
| Malvern Med | 723,570 | 303,492 | 420,078 | OK |
| Malvern High | 912,860 | 303,492 | 609,368 | OK |
| HK Low | 953,440 | 692,196 | 261,244 | OK |
| HK Med | 1,285,440 | 692,196 | 593,244 | OK |
| HK High | 1,836,000 | 692,196 | 1,143,804 | OK |

The 10-year cumulative table is also correct: each row is the annual net savings multiplied by year number.

## Tax Check

UK PAYE assumptions match the stated 2026/27 tax and NI rules used in the model:

| Gross GBP | Income tax GBP | NI GBP | Net GBP | Effective deduction rate | Check |
|---:|---:|---:|---:|---:|---|
| 75,000 | 17,432 | 3,511 | 54,057 | 27.9% | OK |
| 110,000 | 33,432 | 4,211 | 72,357 | 34.2% | OK |
| 150,000 | 53,703 | 5,011 | 91,286 | 39.1% | OK |

HK salaries tax assumptions match the stated progressive rates plus 15% standard-rate cap:

| Gross HKD | HK salaries tax HKD | Net HKD | Effective deduction rate | Check |
|---:|---:|---:|---:|---|
| 1,100,000 | 146,560 | 953,440 | 13.3% | OK, revised HK Low |
| 1,500,000 | 214,560 | 1,285,440 | 14.3% | OK |
| 2,160,000 | 324,000 | 1,836,000 | 15.0% | OK, standard-rate cap binds |

## Errors Found In The Explanatory Block

These were not in the core calculation tables. They were stale narrative/supporting numbers lower down the Sheet and have now been corrected.

| Sheet location | Current Sheet value | Correct value | Direction |
|---|---:|---:|---|
| C62, London monthly cashflow | 55,631 | 55,832 | London understated by 201 HKD/mo |
| C64, London vs HK monthly difference | 2,052 | 1,851 | Difference overstated by 201 HKD/mo |
| A74, Malvern net figure in text | 20,291 | 25,291 | Malvern understated by 5,000 HKD/mo |
| C77, Malvern Medium annual savings | 480,078 | 420,078 | Malvern overstated by 60,000 HKD/yr |
| C78, London Medium annual savings | 55,998 | 53,586 | London overstated by 2,412 HKD/yr |
| C79/D79, Malvern multiple | 8.6x | 7.8x | Multiple overstated |
| A82, London High annual savings | 245,288 | 242,876 | London overstated by 2,412 HKD/yr |
| A82, Malvern Low annual savings | 297,078 | 237,078 | Malvern overstated by 60,000 HKD/yr |
| A82, "London only makes financial sense at the high band" | Text claim | False as written | London Medium is positive, though thin |
| A82, "London High underperforms Malvern Low" | Text claim | False | London High is 5,798 HKD/yr above Malvern Low |

Corrected read:

| Comparison | Correct value |
|---|---:|
| London Medium annual savings | 53,586 HKD |
| Revised HK Low annual savings | 261,244 HKD |
| Revised HK Low minus London Medium | 207,658 HKD |
| Malvern Medium annual savings | 420,078 HKD |
| Malvern Medium vs London Medium | 7.8x |
| London High annual savings | 242,876 HKD |
| Malvern Low annual savings | 237,078 HKD |
| London High minus Malvern Low | 5,798 HKD |

## Break-Even Check

London annual cashflow is HKD 669,984, or GBP 66,998 at 10:1 FX. Re-running the UK PAYE assumptions:

| Gross GBP | Approx net HKD | London cashflow covered? |
|---:|---:|---|
| 75,000 | 540,570 | No |
| 95,000 | 656,574 | No |
| 97,000 | 668,174 | Just short |
| 98,000 | 673,974 | Yes |

So the low band is not just marginally below London break-even. It is materially below: about GBP 23k gross below the rough break-even point.

## Verdict

The Sheet's main calculation tables are usable. The explanatory bottom section was stale, but has now been corrected.

Current status: usable, with the caveat that the output Sheet remains hardcoded and must be refreshed if source row 177 or the salary assumptions change.

## Fix Applied

- Updated Google Sheet range `Sheet1!A58:D83`.
- Replaced the stale London cashflow, Malvern cashflow, annual savings, and ratio values.
- Reworded the honest-read paragraph so it captures that Malvern Low nearly matches London High, while no longer claiming London High underperforms Malvern Low.
- Later updated HK Low in the main tables from HKD 1,000,000 to HKD 1,100,000 for a like-for-like gross comparison with London Medium.
- Replaced the long Honest Read with four one-line summaries in `Sheet1!A82:A86`.
- Added the bottom-line conclusion in `Sheet1!A89:A90`.
- Added the Hong Kong conclusion in `Sheet1!A92:A93`.
- Verified the edited range after update.

Remaining improvement: consider converting the output Sheet to formulas or linked ranges if it is expected to remain live rather than a static visual paste.

## Related

- [[uk-relocation-savings-comparison]] - Wiki companion to the output Sheet
- [[uk-relocation-cashflows]] - Trusted model and assumptions
- [[uk-relocation-decision]] - Project status surface
