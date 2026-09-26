---
type: reference
tags: [finance, uk-relocation, savings, earnings]
created: 2026-07-17
updated: 2026-09-26
source: UK Relocation savings comparison v3 Google Sheet
---

# UK Relocation Savings Comparison

> **What this is.** The findings readout for the **[UK Relocation savings comparison v3 Google Sheet](https://docs.google.com/spreadsheets/d/1TS-ve2WfgcBfNYrEaZCbl-4De_JdqHSqQbm_CdSZojM/edit)** (file ID 1TS-ve2WfgcBfNYrEaZCbl-4De_JdqHSqQbm_CdSZojM, tab "Formula validation"): annual and ten-year savings for London, Malvern and Hong Kong at six salary bands, now including property income, property tax and the FIG regime.
> **Why it exists.** The sheet holds numbers; this note holds what they mean. Rebuilt 25 Sep 2026 after the v3 sheet replaced the July model (which had no property tax and netted rents into living costs).
> **How it is used.** Julian reads §1 to compare locations; §3 gives runway with no salary; §4 explains why Malvern still beats Hong Kong and what living at Mum's costs. Model inputs and assumptions live in [[uk-relocation-cashflows]]; the property tax working is in [[tax-rental-incomes]]. Internal only.

**Map:** §1 executive summary · §2 the numbers · §3 cash burn tables and the formula · §4 why Malvern still beats Hong Kong, reviewing both the numbers and the burn tables, including surviving at Mum's house · §5 caveats · §6 change log · §7 how to update.

---

## 1. Executive summary (as of 26 Sep 2026)

- **Malvern is the strongest saver at every band up to £150k**, and second at £200k. It wins because both properties are let and living costs are lowest, and those two effects outweigh the UK tax bill. It still depends on living with Mum.
- **Hong Kong overtakes Malvern only at £200k**, where the HK salaries tax cap keeps most of the extra pay. HK's living costs are the highest of the three because of school fees, and university costs in years 1 to 6 are higher from HK because Sophia would pay overseas fees (intended treatment and current sheet state in the note at the end of §2; today only the two TTI columns carry a reserve).
- **London is weakest at every band.** At £75k it loses about HK$115k a year; at £135k it saves HK$228k against Malvern's HK$466k. UK tax on salary is the drag.
- **With no salary, all three burn cash:** Malvern about HK$275k a year, London HK$605k, Hong Kong HK$803k.
- **Property tax is now in the model and it matters.** Letting Pine View as a UK resident costs HK$37k a year in HK Property Tax plus UK tax that FIG removes for four years only. Letting Cecil Road from Hong Kong costs HK$24k a year in UK tax. Malvern's earlier lead has narrowed by about HK$100k a year at £135k compared with the July model.
- **The ten-year figures now step down after year four** when FIG expires. At £135k, Malvern reaches HK$4.3M over ten years, Hong Kong HK$3.6M, London HK$1.9M.

---

## 2. The numbers

Figures are HK$ per year, the sheet's "Annual net savings" row (take-home + net rents − property tax − living costs), with occupied-home running costs counted once in property rows18/20. As of 26 Sep 2026, living inputs exclude Housing but retain mortgage principal and interest. Combined costs, savings and runway are unchanged.

### Annual net savings

| Band | London | Malvern | Hong Kong |
|---|---:|---:|---:|
| Zero: GBP 0 | -605,018 | -274,633 | -802,995 |
| Low: GBP 75k | -114,724 | 136,287 | -137,845 |
| Medium: GBP 110k | 88,276 | 333,927 | 152,655 |
| Contract: GBP 135k | 228,346 | 466,427 | 360,155 |
| High: GBP 150k | 307,846 | 545,927 | 484,655 |
| Extra High: GBP 200k | 572,846 | 810,927 | 899,655 |

### TTI university scenarios (26 Sep 2026)

| Scenario         | Gross salary GBP/year | Available savings GBP/year, years1:6 | From year7 |
| ---------------- | --------------------: | -----------------------------------: | ---------: |
| TTI + UNI (T)    |               230,000 |                           100,200.54 | 115,200.54 |
| TTI(S) + UNI (U) |               250,000 |                           117,200.54 | 132,200.54 |
|                  |                       |                                      |            |

TTI(S) means an additional GBP20,000 annual schooling allowance on the GBP230,000 base, modelled as taxable gross employment income. Existing HK school fees remain in expenses. Both columns reserve GBP15,000 annually for future university over six years, totalling GBP90,000. Target/period are editable in B125:B126. This is earmarked saving, not current university expenditure. Contributions stop in year7; salary and schooling support continue. Retirement at61 is not modelled. At FX10, schooling support adds GBP17,000/year after modelled salary tax. Spreadsheet note row130 records the rationale.

### Cumulative after four years (end of the FIG window)

| Band | London | Malvern | Hong Kong |
|---|---:|---:|---:|
| Zero: GBP 0 | -2,420,071 | -1,098,531 | -3,211,978 |
| Low: GBP 75k | -458,895 | 545,149 | -551,378 |
| Medium: GBP 110k | 353,105 | 1,335,709 | 610,622 |
| Contract: GBP 135k | 913,385 | 1,865,709 | 1,440,622 |
| High: GBP 150k | 1,231,385 | 2,183,709 | 1,938,622 |
| Extra High: GBP 200k | 2,291,385 | 3,243,709 | 3,598,622 |

### Cumulative after ten years (FIG expired from year five)

| Band | London | Malvern | Hong Kong |
|---|---:|---:|---:|
| Zero: GBP 0 | -6,050,176 | -2,746,326 | -8,029,946 |
| Low: GBP 75k | -1,153,170 | 1,075,558 | -1,378,446 |
| Medium: GBP 110k | 568,028 | 2,979,118 | 1,526,554 |
| Contract: GBP 135k | 1,923,308 | 4,304,118 | 3,601,554 |
| High: GBP 150k | 2,718,308 | 5,099,118 | 4,846,554 |
| Extra High: GBP 200k | 5,368,308 | 7,749,118 | 8,996,554 |

### Tax on salary, effective rate

| Band | UK (London, Malvern) | Hong Kong | Gap |
|---|---:|---:|---:|
| £75k | 27.92% | 11.31% | UK +16.6pp |
| £110k | 34.22% | 13.12% | UK +21.1pp |
| £135k | 38.27% | 13.84% | UK +24.4pp |
| £150k | 39.14% | 14.16% | UK +25.0pp |
| £200k | 41.11% | 14.87% | UK +26.2pp |

### Tax on property, HK$ per year

| Location | HK Property Tax | UK tax on property, FIG years | UK tax on property, after FIG | Notes |
|---|---:|---:|---:|---|
| London (Pine View let) | 37,158 | 0 at £135k+; 30k to 50k at £75k to £110k | 60,026 at £135k+ | Cecil Road is the home, no UK rent |
| Malvern (both let) | 37,158 | 115,919 at £135k+ | 175,945 at £135k+ | Cecil Road tax cannot be sheltered |
| Hong Kong (Cecil Road let) | 0 | 23,615 | 23,615 | UK non-resident, personal allowance applies |

### Note: university costs (intended treatment, as of 26 Sep 2026)

University starts in year 7 of the projection. The cost should be reserved across years 1 to 6 in every column, with a UK-versus-overseas difference:

| | Per year, years 1 to 6 | Six-year total | Why |
|---|---:|---:|---|
| Every column (London, Malvern, HK) | £5,000 (HK$50,000) | £30,000 | Baseline university cost wherever Julian lives |
| HK columns, additional | £15,000 (HK$150,000) | £90,000 | If Sophia spends the four years before university overseas in HK, she loses UK home-fee status and pays overseas rates |
| HK columns, total | £20,000 (HK$200,000) | £120,000 | |

Contributions stop from year 7. The reserve is earmarked saving, not spending: it lowers available savings in years 1 to 6 but the money remains an asset.

**What the sheet does today:** only the two TTI columns carry a reserve, and only the £15,000 overseas element (HK$150,000 a year in their living expenses). No column carries the £5,000 baseline, and the other HK bands carry nothing. Until the sheet is updated, the TTI columns are not comparable with their neighbours and no column reflects the baseline cost. Applying the intended treatment would lower annual savings in years 1 to 6 by HK$50,000 in every London and Malvern column and by HK$200,000 in every HK column (HK$50,000 more than the TTI columns show now).

---

## 3. Cash burn tables (runway with no salary)

The sheet's two runway tables answer one question: **with no salary, how long do the pots last in each location?** Both take the Zero column's annual shortfall (rents in, property tax and living costs out, no salary), divide by 12 for a monthly burn, and divide the available funds by that. Pots as of 25 Sep 2026: net cash HK$788,273 (HK$841,000 less HK$52,727 of card bills); ISAs HK$3,265,990 and MPF HK$1,244,699 still at July values.

**The formula, in three steps.**

1. **Monthly burn** = living costs + letting costs + property tax − rent. Living costs are the cashflows sheet's Expenses total for that location (mortgages included); the other three are the savings sheet's property rows.
2. **Available funds** = cash balances less card bills, then optionally plus MPF, plus ISAs, or both.
3. **Runway:** months = available funds ÷ monthly burn; years = months ÷ 12.

Malvern, full budget: burn = 62,284 + 7,538 + 5,064 − 52,000 = 22,886 a month; months = 788,273 ÷ 22,886 = 34.4. The lean version repeats the three steps with the cashflows sheet's Non-optional expenses total as living costs.

**Table 1: full burn.** Combined household costs below include housing for comparability. In the sheet, living inputs exclude housing and property rows deduct it separately; the combined burn is unchanged.

| No salary, full budget                        |      London |     Malvern |       Hong Kong |
| --------------------------------------------- | ----------: | ----------: | --------------: |
| Combined household costs per month, full budget           |      70,234 |      62,284 |          86,498 |
| Letting costs and property tax, less rents in |     −19,816 |     −39,398 |         −19,582 |
| Monthly burn (after rent and property tax)    |      50,418 |      22,886 |          66,916 |
| Cash only                                     | 15.6 months | 34.4 months |     11.8 months |
| Cash + MPF | 3.4 years | 7.4 years | n/a while in HK |
| Cash + ISAs                                   |   6.7 years |  14.8 years |       5.0 years |
| Cash + ISAs + MPF                             |   8.8 years |  19.3 years | n/a while in HK |

**Table 2: lean burn.** Same, but living costs limited to what the cashflows sheet classes as non-optional (drops discretionary dining, subscriptions, cleaner, hotel and rail, and the like). Verified live values as of 26 Sep 2026:

| No salary, lean budget | London | Malvern | Hong Kong |
|---|---:|---:|---:|
| Combined household costs per month, lean budget | 47,953 | 44,143 | 69,005 |
| Letting costs and property tax, less rents in | −19,816 | −39,398 | −19,582 |
| Monthly burn (after rent and property tax) | 28,137 | 4,745 | 49,423 |
| Cash only | 28 months | 166 months | 16 months |
| Cash + MPF | 6.0 years | 36 years | n/a while in HK |
| Cash + ISAs | 12.0 years | 71 years | 6.8 years |
| Cash + ISAs + MPF | 15.7 years | 93 years | n/a while in HK |

Both tables use the same rents, letting costs and property tax; the full/lean split also preserves the exclusion of discretionary HK contents insurance. Combined household-cost rows include housing for comparison; the underlying sheet separates it. Lean burn is lower everywhere by the discretionary spend removed (about HK$22k London, HK$18k Malvern, HK$17k Hong Kong a month).

**Why Malvern's burn is so low.** Two rents come in (HK$44k a month net of letting costs) against one elsewhere, and non-mortgage living is HK$34k against London's HK$42k and Hong Kong's HK$59k, because Mum absorbs bills and there are no school fees, helper, cleaner or babysitter. The mortgages (HK$28k a month) are the same everywhere and do not separate the scenarios. In the lean case the two rents almost cover everything, so the cash barely moves.

Cash + MPF is the spend-the-pension-before-ISAs case, using HK$2,032,972. Added and verified 26 Sep 2026; all annual savings and validation results unchanged.

**How to read them.**
- The full-burn table is the planning figure. The lean table is the floor: what happens if spending is cut to essentials during a long search.
- MPF is shown for London and Malvern because leaving Hong Kong permanently unlocks it. It is retirement capital; spending it is the London-eats-the-pension point in [[uk-move-financial-model]] §0.
- HK$164k a year of every burn is Pine View principal, which builds equity. Cash runs down faster than net worth.
- Runway is held constant: no rent rises, no inflation, no investment returns, no salary part-way through.

---

## 4. Why Malvern still beats Hong Kong

At £135k, Malvern saves HK$106k a year more than Hong Kong despite paying HK$460k more tax. The decomposition:

| Effect | Malvern versus Hong Kong, HK$ per year | Why |
|---|---:|---|
| Living costs | **+290,556** | HK living costs include DBIS fees (HK$240k a year), a helper and DB clubs; Malvern has no school fees and Mum absorbs bills |
| Second rent | **+274,954** | Malvern lets Pine View as well as Cecil Road; in HK Julian lives in Pine View |
| Salary tax | −329,786 | UK income tax and NI at £135k versus HK salaries tax |
| Property tax | −129,462 | HK Property Tax plus UK tax on Cecil Road, against HK's UK non-resident tax only |
| **Net** | **+106,262** | |

The same pattern holds at every band up to £150k. At £200k the salary-tax gap widens to about HK$420k and Hong Kong pulls ahead. After year four, when FIG expires, Malvern's property tax rises by HK$60k a year and the £150k band becomes close to a tie.

**What this says about the decision:** Malvern's advantage is not tax efficiency, it is two rents and Mum's house. Remove either (live independently in Malvern, or keep Pine View for yourself) and Hong Kong wins on savings from about £110k upward.

### Surviving at Mum's house

The Malvern no-salary case from the savings sheet (26 Sep 2026). Living costs come from the cashflows sheet's expense totals; rents, letting costs, property tax, pots and runway are computed in the savings sheet.

| Malvern, no salary                                                |                   HK$ |
| ----------------------------------------------------------------- | --------------------: |
| **Monthly**                                                       |                       |
| Living costs, full budget (incl. mortgages HK$27,958)             |                62,284 |
| Rents in, gross (Pine View 27,000 + Cecil Road 25,000)            |               −52,000 |
| Letting costs, both properties                                    |                 7,538 |
| Property tax (HK Property Tax 3,097 + UK tax on Cecil Road 1,968) |                 5,064 |
| **Monthly burn, full budget**                                     |            **22,886** |
| Living costs, lean budget (non-optional only)                     |                44,143 |
| **Monthly burn, lean budget**                                     |             **4,745** |
| **Pots (cash and cards 25 Sep 2026; ISAs and MPF July 2026)**     |                       |
| Net cash                                                          |               788,273 |
| Cash + MPF                                                        |             2,032,972 |
| Cash + ISAs                                                       |             4,054,263 |
| Cash + ISAs + MPF                                                 |             5,298,962 |
| **Runway, full budget**                                           |                       |
| Cash only                                                         |           34.4 months |
| Cash + MPF                                                        |   89 months (7.4 yrs) |
| Cash + ISAs                                                       | 177 months (14.8 yrs) |
| Cash + ISAs + MPF                                                 | 232 months (19.3 yrs) |
| **Runway, lean budget**                                           |                       |
| Cash only                                                         | 166 months (13.8 yrs) |
| Cash + MPF                                                        |   428 months (36 yrs) |
| Cash + ISAs                                                       |   854 months (71 yrs) |
| Cash + ISAs + MPF                                                 | 1,117 months (93 yrs) |

**What is in the Malvern budget.** Both mortgages are inside the HK$62,284 living budget and are its largest item.

| Malvern, full budget, per month | HK$ |
|---|---:|
| Pine View mortgage: principal 13,689 + interest 12,138 | 25,827 |
| Cecil Road mortgage interest | 2,131 |
| Dining | 9,589 |
| Groceries | 6,000 |
| Transport (incl. hotel 2,000, rail 2,000, car contribution 1,000) | 6,400 |
| Travel | 3,300 |
| Bills (incl. Mum's bills 1,000, Claude and Codex 400) | 3,238 |
| Shopping, beauty, health, leisure, Amex | 5,800 |
| **Living budget** | **62,284** |
| Letting costs, both properties | +7,538 |
| Property tax | +5,064 |
| Rents in | −52,000 |
| **Burn** | **22,886** |

HK$28k of mortgage goes out each month and HK$52k of rent comes in. The rent covers the mortgages, the letting costs and the tax with HK$11k to spare; that spare plus cash pays for the HK$34k of actual living. The properties pay for themselves and part of the household, and Mum's house costs almost nothing. The burn also looks lower than it feels because HK$13.7k of the HK$22.9k is Pine View principal: in net-worth terms the loss is about HK$9k a month.

**What is in the lean budget.** Lean keeps only the rows the cashflows sheet classes as non-optional. Malvern, monthly HK$:

| Kept in the lean budget | HK$ per month |
|---|---:|
| Pine View mortgage: principal 13,689 + interest 12,138 | 25,827 |
| Cecil Road mortgage interest | 2,131 |
| Groceries | 6,000 |
| Dining, non-optional (meeting friends 2,000, with Sophia and Mum 2,000, Sophia with friends 1,000) | 5,000 |
| Bills, non-optional (Mum's bills 1,000, Claude and Codex 400, two mobiles 400, Evernote and Dropbox 77) | 1,877 |
| Shopping, non-optional (gifts 500, Sophia's clothing 400, haircuts 200) | 1,100 |
| Leisure, non-optional (Sophia pocket money 400, clubs 400, YouTube 108) | 908 |
| Health, non-optional (gym 500, toiletries 100) | 600 |
| Transport, non-optional (Sophia 200, Julian essentials 200) | 400 |
| Travel, non-optional (school trips) | 200 |
| Beauty, non-optional (haircuts) | 100 |
| **Lean living budget** | **44,143** |

| Dropped from the lean budget | HK$ per month |
|---|---:|
| Dining out and wine | 4,589 |
| Transport, discretionary (rail to London 2,000, taxis 1,000, car contribution 1,000) | 4,000 |
| UK holidays and HK trips | 3,100 |
| Subscriptions and courses (Early Adopters 600, Agentic Academy 290, Substack 200, Google AI 100, Whisperflow 100, Wills 71) | 1,361 |
| Beauty, discretionary (fillers, Botox, creams) | 825 |
| Amex fee | 667 |
| Leisure, discretionary (Disney+, ad-hoc) | 600 |
| Sophia UK sports clubs | 500 |
| Clothing | 500 |
| **Total dropped** | **18,142** |

Lean burn = 44,143 + letting costs 7,538 + property tax 5,064 − rents 52,000 = **HK$4,745 a month**. Note that lean drops the car contribution and rail as discretionary, so the board-and-car caveat below applies with more force to the lean case: a rural car is hard to call optional.

**Read.** Living at Mum's with both properties let, the rents nearly cover the mortgages and bare living, so cash barely moves. On the full budget the cash alone lasts nearly three years and cash plus ISAs almost fifteen.

**Where the Malvern figures are generous.** Three adjustments the sheet does not make:

| Malvern, no salary, per month | HK$ | Cumulative |
|---|---:|---:|
| Burn as modelled in the sheet | 22,886 | 22,886 |
| Board: sheet has HK$1,000 for Mum's bills; the financial model's honest figure is about £500 (HK$5,000) | +4,000 | 26,886 |
| Car: sheet has HK$1,000 contribution; the model's honest running cost is about £225 (HK$2,250) | +1,250 | 28,136 |
| Void allowance: one empty month per property per two-year tenancy, about HK$52,000 over 24 months | +2,170 | 30,300 |
| Commuting: hotel HK$2,000 and rail HK$2,000 exist only with a job | −4,000 | 26,300 |

Board and car are small lines, but Malvern's advantage is built from small lines, so the HK$5,250 uplift moves cash-only runway from 34 to 28 months. Malvern is the only scenario resting on two rents: a void month at Pine View costs HK$27,000 while management fees and rates continue, and HK$25,000 at Cecil Road. The honest no-salary burn is about HK$26,000 to 28,000 a month, giving 28 to 30 months on cash alone rather than 34. Still the longest of the three, but by less than the raw figure suggests.

---

## 5. Caveats

- **Malvern assumes living with Mum.** Independent Malvern accommodation, bills and a car add roughly HK$10k a month and remove most of the lead.
- **Hong Kong assumes DBIS fees of HK$20k a month** and the sheet's HK salaries tax basis (basic allowance only). Claiming the child and single-parent allowances would add about HK$48,500 a year to every HK column.
- **FIG requires 2027/28 to be the first UK-resident year** and the evidenced 12 non-resident years; the four-year window runs from then regardless of claims.
- **Property rates are 2027/28** (22/42/47% on property income, 22% interest credit); salary tax is 2026/27, unchanged for salary.
- **Rents are targets, not signed:** Pine View HK$27,000, Cecil Road £2,500 a month. Voids and repairs are not modelled.
- **No salary growth, no investment returns, no starting pot, no pension contributions.** Pension contributions at £135k+ would restore some personal allowance.
- **Living-cost inputs were corrected by hand on 25 Sep** (housing of the lived-in home restored, DB figures updated, duplicate Wills and HK Oyster removed). Housing running costs are now deducted in savings property rows; cashflow living inputs exclude Housing. Julian deleted the legacy income/burn blocks. See [[savings-v3-review]].

---

## 6. Change log

| Date | What changed |
|---|---|
| 2026-09-26 | Housing running costs separated from living inputs; hotel moved to discretionary Transport. Combined spending, savings and runway unchanged. |
| 2026-09-26 | Added TTI + UNI and TTI(S) + UNI; extra GBP20,000 schooling support treated as gross salary, existing fees and university reserve retained. |
| 2026-09-25 | **Runway tables added** (full and lean, no salary), fed by the Zero columns and the 25 Sep cash and card balances; §4 explains them. HK living costs refreshed to 86,498.30/mo (HK figures moved by HK$10). |
| 2026-09-25 | **v3 sheet replaces the July model.** New file ([UK Relocation savings comparison v3](https://docs.google.com/spreadsheets/d/1TS-ve2WfgcBfNYrEaZCbl-4De_JdqHSqQbm_CdSZojM/edit)), 18 columns (135k band added to each location), property income and letting expenses in their own rows, HK Property Tax and UK property tax rows (with and without FIG, and the "use" choice), FIG expiry after four years in the cumulative rows, HK basic allowance HK$145,000 (2026/27 onward), living costs from the cashflows expense totals with the lived-in home's housing restored. Codex adversarial review: [[uk-relocation-savings-v3-codex-review-2026-09-25]]; deliverable record [[savings-v3-review]]. Tax working: [[tax-rental-incomes]]. This note rebuilt around the new results; the July findings are superseded. |
| 2026-08-04 | Added zero-income stress columns, formula-driven cumulative rows, the Malvern false-economy caveat, and moved findings out of the sheet into this note. |
| 2026-07-17 | Initial sheet and findings note. |

---

## 7. How to update

1. Change inputs in the v3 sheet's "Numeric model inputs" block or the property rows; everything else recalculates. The three living-cost inputs are typed values from the cashflows sheet's "Expenses total excluding housing" row and must be refreshed by hand.
2. Confirm both validation rows read OK.
3. Update §2 tables here and [[uk-relocation-cashflows]] Sections 2 and 3, and add a change log row in both if the structure changed.
4. Keep findings here, not in the sheet.

---

## Related

- [[uk-relocation-cashflows]] - model inputs, assumptions and mirrored tables
- [[tax-rental-incomes]] - the property tax computation behind the tax rows
- [[uk-relocation-savings-v3-codex-review-2026-09-25]] - the independent check of the sheet
- [[uk-relocation-project]] - the project this feeds
- [[uk-move-financial-model]] - runway and pot modelling
