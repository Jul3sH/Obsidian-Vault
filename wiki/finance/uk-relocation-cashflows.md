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

## Executive Summary

### Bottom Line

- This file is the auditable model companion for the relocation savings comparison: cashflow source, tax assumptions, salary bands, annual net savings, and 10-year cumulative savings.
- The live source cashflow comes from the Relocation Cash Flows Google Sheet row 177: London HKD 669,984/yr, Malvern HKD 303,492/yr, and Hong Kong HKD 692,196/yr.
- The comparison uses four identical gross salary bands for London, Malvern, and Hong Kong: GBP 75k / HKD 750k, GBP 110k / HKD 1.1m, GBP 150k / HKD 1.5m, and GBP 200k / HKD 2.0m.
- Each location also has a zero-income stress case with its own cashflow still applied: London HKD -669,984/yr, Malvern HKD -303,492/yr, and Hong Kong HKD -692,196/yr.
- This file keeps the assumptions and calculations. The interpretive findings and observations live in [[uk-relocation-savings-comparison]].

### Key Takeaways

- Malvern has the lowest modelled cashflow only under the living-with-Mum assumption, with both properties rented and no independent Malvern accommodation, bills, or car added.
- London and Malvern use UK income tax and National Insurance. Hong Kong uses HK salaries tax with the 15% standard-rate cap.
- **At low salary, London and Hong Kong are both negative** on annual savings, while Malvern is positive because the cost base is much lower.
- **At medium and high salary, all locations are positive**, but London remains weakest because UK tax absorbs much more of the same gross salary.
- At extra-high salary, Hong Kong becomes the strongest savings case because the HK tax cap preserves more of the salary uplift.

---

## Change Log

| Date | What changed |
|---|---|
| 2026-08-04 | Added an executive summary so the model companion opens with the bottom line, key takeaways, source cashflow numbers, zero-income stress cases, and document boundary. |
| 2026-08-04 | Added London Zero and Hong Kong Zero stress-case columns to the live savings comparison. The model now has one GBP 0 / HKD 0 earnings case per location, with each location's own annual cashflow still applied. Updated the mirrored salary and 10-year cumulative tables here. |
| 2026-08-04 | Added a Malvern Zero stress-case column to the live savings comparison: GBP 0 / HKD 0 gross earnings with Malvern annual cashflow still applied. Updated the mirrored salary and 10-year cumulative tables here. |
| 2026-08-04 | Normalised the savings comparison to four identical salary bands across London, Malvern, and Hong Kong: Low GBP 75k / HKD 750k, Medium GBP 110k / HKD 1.1m, High GBP 150k / HKD 1.5m, Extra High GBP 200k / HKD 2.0m. Updated the live comparison Sheet rows 1-23, refreshed assumptions, and moved the findings readout to [[uk-relocation-savings-comparison]]. |
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
| Low band | GBP 75,000 / HKD 750,000 gross in every location |
| Medium band | GBP 110,000 / HKD 1,100,000 gross in every location |
| High band | GBP 150,000 / HKD 1,500,000 gross in every location |
| Extra High band | GBP 200,000 / HKD 2,000,000 gross in every location |
| Zero scenarios | Stress cases only: GBP 0 / HKD 0 gross earnings, with each location's own cashflow still applied. |
| Banding method | All three locations use identical salary bands for like-for-like comparison; original Robert Half ranges remain the source context, not separate location-specific bands. |
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

| | Lon Zero | Lon Low | Lon Med | Lon High | Lon Extra High | Mal Zero | Mal Low | Mal Med | Mal High | Mal Extra High | HK Zero | HK Low | HK Med | HK High | HK Extra High |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Gross salary (GBP) | 0 | 75,000 | 110,000 | 150,000 | 200,000 | 0 | 75,000 | 110,000 | 150,000 | 200,000 | 0 | 75,000 | 110,000 | 150,000 | 200,000 |
| Gross salary (HKD) | 0 | 750,000 | 1,100,000 | 1,500,000 | 2,000,000 | 0 | 750,000 | 1,100,000 | 1,500,000 | 2,000,000 | 0 | 750,000 | 1,100,000 | 1,500,000 | 2,000,000 |
| Income tax (HKD) | 0 | 174,320 | 334,320 | 537,030 | 762,030 | 0 | 174,320 | 334,320 | 537,030 | 762,030 | 0 | 87,060 | 146,560 | 214,560 | 299,560 |
| NI / HK salaries tax (HKD) | 0 | 35,110 | 42,110 | 50,110 | 60,110 | 0 | 35,110 | 42,110 | 50,110 | 60,110 | 0 | 0 | 0 | 0 | 0 |
| Total deductions (HKD) | 0 | 209,430 | 376,430 | 587,140 | 822,140 | 0 | 209,430 | 376,430 | 587,140 | 822,140 | 0 | 87,060 | 146,560 | 214,560 | 299,560 |
| Effective rate | 0.00% | 27.92% | 34.22% | 39.14% | 41.11% | 0.00% | 27.92% | 34.22% | 39.14% | 41.11% | 0.00% | 11.61% | 13.32% | 14.30% | 14.98% |
| Net take-home (HKD) | 0 | 540,570 | 723,570 | 912,860 | 1,177,860 | 0 | 540,570 | 723,570 | 912,860 | 1,177,860 | 0 | 662,940 | 953,440 | 1,285,440 | 1,700,440 |
| Annual cashflow (HKD) | 669,984 | 669,984 | 669,984 | 669,984 | 669,984 | 303,492 | 303,492 | 303,492 | 303,492 | 303,492 | 692,196 | 692,196 | 692,196 | 692,196 | 692,196 |
| **Annual net savings (HKD)** | **-669,984** | **-129,414** | **53,586** | **242,876** | **507,876** | **-303,492** | **237,078** | **420,078** | **609,368** | **874,368** | **-692,196** | **-29,256** | **261,244** | **593,244** | **1,008,244** |

