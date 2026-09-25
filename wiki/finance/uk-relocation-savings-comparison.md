---
type: reference
tags: [finance, uk-relocation, savings, earnings]
created: 2026-07-17
updated: 2026-09-25
source: UK Relocation savings comparison v3 Google Sheet
---

# UK Relocation Savings Comparison

> **What this is.** The findings readout for the **[UK Relocation savings comparison v3 Google Sheet](https://docs.google.com/spreadsheets/d/1TS-ve2WfgcBfNYrEaZCbl-4De_JdqHSqQbm_CdSZojM/edit)** (file ID 1TS-ve2WfgcBfNYrEaZCbl-4De_JdqHSqQbm_CdSZojM, tab "Formula validation"): annual and ten-year savings for London, Malvern and Hong Kong at six salary bands, now including property income, property tax and the FIG regime.
> **Why it exists.** The sheet holds numbers; this note holds what they mean. Rebuilt 25 Sep 2026 after the v3 sheet replaced the July model (which had no property tax and netted rents into living costs).
> **How it is used.** Julian reads §1 to compare locations; §3 explains why Malvern still beats Hong Kong. Model inputs and assumptions live in [[uk-relocation-cashflows]]; the property tax working is in [[tax-rental-incomes]]. Internal only.

**Map:** §1 bottom line · §2 the numbers · §3 why Malvern beats Hong Kong · §4 caveats · §5 change log · §6 how to update.

---

## 1. Bottom line (as of 25 Sep 2026)

- **Malvern is the strongest saver at every band up to £150k**, and second at £200k. It wins because both properties are let and living costs are lowest, and those two effects outweigh the UK tax bill. It still depends on living with Mum.
- **Hong Kong overtakes Malvern only at £200k**, where the HK salaries tax cap keeps most of the extra pay. HK's living costs are the highest of the three because of school fees.
- **London is weakest at every band.** At £75k it loses about HK$115k a year; at £135k it saves HK$228k against Malvern's HK$466k. UK tax on salary is the drag.
- **With no salary, all three burn cash:** Malvern about HK$275k a year, London HK$605k, Hong Kong HK$803k.
- **Property tax is now in the model and it matters.** Letting Pine View as a UK resident costs HK$37k a year in HK Property Tax plus UK tax that FIG removes for four years only. Letting Cecil Road from Hong Kong costs HK$24k a year in UK tax. Malvern's earlier lead has narrowed by about HK$100k a year at £135k compared with the July model.
- **The ten-year figures now step down after year four** when FIG expires. At £135k, Malvern reaches HK$4.3M over ten years, Hong Kong HK$3.6M, London HK$1.9M.

---

## 2. The numbers

Figures are HK$ per year, the sheet's "Annual net savings" row (take-home + net rents − property tax − living costs), with the occupied-home costs counted once, in living costs. Sheet state as of 25 Sep 2026: the tables below reflect the double-count correction (London UK property expenses and HK lived-in expenses set to zero in the property rows); confirm the sheet's rows 18 and 20 match before quoting it.

### Annual net savings

| Band | London | Malvern | Hong Kong |
|---|---:|---:|---:|
| Zero: GBP 0 | -605,018 | -274,633 | -802,985 |
| Low: GBP 75k | -114,724 | 136,287 | -137,835 |
| Medium: GBP 110k | 88,276 | 333,927 | 152,665 |
| Contract: GBP 135k | 228,346 | 466,427 | 360,165 |
| High: GBP 150k | 307,846 | 545,927 | 484,665 |
| Extra High: GBP 200k | 572,846 | 810,927 | 899,665 |

### Cumulative after four years (end of the FIG window)

| Band | London | Malvern | Hong Kong |
|---|---:|---:|---:|
| Zero: GBP 0 | -2,420,071 | -1,098,531 | -3,211,939 |
| Low: GBP 75k | -458,895 | 545,149 | -551,339 |
| Medium: GBP 110k | 353,105 | 1,335,709 | 610,661 |
| Contract: GBP 135k | 913,385 | 1,865,709 | 1,440,661 |
| High: GBP 150k | 1,231,385 | 2,183,709 | 1,938,661 |
| Extra High: GBP 200k | 2,291,385 | 3,243,709 | 3,598,661 |

### Cumulative after ten years (FIG expired from year five)

| Band | London | Malvern | Hong Kong |
|---|---:|---:|---:|
| Zero: GBP 0 | -6,050,176 | -2,746,326 | -8,029,846 |
| Low: GBP 75k | -1,153,170 | 1,075,558 | -1,378,346 |
| Medium: GBP 110k | 568,028 | 2,979,118 | 1,526,654 |
| Contract: GBP 135k | 1,923,308 | 4,304,118 | 3,601,654 |
| High: GBP 150k | 2,718,308 | 5,099,118 | 4,846,654 |
| Extra High: GBP 200k | 5,368,308 | 7,749,118 | 8,996,654 |

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

---

## 3. Why Malvern still beats Hong Kong

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

---

## 4. Caveats

- **Malvern assumes living with Mum.** Independent Malvern accommodation, bills and a car add roughly HK$10k a month and remove most of the lead.
- **Hong Kong assumes DBIS fees of HK$20k a month** and the sheet's HK salaries tax basis (basic allowance only). Claiming the child and single-parent allowances would add about HK$48,500 a year to every HK column.
- **FIG requires 2027/28 to be the first UK-resident year** and the evidenced 12 non-resident years; the four-year window runs from then regardless of claims.
- **Property rates are 2027/28** (22/42/47% on property income, 22% interest credit); salary tax is 2026/27, unchanged for salary.
- **Rents are targets, not signed:** Pine View HK$27,000, Cecil Road £2,500 a month. Voids and repairs are not modelled.
- **No salary growth, no investment returns, no starting pot, no pension contributions.** Pension contributions at £135k+ would restore some personal allowance.
- **Living-cost inputs were corrected by hand on 25 Sep** (housing of the lived-in home restored, DB figures updated, duplicate Wills and HK Oyster removed). The cashflows Google Sheet has not yet been cleaned up to match; see [[uk-relocation-cashflows]].

---

## 5. Change log

| Date | What changed |
|---|---|
| 2026-09-25 | **v3 sheet replaces the July model.** New file ([UK Relocation savings comparison v3](https://docs.google.com/spreadsheets/d/1TS-ve2WfgcBfNYrEaZCbl-4De_JdqHSqQbm_CdSZojM/edit)), 18 columns (135k band added to each location), property income and letting expenses in their own rows, HK Property Tax and UK property tax rows (with and without FIG, and the "use" choice), FIG expiry after four years in the cumulative rows, HK basic allowance HK$145,000 (2026/27 onward), living costs from the cashflows expense totals with the lived-in home's housing restored. Codex adversarial review: [[uk-relocation-savings-v3-codex-review-2026-09-25]]; deliverable record [[savings-v3-review]]. Tax working: [[tax-rental-incomes]]. This note rebuilt around the new results; the July findings are superseded. |
| 2026-08-04 | Added zero-income stress columns, formula-driven cumulative rows, the Malvern false-economy caveat, and moved findings out of the sheet into this note. |
| 2026-07-17 | Initial sheet and findings note. |

---

## 6. How to update

1. Change inputs in the v3 sheet's "Numeric model inputs" block or the property rows; everything else recalculates. The three living-cost inputs are typed values from the cashflows sheet's "Expenses total" row and must be refreshed by hand.
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
