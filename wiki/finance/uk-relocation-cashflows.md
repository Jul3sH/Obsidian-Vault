---
type: model
tags: [finance, uk-relocation, earnings, savings]
created: 2026-07-17
source: UK Relocation Cashflows Google Sheet
---

# UK Relocation Cashflows

> Wiki companion to the **[UK Relocation Cashflows Google Sheet](https://docs.google.com/spreadsheets/d/1HP-4Gm7TUqftlnCiXFqe34Wpp4torBt3NOZOb9BG4U4/edit)** (file ID: 1HP-4Gm7TUqftlnCiXFqe34Wpp4torBt3NOZOb9BG4U4). The Google Sheet is the live source of truth for all cashflow figures. This file documents the earnings and savings model built from it so any agent can resume or review the work without re-deriving from scratch.

**Do not use the burn rates in [[uk-move-financial-model]] section 0 as cashflow inputs. Those figures are superseded by the Google Sheet.**

---

## Change Log

| Date | What changed |
|---|---|
| 2026-07-17 | Added the Hong Kong conclusion to the Google Sheet: if HK work is available, HK is financially much better; the management issue is explaining and controlling why HK actual spending has been high. |
| 2026-07-17 | Added the bottom-line conclusion to the Google Sheet: London does not stack up financially unless high bracket London work is materially easier to land than lower bracket work in Malvern or Hong Kong. |
| 2026-07-17 | Replaced the Google Sheet's long Honest Read with four one-line summaries: HK Low beats London High; Malvern Low nearly matches London High; London has broader job-market upside while HK Low equals London Medium gross; Malvern High is near HK Median. |
| 2026-07-17 | Revised HK Low from HKD 1,000,000 / GBP 100k to HKD 1,100,000 / GBP 110k so it is a like-for-like gross comparison with UK Medium. HK Low annual savings increase from HKD 178,244 to HKD 261,244. |
| 2026-07-17 | Added the key savings insight: Malvern Low saves almost the same as London High (HKD 237,078 vs 242,876/yr), so Malvern's lower cost base nearly offsets the jump from GBP 75k to GBP 150k gross. |
| 2026-07-17 | Initial model created. Cashflow figures from Google Sheet row 177 (Cashflow total, monthly HKD). UK salary bands from Robert Half UK 2026. HK salary bands from Robert Half HK 2026. UK 2026/27 income tax + NI applied. HK salaries tax progressive rates applied. Previous wiki burn rates (uk-move-financial-model section 0) retired as cashflow source. |

---

## Trusted Source: How to Read the Google Sheet

All cashflow figures come from **row 177, labelled "Cashflow total"** in the Google Sheet. The figures are **monthly in HKD**. To use in annual HKD: multiply by 12.

**What the cashflow figures include (already netted):**
- All living expenses: dining, shopping, groceries, beauty, health, leisure, travel, bills, housing, transport, medical, financial
- Mortgage payments: Pine View principal + interest; Cecil Road interest via Barclays
- Property income already deducted: Cecil Road net income credited for HK and Malvern; Pine View net income credited for London and Malvern
- Hybrid commuting costs included in Malvern: hotels 2 nights/week (HKD 2,000/mo) + weekly rail ticket to London (HKD 2,000/mo)

**Property income by scenario:**

| Scenario | Julian lives in | Properties rented out | Rental income in cashflow |
|---|---|---|---|
| HK | Pine View (HK) | Cecil Road | Cecil Road net HKD 21,940/mo |
| London | Cecil Road (Wimbledon) | Pine View | Pine View net HKD 22,000/mo |
| Malvern | Mum's (Malvern) | Both | Cecil Road HKD 21,940 + Pine View HKD 22,000 = HKD 43,940/mo |

---

## Assumptions

| Assumption | Value |
|---|---|
| Exchange rate | HKD 10 = GBP 1 |
| Tax system (UK) | 2026/27 HMRC income tax + National Insurance |
| Personal allowance | GBP 12,570 (tapers GBP 1 per GBP 2 above GBP 100k; zero above GBP 125,140) |
| UK Basic rate | 20% on GBP 12,571 to GBP 50,270 |
| UK Higher rate | 40% on GBP 50,271 to GBP 125,140 |
| UK Additional rate | 45% above GBP 125,140 |
| UK NI employee rate | 8% on GBP 12,570 to GBP 50,270; 2% above GBP 50,270 |
| HK tax system | Progressive rates + 15% standard rate cap; basic allowance HKD 132,000 |
| HK progressive rates | 2% / 6% / 10% / 14% / 17% in HKD 50,000 bands above allowance |
| UK salary bands source | Robert Half UK Salary Guide 2026 (Enterprise/Solution Architect, London) |
| HK salary bands source | Robert Half HK Salary Guide 2026 (Enterprise Architect) |
| UK Low band | GBP 75,000 gross (floor role; Julian is over-qualified; just below cash-flow break-even in London) |
| UK Medium band | GBP 110,000 gross (central case perm; mid-point of GBP 85-130k band) |
| UK High band | GBP 150,000 gross (top-decile target; Robert Half P75) |
| HK Low band | HKD 1,100,000 gross (like-for-like with UK Medium / GBP 110k) |
| HK Medium band | HKD 1,500,000 gross (Robert Half P50) |
| HK High band | HKD 2,160,000 gross (Robert Half P75) |
| Cashflow source | Google Sheet row 177; monthly HKD net outflow after property income |
| Cashflow figures | Held constant (no inflation modelled) |
| Salary | Held constant (no growth modelled over 10 years) |
| Pension contributions | Not deducted from take-home; employer pension match is additional upside not modelled |
| Investment returns | Not modelled on accumulated savings |
| MPF | Not included; separate consideration on departure from HK |
| Cumulative savings | Incremental only; no starting pot included |
| Retired source | wiki/finance/uk-move-financial-model.md section 0 burn rates are superseded by the Google Sheet |

---

## Section 1: Cashflow (Source: Google Sheet row 177)

| | London | Malvern | HK |
|---|---|---|---|
| Monthly cashflow (HKD) | 55,832 | 25,291 | 57,683 |
| Annual cashflow (HKD) | 669,984 | 303,492 | 692,196 |

---

## Section 2: Salary, Tax and Annual Net Savings (all HKD)

| | Lon Low | Lon Med | Lon High | Mal Low | Mal Med | Mal High | HK Low | HK Med | HK High |
|---|---|---|---|---|---|---|---|---|---|
| Gross salary (GBP) | 75,000 | 110,000 | 150,000 | 75,000 | 110,000 | 150,000 | 110,000 | 150,000 | 216,000 |
| Gross salary (HKD) | 750,000 | 1,100,000 | 1,500,000 | 750,000 | 1,100,000 | 1,500,000 | 1,100,000 | 1,500,000 | 2,160,000 |
| Income tax (HKD) | 174,320 | 334,320 | 537,030 | 174,320 | 334,320 | 537,030 | 146,560 | 214,560 | 324,000 |
| NI / HK salaries tax (HKD) | 35,110 | 42,110 | 50,110 | 35,110 | 42,110 | 50,110 | 0 | 0 | 0 |
| Total deductions (HKD) | 209,430 | 376,430 | 587,140 | 209,430 | 376,430 | 587,140 | 146,560 | 214,560 | 324,000 |
| Effective rate | 27.9% | 34.2% | 39.1% | 27.9% | 34.2% | 39.1% | 13.3% | 14.3% | 15.0% |
| Net take-home (HKD) | 540,570 | 723,570 | 912,860 | 540,570 | 723,570 | 912,860 | 953,440 | 1,285,440 | 1,836,000 |
| Annual cashflow (HKD) | 669,984 | 669,984 | 669,984 | 303,492 | 303,492 | 303,492 | 692,196 | 692,196 | 692,196 |
| **Annual net savings (HKD)** | **-129,414** | **53,586** | **242,876** | **237,078** | **420,078** | **609,368** | **261,244** | **593,244** | **1,143,804** |

---

## Section 3: Cumulative Savings Y1-Y10 (HKD)

| Year | Lon Low | Lon Med | Lon High | Mal Low | Mal Med | Mal High | HK Low | HK Med | HK High |
|---|---|---|---|---|---|---|---|---|---|
| Y1 | -129,414 | 53,586 | 242,876 | 237,078 | 420,078 | 609,368 | 261,244 | 593,244 | 1,143,804 |
| Y2 | -258,828 | 107,172 | 485,752 | 474,156 | 840,156 | 1,218,736 | 522,488 | 1,186,488 | 2,287,608 |
| Y3 | -388,242 | 160,758 | 728,628 | 711,234 | 1,260,234 | 1,828,104 | 783,732 | 1,779,732 | 3,431,412 |
| Y4 | -517,656 | 214,344 | 971,504 | 948,312 | 1,680,312 | 2,437,472 | 1,044,976 | 2,372,976 | 4,575,216 |
| Y5 | -647,070 | 267,930 | 1,214,380 | 1,185,390 | 2,100,390 | 3,046,840 | 1,306,220 | 2,966,220 | 5,719,020 |
| Y6 | -776,484 | 321,516 | 1,457,256 | 1,422,468 | 2,520,468 | 3,656,208 | 1,567,464 | 3,559,464 | 6,862,824 |
| Y7 | -905,898 | 375,102 | 1,700,132 | 1,659,546 | 2,940,546 | 4,265,576 | 1,828,708 | 4,152,708 | 8,006,628 |
| Y8 | -1,035,312 | 428,688 | 1,943,008 | 1,896,624 | 3,360,624 | 4,874,944 | 2,089,952 | 4,745,952 | 9,150,432 |
| Y9 | -1,164,726 | 482,274 | 2,185,884 | 2,133,702 | 3,780,702 | 5,484,312 | 2,351,196 | 5,339,196 | 10,294,236 |
| Y10 | -1,294,140 | 535,860 | 2,428,760 | 2,370,780 | 4,200,780 | 6,093,680 | 2,612,440 | 5,932,440 | 11,438,040 |

---

## Key Observations

- **London Low loses money every year** (HKD -129,414/yr): London cashflow (HKD 55,832/mo) is nearly identical to HK (HKD 57,683/mo) but UK tax is far higher, so the take-home never covers costs at the low band.
- **UK tax penalty is severe at the like-for-like GBP 110k band**: London Medium saves HKD 53,586/yr; revised HK Low saves HKD 261,244/yr on the same gross salary. HK is ahead by HKD 207,658/yr.
- **Malvern only makes financial sense as a hybrid working base**: the Malvern figures include HKD 4,000/mo of commuting cost (hotels + rail). Without a London-facing hybrid role, those costs are wasted.
- **Malvern Medium is the realistic central case for hybrid**: GBP 110,000 sits mid-range of the GBP 85-130k central case. Annual savings HKD 420,078 (HKD 4,200,780 over 10 years).
- **Malvern Low nearly matches London High on savings**: Malvern Low saves HKD 237,078/yr; London High saves HKD 242,876/yr, only HKD 5,798/yr more. The lower Malvern cost base almost offsets the gross-salary jump from GBP 75k to GBP 150k.
- **HK Low beats London High on savings**: revised HK Low saves HKD 261,244/yr; London High saves HKD 242,876/yr.
- **Malvern High is close to HK Median**: Malvern High saves HKD 609,368/yr; HK Medium saves HKD 593,244/yr.
- **HK High (HKD 1,143,804/yr) is the best outcome by far** but is conditional on landing a role at Robert Half P75 in a cooling, local-first market.
- **Bottom line**: London does not stack up financially as an option unless high bracket London work is materially easier to land than lower bracket work in Malvern or Hong Kong.
- **Hong Kong conclusion**: if work is available in Hong Kong, it is financially much better; the management issue is explaining and controlling why HK actual spending has been high.

---

## Related

- [[uk-relocation-decision|UK Relocation Decision]] - the project this feeds
- [[uk-move-financial-model|UK Move Financial Model]] - runway and pot modelling (cashflow burn rates in section 0 superseded by Google Sheet)
- [[malvern-permanent-feasibility-2026-07-14|Malvern Permanent Feasibility]] - rules out permanent-Malvern variants
- [[uk-vs-hk-earning-comparison|UK vs HK Earning Comparison]] - salary band sources and tax differential
- [[uk-150k-feasibility-report|UK GBP 150k Feasibility Report]] - salary band sources, UK side