---

## Section 3: Cumulative Savings Y1-Y10 (HKD)

| Year | Lon Zero | Lon Low | Lon Med | Lon High | Lon Extra High | Mal Zero | Mal Low | Mal Med | Mal High | Mal Extra High | HK Zero | HK Low | HK Med | HK High | HK Extra High |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Y1 | -669,984 | -129,414 | 53,586 | 242,876 | 507,876 | -303,492 | 237,078 | 420,078 | 609,368 | 874,368 | -692,196 | -29,256 | 261,244 | 593,244 | 1,008,244 |
| Y2 | -1,339,968 | -258,828 | 107,172 | 485,752 | 1,015,752 | -606,984 | 474,156 | 840,156 | 1,218,736 | 1,748,736 | -1,384,392 | -58,512 | 522,488 | 1,186,488 | 2,016,488 |
| Y3 | -2,009,952 | -388,242 | 160,758 | 728,628 | 1,523,628 | -910,476 | 711,234 | 1,260,234 | 1,828,104 | 2,623,104 | -2,076,588 | -87,768 | 783,732 | 1,779,732 | 3,024,732 |
| Y4 | -2,679,936 | -517,656 | 214,344 | 971,504 | 2,031,504 | -1,213,968 | 948,312 | 1,680,312 | 2,437,472 | 3,497,472 | -2,768,784 | -117,024 | 1,044,976 | 2,372,976 | 4,032,976 |
| Y5 | -3,349,920 | -647,070 | 267,930 | 1,214,380 | 2,539,380 | -1,517,460 | 1,185,390 | 2,100,390 | 3,046,840 | 4,371,840 | -3,460,980 | -146,280 | 1,306,220 | 2,966,220 | 5,041,220 |
| Y6 | -4,019,904 | -776,484 | 321,516 | 1,457,256 | 3,047,256 | -1,820,952 | 1,422,468 | 2,520,468 | 3,656,208 | 5,246,208 | -4,153,176 | -175,536 | 1,567,464 | 3,559,464 | 6,049,464 |
| Y7 | -4,689,888 | -905,898 | 375,102 | 1,700,132 | 3,555,132 | -2,124,444 | 1,659,546 | 2,940,546 | 4,265,576 | 6,120,576 | -4,845,372 | -204,792 | 1,828,708 | 4,152,708 | 7,057,708 |
| Y8 | -5,359,872 | -1,035,312 | 428,688 | 1,943,008 | 4,063,008 | -2,427,936 | 1,896,624 | 3,360,624 | 4,874,944 | 6,994,944 | -5,537,568 | -234,048 | 2,089,952 | 4,745,952 | 8,065,952 |
| Y9 | -6,029,856 | -1,164,726 | 482,274 | 2,185,884 | 4,570,884 | -2,731,428 | 2,133,702 | 3,780,702 | 5,484,312 | 7,869,312 | -6,229,764 | -263,304 | 2,351,196 | 5,339,196 | 9,074,196 |
| Y10 | -6,699,840 | -1,294,140 | 535,860 | 2,428,760 | 5,078,760 | -3,034,920 | 2,370,780 | 4,200,780 | 6,093,680 | 8,743,680 | -6,921,960 | -292,560 | 2,612,440 | 5,932,440 | 10,082,440 |

---

## Related

- [[uk-relocation-decision|UK Relocation Decision]] - the project this feeds
- [[uk-move-financial-model|UK Move Financial Model]] - runway and pot modelling (cashflow burn rates in section 0 superseded by Google Sheet)
- [[malvern-permanent-feasibility-2026-07-14|Malvern Permanent Feasibility]] - rules out permanent-Malvern variants
- [[uk-vs-hk-earning-comparison|UK vs HK Earning Comparison]] - salary band sources and tax differential
- [[uk-150k-feasibility-report|UK GBP 150k Feasibility Report]] - salary band sources, UK side
