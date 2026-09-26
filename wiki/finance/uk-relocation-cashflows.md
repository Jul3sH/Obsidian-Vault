---
type: model
tags: [finance, uk-relocation, earnings, savings]
created: 2026-07-17
updated: 2026-09-26
source: UK Relocation savings comparison v3 and UK Relocation Cashflows Google Sheets
---

# UK Relocation Cashflows

> **What this is.** The model companion for the relocation savings comparison: where every input comes from, the assumptions, and a mirror of the v3 sheet's tables so any agent can resume or review without re-deriving.
> **Why it exists.** The Google Sheets are the live surfaces; this file makes them auditable. Rebuilt 25 Sep 2026 for the v3 model, which separates property income, letting costs and property tax from living costs.
> **How it is used.** Read before changing either sheet. Findings and what the numbers mean live in [[uk-relocation-savings-comparison]]. Internal only.

**Do not use the burn rates in [[uk-move-financial-model]] section 0 as cashflow inputs. Those figures are superseded.**

**Map:** §1 the two sheets · §2 property income by scenario · §3 assumptions · §4 living costs · §5 salary, tax and savings · §6 cumulative Y1 to Y10 · §6b runway blocks · §7 change log.

---

## 1. The two sheets

| Sheet | Role | Tab to use |
|---|---|---|
| [UK Relocation savings comparison v3](https://docs.google.com/spreadsheets/d/1TS-ve2WfgcBfNYrEaZCbl-4De_JdqHSqQbm_CdSZojM/edit) | The model: salary, tax, property rows, savings, cumulative | "Formula validation" (formula-driven) |
| [UK Relocation Cashflows](https://docs.google.com/spreadsheets/d/1HP-4Gm7TUqftlnCiXFqe34Wpp4torBt3NOZOb9BG4U4/edit) | Living costs by location, itemised | "Cashflow comparison"; its "Expenses total excluding housing" row feeds the savings sheet's three living-cost inputs |

**As of 26 Sep 2026, housing split.** The cashflow expense output excludes Housing running costs; the Housing block remains a supporting breakdown. The Malvern hotel belongs in discretionary Transport. Savings rows18/20 carry property running costs whether let or occupied. Mortgage principal and interest remain in the cashflow living budget. Julian removed the superseded cash-inflow/cash-burn blocks; use savings-sheet runway tables. Verification record: [[savings-v3-review]].

---

## 2. Property income by scenario

| Scenario | Julian lives in | Let | Rent in the model | Letting costs in the model | Lived-in home costs |
|---|---|---|---|---|---|
| Hong Kong | Pine View | Cecil Road | £30,000/yr | £4,140/yr | DB management, rates and insurance: HK$44,722/yr in savings row20 |
| London | Cecil Road | Pine View | HK$324,000/yr | HK$49,046/yr | Council tax, buildings and contents insurance: GBP2,652/yr in savings row18 |
| Malvern | Mum's | Both | £30,000 + HK$324,000 | £4,140 + HK$49,046 | None; hotel HK$2,000/mo for hybrid commuting stays in living costs |

Mortgage interest (Pine View HK$12,138/mo, Cecil Road £213/mo) and Pine View principal (HK$13,689/mo) sit inside living costs in every scenario. The principal builds equity but reduces cash.

---

## 3. Assumptions

| Assumption | Value |
|---|---|
| Exchange rate | HKD 10 = GBP 1 |
| Salary tax (UK) | 2026/27 income tax + NI: PA £12,570 tapering above £100k; 20% to £50,270; 40% to £125,140; 45% above; NI 8% then 2% above £50,270 |
| Property tax (UK) | 2027/28 property income rates 22% / 42% / 47%, mortgage interest credit 22% (Finance Act 2026 s7). Property income stacked on salary; personal allowance tapered on total income; HK tax credited up to the UK tax on the HK rent; interest credit applied before the foreign tax credit |
| FIG regime | Claim per year on the HK rent, first four UK-resident tax years from 2027/28; costs the personal allowance in the claim year. The sheet takes the lower of claim / no claim per column, and cumulative rows drop the relief from year five |
| HK Property Tax | 15% of 80% of (rent less rates) = HK$37,158/yr at HK$324,000 rent; London and Malvern only |
| HK salaries tax | Progressive 2/6/10/14/17% in HK$50,000 bands above basic allowance HK$145,000 (2026/27 onward); 15% standard-rate cap. Child and single-parent allowances not applied |
| UK tax when non-resident (HK scenario) | Cecil Road profit less personal allowance at 22%, less 22% interest credit: £2,361/yr |
| Salary bands | £0 / 75k / 110k / 135k / 150k / 200k in every location; HK$ at 10:1. Robert Half UK and HK 2026 guides are context only |
| Rents | Pine View HK$27,000/mo (target; agent estimated 22,000); Cecil Road £2,500/mo (target; May 2026 statement) |
| Letting costs, Pine View | DB management 2,054 + rates 1,196 + buildings insurance 275 per month, plus agent fee HK$13,500 per two-year tenancy: HK$49,046/yr |
| Letting costs, Cecil Road | Brinkleys £270/mo + rent protection £36/mo + buildings insurance £469/yr: £4,140/yr |
| Living costs | Cashflows sheet "Expenses total excluding housing" per location (see §4); mortgage payments retained; held constant, no inflation |
| Salary growth, investment returns, pension, MPF, starting pot | Not modelled |

---

## 4. Living costs (HK$ per month)

As of 26 Sep 2026, housing running costs are separated from the living inputs. This changes presentation, not cash burn.

| | London | Malvern | Hong Kong |
|---|---:|---:|---:|
| Full living inputs excluding Housing | 68,024.47 | 62,284.47 | 82,771.47 |
| Housing running costs in property rows | 2,210.00 | 0 | 3,726.83 |
| Combined full household costs | 70,234.47 | 62,284.47 | 86,498.30 |
| Lean living inputs excluding Housing | 45,742.97 | 44,142.97 | 65,479.97 |
| Housing retained in lean | 2,210.00 | 0 | 3,525.00 |

HK includes DBIS school fees HK$20,000/month. Malvern includes hotel HK$2,000/month and rail HK$2,000/month in discretionary Transport. Mortgage interest and principal remain included in all living inputs. HK contents insurance is discretionary: the lean formula adds back HK$2,422/year after full housing is deducted in property row20. The helper input is B132.


---

## 5. Salary, tax and annual net savings (HK$ per year)

Annual net savings = net take-home + (UK property income − UK property running costs) × 10 + HK property income − HK property running costs − HK Property Tax − UK tax on property (use) − living costs.

| | Lon Zero | Lon Low | Lon Med | Lon 135k | Lon High | Lon Extra High | Mal Zero | Mal Low | Mal Med | Mal 135k | Mal High | Mal Extra High | HK Zero | HK Low | HK Med | HK 135k | HK High | HK Extra High |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| Gross salary (GBP) | 0 | 75,000 | 110,000 | 135,000 | 150,000 | 200,000 | 0 | 75,000 | 110,000 | 135,000 | 150,000 | 200,000 | 0 | 75,000 | 110,000 | 135,000 | 150,000 | 200,000 |
| Gross salary (HKD) | 0 | 750,000 | 1,100,000 | 1,350,000 | 1,500,000 | 2,000,000 | 0 | 750,000 | 1,100,000 | 1,350,000 | 1,500,000 | 2,000,000 | 0 | 750,000 | 1,100,000 | 1,350,000 | 1,500,000 | 2,000,000 |
| UK property income (GBP) | 0 | 0 | 0 | 0 | 0 | 0 | 30,000 | 30,000 | 30,000 | 30,000 | 30,000 | 30,000 | 30,000 | 30,000 | 30,000 | 30,000 | 30,000 | 30,000 |
| UK property expenses (GBP), let or lived in | 2,652 | 2,652 | 2,652 | 2,652 | 2,652 | 2,652 | 4,140 | 4,140 | 4,140 | 4,140 | 4,140 | 4,140 | 4,140 | 4,140 | 4,140 | 4,140 | 4,140 | 4,140 |
| HK property income (HKD) | 324,000 | 324,000 | 324,000 | 324,000 | 324,000 | 324,000 | 324,000 | 324,000 | 324,000 | 324,000 | 324,000 | 324,000 | 0 | 0 | 0 | 0 | 0 | 0 |
| HK property expenses (HKD), let or lived in | 49,046 | 49,046 | 49,046 | 49,046 | 49,046 | 49,046 | 49,046 | 49,046 | 49,046 | 49,046 | 49,046 | 49,046 | 44,722 | 44,722 | 44,722 | 44,722 | 44,722 | 44,722 |
| Income tax (HKD) | 0 | 174,320 | 334,320 | 469,530 | 537,030 | 762,030 | 0 | 174,320 | 334,320 | 469,530 | 537,030 | 762,030 | 0 | 84,850 | 144,350 | 186,850 | 212,350 | 297,350 |
| NI / HK salaries tax (HKD) | 0 | 35,106 | 42,106 | 47,106 | 50,106 | 60,106 | 0 | 35,106 | 42,106 | 47,106 | 50,106 | 60,106 | 0 | 0 | 0 | 0 | 0 | 0 |
| Net take-home (HKD) | 0 | 540,574 | 723,574 | 833,364 | 912,864 | 1,177,864 | 0 | 540,574 | 723,574 | 833,364 | 912,864 | 1,177,864 | 0 | 665,150 | 955,650 | 1,163,150 | 1,287,650 | 1,702,650 |
| Living expenses (HKD), excluding housing running costs | 816,294 | 816,294 | 816,294 | 816,294 | 816,294 | 816,294 | 747,414 | 747,414 | 747,414 | 747,414 | 747,414 | 747,414 | 993,258 | 993,258 | 993,258 | 993,258 | 993,258 | 993,258 |
| HK Property Tax (HKD) | 37,158 | 37,158 | 37,158 | 37,158 | 37,158 | 37,158 | 37,158 | 37,158 | 37,158 | 37,158 | 37,158 | 37,158 | 0 | 0 | 0 | 0 | 0 | 0 |
| UK tax on property, no FIG (HKD) | 0 | 51,269 | 82,736 | 60,026 | 60,026 | 60,026 | 23,615 | 201,155 | 198,655 | 175,945 | 175,945 | 175,945 | 23,615 | 23,615 | 23,615 | 23,615 | 23,615 | 23,615 |
| UK tax on property, use (HKD) | 0 | 50,280 | 30,280 | 0 | 0 | 0 | 23,615 | 153,269 | 138,629 | 115,919 | 115,919 | 115,919 | 23,615 | 23,615 | 23,615 | 23,615 | 23,615 | 23,615 |
| **Annual net savings (HKD)** | **-605,018** | **-114,724** | **88,276** | **228,346** | **307,846** | **572,846** | **-274,633** | **136,287** | **333,927** | **466,427** | **545,927** | **810,927** | **-802,995** | **-137,845** | **152,655** | **360,155** | **484,655** | **899,655** |

---

## 6. Cumulative savings Y1 to Y10 (HK$)

Years 1 to 4 use the FIG-reduced tax where a claim is made; years 5 to 10 use the no-FIG tax.

| Year | Lon Zero | Lon Low | Lon Med | Lon 135k | Lon High | Lon Extra High | Mal Zero | Mal Low | Mal Med | Mal 135k | Mal High | Mal Extra High | HK Zero | HK Low | HK Med | HK 135k | HK High | HK Extra High |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| Y1 | -605,018 | -114,724 | 88,276 | 228,346 | 307,846 | 572,846 | -274,633 | 136,287 | 333,927 | 466,427 | 545,927 | 810,927 | -802,995 | -137,845 | 152,655 | 360,155 | 484,655 | 899,655 |
| Y2 | -1,210,035 | -229,447 | 176,553 | 456,693 | 615,693 | 1,145,693 | -549,265 | 272,575 | 667,855 | 932,855 | 1,091,855 | 1,621,855 | -1,605,989 | -275,689 | 305,311 | 720,311 | 969,311 | 1,799,311 |
| Y3 | -1,815,053 | -344,171 | 264,829 | 685,039 | 923,539 | 1,718,539 | -823,898 | 408,862 | 1,001,782 | 1,399,282 | 1,637,782 | 2,432,782 | -2,408,984 | -413,534 | 457,966 | 1,080,466 | 1,453,966 | 2,698,966 |
| Y4 | -2,420,071 | -458,895 | 353,105 | 913,385 | 1,231,385 | 2,291,385 | -1,098,531 | 545,149 | 1,335,709 | 1,865,709 | 2,183,709 | 3,243,709 | -3,211,978 | -551,378 | 610,622 | 1,440,622 | 1,938,622 | 3,598,622 |
| Y5 | -3,025,088 | -574,607 | 388,926 | 1,081,706 | 1,479,206 | 2,804,206 | -1,373,163 | 633,551 | 1,609,611 | 2,272,111 | 2,669,611 | 3,994,611 | -4,014,973 | -689,223 | 763,277 | 1,800,777 | 2,423,277 | 4,498,277 |
| Y6 | -3,630,106 | -690,320 | 424,746 | 1,250,026 | 1,727,026 | 3,317,026 | -1,647,796 | 721,952 | 1,883,512 | 2,678,512 | 3,155,512 | 4,745,512 | -4,817,968 | -827,068 | 915,932 | 2,160,932 | 2,907,932 | 5,397,932 |
| Y7 | -4,235,123 | -806,032 | 460,567 | 1,418,347 | 1,974,847 | 3,829,847 | -1,922,428 | 810,354 | 2,157,414 | 3,084,914 | 3,641,414 | 5,496,414 | -5,620,962 | -964,912 | 1,068,588 | 2,521,088 | 3,392,588 | 6,297,588 |
| Y8 | -4,840,141 | -921,745 | 496,387 | 1,586,667 | 2,222,667 | 4,342,667 | -2,197,061 | 898,755 | 2,431,315 | 3,491,315 | 4,127,315 | 6,247,315 | -6,423,957 | -1,102,757 | 1,221,243 | 2,881,243 | 3,877,243 | 7,197,243 |
| Y9 | -5,445,159 | -1,037,458 | 532,207 | 1,754,987 | 2,470,487 | 4,855,487 | -2,471,694 | 987,156 | 2,705,216 | 3,897,716 | 4,613,216 | 6,998,216 | -7,226,951 | -1,240,601 | 1,373,899 | 3,241,399 | 4,361,899 | 8,096,899 |
| Y10 | -6,050,176 | -1,153,170 | 568,028 | 1,923,308 | 2,718,308 | 5,368,308 | -2,746,326 | 1,075,558 | 2,979,118 | 4,304,118 | 5,099,118 | 7,749,118 | -8,029,946 | -1,378,446 | 1,526,554 | 3,601,554 | 4,846,554 | 8,996,554 |

---

## 6b. Runway blocks (how the two cash-burn tables are built)

Both blocks sit below the "Numeric model inputs" on the Formula validation tab, appended 25 Sep 2026. Interpretation is in [[uk-relocation-savings-comparison]] §3.

**Inputs (B69:B81).** Cash balance 1 HK$721,000, cash balance 2 HK$120,000, three card bills (1,504 + 40,839 + 10,384 = 52,727), ISAs 3,265,990, MPF 1,244,699. Derived: cash total 841,000, net cash 788,273, net cash + MPF 2,032,972, net cash + ISAs 4,054,263, net cash + ISAs + MPF 5,298,962. Cash and cards as of 25 Sep 2026; ISAs and MPF still July 2026 values.

**Table 1, full burn.**
- Annual net savings = the Zero columns' row 31 (London B31, Malvern H31, HK N31).
- Monthly burn = −annual net savings ÷ 12.
- Months = available funds ÷ monthly burn, for four pot combinations (cash; cash + MPF; cash + ISAs; cash + ISAs + MPF); years = months ÷ 12. Cash + MPF added 26 Sep 2026: the "spend the pension before the ISAs" case.
- If burn is zero or negative the cell shows "No depletion". The MPF combination shows "n/a while in HK" for the HK column because MPF is only accessible on permanent departure.

**Table 2, lean burn.**
- Lean living costs per month (B108:D108) are typed snapshots of the cashflows sheet's "Non-optional expenses excluding housing" row (London F, Malvern G, HK E), read 26 Sep 2026: 45,742.97 / 44,142.97 / 65,479.97. Not live-linked; refresh by hand after changing the cashflow budget.
- Lean annual savings = Zero annual savings + full annual living costs - lean monthly living costs x12, plus HK discretionary housing add-back B132. This preserves the exclusion of HK contents insurance. Rents, tax and resulting burn are unchanged.
- Burn and runway rows then follow Table 1's formulas on the lean figures.
- As of 26 Sep 2026 both runway tables are populated; all pot cases retain their previous results after the housing split.

**Not modelled in either:** rent voids, inflation, investment returns, a salary starting part-way, the board and car uplift the financial model applies to Malvern (see findings note §4).

---

## 7. Change log

| Date | What changed |
|---|---|
| 2026-09-26 | Housing running costs separated into savings rows18/20; full and lean living inputs exclude Housing. Hotel moved to discretionary Transport; mortgages retained in living costs. Savings and runway preserved. |
| 2026-09-25 | **Runway blocks added** to the savings sheet (full and lean, no salary), documented in §6b. HK living costs refreshed to 86,498.30/mo. |
| 2026-09-25 | **v3 model.** New savings sheet with 18 columns (135k band added), property income and letting costs in their own rows, HK Property Tax and UK property tax rows with the FIG choice, FIG expiry after four years, HK basic allowance HK$145,000, living costs from the cashflows expense totals corrected by hand. Occupied-home costs counted once, in living costs. Codex review [[uk-relocation-savings-v3-codex-review-2026-09-25]]; record [[savings-v3-review]]; tax working [[tax-rental-incomes]]. Cashflows sheet clean-up still owed. Sections 1 to 6 rebuilt. |
| 2026-08-04 | Zero-income stress columns, formula-driven cumulative rows, executive summary, four identical salary bands. |
| 2026-07-17 | Initial model from cashflows sheet row 177; UK 2026/27 tax and HK salaries tax applied. |

---

## Related

- [[uk-relocation-savings-comparison]] - findings and what the numbers mean
- [[tax-rental-incomes]] - property tax working
- [[uk-relocation-savings-v3-codex-review-2026-09-25]] - independent check of the v3 sheet
- [[uk-relocation-project]] - the project this feeds
- [[uk-move-financial-model]] - runway and pot modelling
- [[malvern-permanent-feasibility-2026-07-14]] - rules out permanent-Malvern variants
- [[uk-vs-hk-earning-comparison]] - salary band sources and tax differential
