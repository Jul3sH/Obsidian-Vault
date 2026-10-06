---
type: reference
tags: [finance, uk-relocation, savings, earnings]
created: 2026-07-17
updated: 2026-10-06
source: UK Relocation savings comparison v3 Google Sheet (living-cost inputs from UK Relocation Expenses)
---

# UK Relocation Savings Comparison

> **What this is.** The self-contained companion to the **[UK Relocation savings comparison v3 Google Sheet](https://docs.google.com/spreadsheets/d/1TS-ve2WfgcBfNYrEaZCbl-4De_JdqHSqQbm_CdSZojM/edit)** (file ID 1TS-ve2WfgcBfNYrEaZCbl-4De_JdqHSqQbm_CdSZojM, tab "Formula validation"): annual and ten-year savings for London, Malvern and Hong Kong at six salary bands, now including property income, property tax, the FIG regime and, from 27 Sep 2026, the university reserve.
> **Why it exists.** The sheet holds numbers; this note holds what they mean. Rebuilt 25 Sep 2026 after the v3 sheet replaced the July model (which had no property tax and netted rents into living costs).
> **How it is used.** Julian reads §1 to compare locations; §3 gives runway with no salary; §4 explains why Malvern still beats Hong Kong and what living at Mum's costs. §6 holds the model inputs and assumptions and §7 mirrors the sheet's tables and runway mechanics, so nothing here depends on another note; the itemised living costs are in [[uk-relocation-expenses]] and the property tax working in [[tax-rental-incomes]]. Internal only.

**Map:** §1 executive summary · §2 the numbers · §3 cash burn tables and the formula · §4 why Malvern still beats Hong Kong, reviewing both the numbers and the burn tables, including surviving at Mum's house · §5 caveats · §6 model inputs and assumptions · §7 mirrored sheet tables and runway mechanics · §8 change log · §9 how to update · §10 sheet changes for Codex (6 Oct 2026).

---

## 1. Executive summary (as of 6 Oct 2026)

- **Malvern is the strongest saver at every band up to £150k**, and second at £200k. It wins because both properties are let and living costs are lowest, and those two effects outweigh the UK tax bill. It still depends on living with Mum.
- **Hong Kong overtakes Malvern only at £200k**, where the HK salaries tax cap keeps most of the extra pay. HK's living costs are the highest of the three because of school fees, and university costs in years 1 to 6 are higher from HK because Sophia would pay overseas fees. The university reserve is in the sheet (27 Sep 2026): GBP 40,000 in every column plus GBP 120,000 extra in the HK columns, both over six years (detail in the note at the end of §2). On the after-reserve figures Malvern stays ahead at £200k in years 1 to 6 (HK$744k against HK$633k) and Hong Kong only edges ahead over ten years (HK$7.40M against HK$7.35M).
- **London is weakest at every band.** At £75k it loses about HK$115k a year; at £135k it saves HK$228k against Malvern's HK$466k. UK tax on salary is the drag.
- **With no salary, all three burn cash:** including the university reserve for years 1 to 6, Malvern about HK$341k a year, London HK$672k, Hong Kong HK$1,070k. After year 6 the burn drops to HK$275k, HK$605k and HK$803k.
- **Property tax is now in the model and it matters.** Letting Pine View as a UK resident costs HK$37k a year in HK Property Tax plus UK tax that FIG removes for four years only. Letting Cecil Road from Hong Kong costs HK$24k a year in UK tax. Malvern's earlier lead has narrowed by about HK$100k a year at £135k compared with the July model.
- **The ten-year figures now step down after year four** when FIG expires. At £135k, Malvern reaches HK$3.9M over ten years, Hong Kong HK$2.0M, London HK$1.5M, after the university reserve.
- **TTI downside and exit scenarios (6 Oct 2026).** Over ten years, the TTI worst case (job lost after year 3, a year with no pay, back to Malvern on £135k, overseas university fees) reaches HK$3.73M, close to staying in Malvern on £135k (HK$3.90M). Two years of TTI then Malvern on £135k, keeping home fees, reaches HK$5.40M on TTI 230 and HK$5.74M on TTI 250. Ten years on TTI 230: HK$9.92M. Columns W, X and Y in the sheet; §2 table.
- **The university reserve is now in the model (27 Sep 2026).** GBP 40,000 over six years in every column, plus GBP 120,000 in the HK columns (GBP 160,000 in Hong Kong). It is earmarked saving, not spending: it lowers available savings in years 1 to 6 but the money remains an asset. On it, the TTI 230 return reaches HK$5.3M at six years against HK$4.3M for the TTI role done from Malvern (the £200k stand-in).

---

## 2. The numbers

Figures are HK$ per year, the sheet's "Annual net savings before university reserve" row (take-home + net rents − property tax − living costs), with occupied-home running costs counted once in living expenses. From 27 Sep 2026 the sheet also carries the university reserve and the available savings after it (second table below). As of 26 Sep 2026, property rows18/20 contain letting expenses only; living inputs include housing and mortgage payments. Combined costs, savings and runway are unchanged.

### Annual net savings before university reserve

| Band | London | Malvern | Hong Kong |
|---|---:|---:|---:|
| Zero: GBP 0 | -605,018 | -274,633 | -802,995 |
| Low: GBP 75k | -114,724 | 136,287 | -137,845 |
| Medium: GBP 110k | 88,276 | 333,927 | 152,655 |
| Contract: GBP 135k | 228,346 | 466,427 | 360,155 |
| High: GBP 150k | 307,846 | 545,927 | 484,655 |
| Extra High: GBP 200k | 572,846 | 810,927 | 899,655 |

### Annual available savings after reserve, years 1 to 6

| Band | London | Malvern | Hong Kong |
|---|---:|---:|---:|
| Zero: GBP 0 | -671,684 | -341,299 | -1,069,661 |
| Low: GBP 75k | -181,390 | 69,621 | -404,511 |
| Medium: GBP 110k | 21,610 | 267,261 | -114,011 |
| Contract: GBP 135k | 161,680 | 399,761 | 93,489 |
| High: GBP 150k | 241,180 | 479,261 | 217,989 |
| Extra High: GBP 200k | 506,180 | 744,261 | 632,989 |

The reserve is HK$66,667 a year in London and Malvern and HK$266,667 a year in Hong Kong, in years 1 to 6 only; it stops after year 6, when available savings return to the before-reserve figures.

### Cumulative after four years (end of the FIG window, after the university reserve)

| Band | London | Malvern | Hong Kong |
|---|---:|---:|---:|
| Zero: GBP 0 | -2,686,737 | -1,365,197 | -4,278,645 |
| Low: GBP 75k | -725,561 | 278,483 | -1,618,045 |
| Medium: GBP 110k | 86,439 | 1,069,043 | -456,045 |
| Contract: GBP 135k | 646,719 | 1,599,043 | 373,955 |
| High: GBP 150k | 964,719 | 1,917,043 | 871,955 |
| Extra High: GBP 200k | 2,024,719 | 2,977,043 | 2,531,955 |

### Cumulative after ten years (FIG expired from year five, after the university reserve)

| Band | London | Malvern | Hong Kong |
|---|---:|---:|---:|
| Zero: GBP 0 | -6,450,176 | -3,146,326 | -9,629,946 |
| Low: GBP 75k | -1,553,170 | 675,558 | -2,978,446 |
| Medium: GBP 110k | 168,028 | 2,579,118 | -73,446 |
| Contract: GBP 135k | 1,523,308 | 3,904,118 | 2,001,554 |
| High: GBP 150k | 2,318,308 | 4,699,118 | 3,246,554 |
| Extra High: GBP 200k | 4,968,308 | 7,349,118 | 7,396,554 |

Restored 27 Sep 2026: both tables were lost in an edit earlier the same day and are rebuilt here from the sheet's cumulative rows (reserve excluded in years 1 to 6).

### TTI scenarios (27 Sep 2026; relabelled 6 Oct 2026)

| Scenario | Gross salary (GBP) | Net take-home (HK$) | Living expenses (HK$) | Savings before reserve (HK$) | University reserve, years 1 to 6 (HK$) | Available savings, years 1 to 6 (GBP/yr) | Available savings from year 7 (GBP/yr) |
|---|---:|---:|---:|---:|---:|---:|---:|
| HK, TTI 230 | 230,000 | 1,955,000 | 1,037,980 | 1,152,005 | 266,667 | 88,533.9 | 115,200.5 |
| HK, TTI 250 | 250,000 | 2,125,000 | 1,037,980 | 1,322,005 | 266,667 | 105,533.9 | 132,200.5 |

**TTI 230** is a permanent salary of HK$2,300,000 (GBP 230,000). **TTI 250** is HK$2,500,000 (GBP 250,000), standing for either of two packages (Julian, 6 Oct 2026): the same permanent salary plus HK$200,000 a year schooling support, taxed as salary; or the HK$2,500,000 consulting fee previously quoted. *The sheet taxes both at the 15% salaries tax standard rate; a consulting fee may be taxed differently, which is not modelled.* The column labels were renamed on 6 Oct 2026 from "TTI + UNI" and "TTI(S) + UNI": the university reserve is in every column, so it no longer needs naming. In both, the existing HK school fees stay in living expenses, which are now 1,037,980 in every HK column including these two. The university reserve is the shared HK figure of GBP 160,000 over six years (GBP 40,000 baseline plus GBP 120,000 additional), HK$266,667 a year in the sheet's reserve row, not inside living expenses; contributions stop in year 7. GBP figures are the sheet's HK$ at FX 10. Retirement at 61 is not modelled.

### HK-return comparison at 6, 8 and 10 years

| Scenario | What it stands for (Julian's words) | Year 6 | Year 8 | Year 10 |
|---|---|---:|---:|---:|
| Malvern 135k | What he is likely to earn as a contractor based in Malvern | 2,278,512 | 3,091,315 | 3,904,118 |
| London 135k | Contractor earnings if circumstances change and he goes to London | 850,026 | 1,186,667 | 1,523,308 |
| Malvern Extra High (£200k) | A TTI role on current salary, done from the UK, Malvern base | 4,345,512 | 5,847,315 | 7,349,118 |
| London Extra High (£200k) | A TTI role on current salary, done from the UK, London base | 2,917,026 | 3,942,667 | 4,968,308 |
| HK, TTI 230 (£230k) | If he goes to Hong Kong on the permanent salary. After the HK university reserve (GBP 160,000 over six years), which stops in year 7 | 5,312,032 | 7,616,043 | 9,920,054 |
| HK, TTI 250 (£250k) | If he goes to Hong Kong with schooling in the package (HK$200k/yr, taxed as salary), or on the HK$2.5M consulting fee. Same reserve | 6,332,032 | 8,976,043 | 11,620,054 |
| HK, TTI worst case (lost after year 3) | Goes to Hong Kong on TTI 230, loses the job after year 3, no salary in year 4 while Sophia finishes GCSEs, back to Malvern on £135k from year 5; overseas university rates in years 1 to 6 (column W, 6 Oct 2026) | 1,985,876 | 2,918,731 | 3,731,534 |
| HK, TTI 250 then Malvern (two-year exit) | Goes to Hong Kong on TTI 250 for two years, then back to Malvern on £135k from year 3 before Sophia's GCSEs; home-fee university reserve (column X, 6 Oct 2026) | 4,109,720 | 4,922,523 | 5,735,326 |
| HK, TTI 230 then Malvern (two-year exit) | As above on TTI 230 (column Y, 6 Oct 2026) | 3,769,720 | 4,582,523 | 5,395,326 |

All rows are read from the sheet's cumulative table (FIG for years 1 to 4, no-FIG tax from year 5, university reserve excluded in years 1 to 6, all columns). The 18 band columns are mirrored in §7; the two TTI columns are the sheet's columns T ("TTI 230") and U ("TTI 250"). As of 6 Oct 2026 both header blocks label T and U "TTI 230" and "TTI 250". Columns V and W were added by Julian, cumulative gaps in HK$ (checked 6 Oct 2026 against columns K, M and U): **V "TTI 250 - MAL 135"** is TTI 250 in Hong Kong minus a normal contract salary in Malvern (column U minus Mal 135k, column K), HK$4.05M at year 6 and HK$7.72M at year 10. **W, the TTI worst case (redefined by Julian 6 Oct 2026; formula-driven from 6 Oct 2026):** Julian goes to Hong Kong on TTI 230, loses the job after year 3, earns nothing in year 4 while Sophia finishes her GCSEs in Hong Kong, and moves back to Malvern on £135k in year 5. Sophia no longer qualifies for UK home university fees, so the overseas-rate reserve (HK$266,667 a year) applies in years 1 to 6. Annual basis: years 1 to 3, column T after reserve (885,339); year 4, HK Zero after reserve (column N, -1,069,661); years 5 and 6, Mal 135k before reserve with FIG (466,427) less the overseas reserve (199,760); years 7 and 8, Mal 135k with FIG, no reserve (466,427); years 9 and 10, Mal 135k without FIG (406,401). FIG in years 5 to 8 assumes the return restarts the four-year window after more than ten years non-resident (Julian confirmed the assumption 6 Oct; adviser check advisable); without it, year 10 is about HK$240k lower. Cumulative (read back 6 Oct 2026): 885,339 / 1,770,677 / 2,656,016 / 1,586,355 / 1,786,116 / 1,985,876 / 2,452,304 / 2,918,731 / 3,325,133 / 3,731,534. As of 6 Oct 2026: V's year 1 formula returns 655,578. W formulas differ from the listed rounded expectations by HK$0 to HK$3, within the HK$5 allowance.

| Ratio | Year 6 | Year 8 | Year 10 |
|---|---:|---:|---:|
| HK TTI 230 vs Malvern 135k | 2.3x | 2.5x | 2.5x |
| HK TTI 230 vs Malvern Extra High | 1.2x | 1.3x | 1.4x |
| HK TTI 250 vs Malvern 135k | 2.8x | 2.9x | 3.0x |
| HK TTI 250 vs Malvern Extra High | 1.5x | 1.5x | 1.6x |
| Gap, HK TTI 230 minus Malvern Extra High (HK$) | 0.97M | 1.77M | 2.57M |
| Gap, HK TTI 250 minus Malvern Extra High (HK$) | 1.99M | 3.13M | 4.27M |

The £200k band stands in for a TTI role done from the UK. The TTI salary modelled here is £230k, so the two Extra High rows already assume £30k a year less for being UK-based. If TTI paid the full £230k from the UK, those rows would be higher.

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

### What is deductible where (as of 27 Sep 2026)

The rule the sheet follows: **letting costs of a let property are deductible in the UK; occupied-home costs and mortgage principal are never deductible; Hong Kong ignores actual costs and uses its own formula.** Cell references are to the savings sheet's Formula validation tab.

| Cost | Sits in | UK tax on rental profit | HK Property Tax (Pine View let) |
|---|---|---|---|
| Cecil Road letting: Brinkleys management £3,240, rent protection £432, buildings insurance £469 = £4,140/yr | Row 18, only when Cecil Road is let | Deductible | Not applicable (UK property) |
| Pine View letting: DB management 24,648, rates 14,348, buildings insurance 3,300, agent fee 6,750 (HK$13,500 per two-year tenancy) = HK$49,046/yr | Row 20, only when Pine View is let | Deductible, government rent included if it is in the bill | Only owner-paid rates (B59) are deducted; a flat 20% allowance replaces every other cost. Tax = 15% x 80% x (rent less rates) = HK$37,158 |
| Mortgage interest: Cecil Road £2,556 (B57), Pine View £14,566 (B58) | Cashflow living costs, every scenario | Not deductible; a 22% tax credit instead, capped at the property tax due | Not deductible |
| Mortgage principal: Pine View HK$164,268/yr | Cashflow living costs, every scenario | Never | Never |
| Occupied-home costs: council tax, contents and buildings insurance at Cecil Road when living there; DB management, rates and insurance at Pine View when living there | Cashflow living costs (Housing), rows 18/20 set to zero for that home | Never | Never |

- HK Property Tax paid is credited against the UK tax on the same rent, capped at that UK tax, so the sheet's "UK tax on property" rows are after the credit. Working: [[tax-rental-incomes]].
- Open check: B59 assumes the HK$14,348 bill is rates only. If it also contains government rent, HK Property Tax rises by at most HK$646/yr; UK deductibility is unaffected. Confirm from the RVD demand note.

### University reserve (in the sheet from 27 Sep 2026)

University starts in year 7 of the projection. The cost is reserved across years 1 to 6 in every column, with a UK-versus-overseas difference:

| | Per year, years 1 to 6 | Six-year total | Why |
|---|---:|---:|---|
| Every column (London, Malvern, HK) | GBP 6,667 (HK$66,667) | GBP 40,000 | Baseline university cost wherever Julian lives |
| HK columns, additional | GBP 20,000 (HK$200,000) | GBP 120,000 | If Sophia spends the four years before university overseas in HK, she loses UK home-fee status and pays overseas rates |
| HK columns, total | GBP 26,667 (HK$266,667) | GBP 160,000 | |

Contributions stop from year 7. The reserve is earmarked saving, not spending: it lowers available savings in years 1 to 6 but the money remains an asset.

**What the sheet does (27 Sep 2026):** every column carries an "Annual university reserve, years 1 to 6" row and an "Annual available savings after reserve, years 1 to 6" row. The reserve is excluded from available and cumulative savings in years 1 to 6 and the full before-reserve savings are added from year 7; the runway tables include it in the years 1 to 6 burn. The old arrangement (a GBP 15,000 overseas element inside the two TTI columns' living expenses only) is gone.

Confirmed by Julian, 27 Sep 2026: the HK reserve total is GBP 160,000 (40,000 baseline plus 120,000 additional), as the sheet carries it. which was intended.

---

## 3. Cash burn tables (runway with no salary)

The sheet's two runway tables answer one question: **with no salary, how long do the pots last in each location?** Both take the Zero column's annual shortfall (rents in; property tax, living costs and, in years 1 to 6, the university reserve out; no salary), divide by 12 for a monthly burn, and divide the available funds by that. From 27 Sep 2026 the runway is piecewise: the reserve is in the burn for years 1 to 6 and drops out after. Pots as of 25 Sep 2026: net cash HK$788,273 (HK$841,000 less HK$52,727 of card bills); ISAs HK$3,265,990 and MPF HK$1,244,699 still at July values.

**The formula, in three steps.**

1. **Monthly burn** = living costs + letting costs + property tax − rent + university reserve (years 1 to 6 only). Living costs are the cashflows sheet's Expenses total for that location (mortgages included); letting costs, property tax and rent are the savings sheet's property rows; the reserve is HK$5,556 a month in London and Malvern and HK$22,222 in Hong Kong.
2. **Available funds** = cash balances less card bills, then optionally plus MPF, plus ISAs, or both.
3. **Runway:** piecewise. If a pot runs out within six years, months = available funds ÷ monthly burn including reserve. Otherwise years = 6 + (available funds − six years of that burn) ÷ the annual burn after year 6, when the reserve has stopped; months = years × 12.

Malvern, full budget: burn = 62,284 + 7,538 + 5,064 − 52,000 + 5,556 reserve = 28,442 a month; months = 788,273 ÷ 28,442 = 27.7. The lean version repeats the three steps with the cashflows sheet's Non-optional expenses total as living costs.

**Table 1: full burn.** Combined household costs below include housing for comparability. Living inputs include occupied-home housing; property rows deduct letting expenses separately.

| No salary, full budget | London | Malvern | Hong Kong |
|---|---:|---:|---:|
| Combined household costs per month, full budget | 70,234 | 62,284 | 86,498 |
| Letting costs and property tax, less rents in | −19,816 | −39,398 | −19,582 |
| University reserve per month, years 1 to 6 | 5,556 | 5,556 | 22,222 |
| Monthly burn including reserve, years 1 to 6 | 55,974 | 28,442 | 89,138 |
| Cash only | 14.1 months | 27.7 months | 8.8 months |
| Cash + MPF | 3.0 years | 6.0 years | n/a while in HK |
| Cash + ISAs | 6.0 years | 13.3 years | 3.8 years |
| Cash + ISAs + MPF | 8.1 years | 17.8 years | n/a while in HK |

After year 6 the burn drops to the pre-reserve figure (50,418 / 22,886 / 66,916 a month) and the runway formula is piecewise: pots that outlast six years run down at the lower burn from year 7.

**Table 2: lean burn.** Same, but living costs limited to what the cashflows sheet classes as non-optional (drops discretionary dining, subscriptions, cleaner, hotel and rail, and the like). Verified live values as of 27 Sep 2026, university reserve included:

| No salary, lean budget | London | Malvern | Hong Kong |
|---|---:|---:|---:|
| Combined household costs per month, lean budget | 47,953 | 44,143 | 69,005 |
| Letting costs and property tax, less rents in | −19,816 | −39,398 | −19,582 |
| University reserve per month, years 1 to 6 | 5,556 | 5,556 | 22,222 |
| Monthly burn including reserve, years 1 to 6 | 33,692 | 10,300 | 71,645 |
| Cash only | 23.4 months | 81.8 months | 11.0 months |
| Cash + MPF | 5.0 years | 28.7 years | n/a while in HK |
| Cash + ISAs | 10.8 years | 64.2 years | 4.7 years |
| Cash + ISAs + MPF | 14.5 years | 86.0 years | n/a while in HK |

After year 6 the lean burn drops to the pre-reserve figure (28,137 / 4,745 / 49,423 a month) and the same piecewise formula applies.

Both tables use the same rents, letting costs and property tax; the full/lean split also preserves the exclusion of discretionary HK contents insurance. The living inputs include occupied-home housing. Lean burn is lower everywhere by the discretionary spend removed (about HK$22k London, HK$18k Malvern, HK$17k Hong Kong a month).

**Why Malvern's burn is so low.** Two rents come in (HK$44k a month net of letting costs) against one elsewhere, and non-mortgage living is HK$34k against London's HK$42k and Hong Kong's HK$59k, because Mum absorbs bills and there are no school fees, helper, cleaner or babysitter. The mortgages (HK$28k a month) are the same everywhere and do not separate the scenarios. In the lean case the two rents almost cover everything, so the cash barely moves.

Cash + MPF is the spend-the-pension-before-ISAs case, using HK$2,032,972. Added 26 Sep 2026; re-verified 27 Sep 2026 with the university reserve in the years 1 to 6 burn; every validation check on the sheet reads OK.

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

These figures are before the university reserve. After it (27 Sep 2026) Malvern's lead in years 1 to 6 widens to HK$306k, because the HK reserve is HK$200k a year larger. The same pattern holds at every band up to £150k. At £200k the salary-tax gap widens to about HK$420k and Hong Kong pulls ahead before the reserve; after it Malvern stays ahead in years 1 to 6 and Hong Kong only edges ahead over ten years. After year four, when FIG expires, Malvern's property tax rises by HK$60k a year and the £150k band becomes close to a tie.

**What this says about the decision:** Malvern's advantage is not tax efficiency, it is two rents and Mum's house. Remove either (live independently in Malvern, or keep Pine View for yourself) and Hong Kong wins on savings from about £110k upward before the university reserve; with the HK reserve HK$200k a year larger, the crossover sits higher in years 1 to 6.

### Surviving at Mum's house

The Malvern no-salary case from the savings sheet (27 Sep 2026, university reserve included in years 1 to 6). Living costs come from the cashflows sheet's expense totals; rents, letting costs, property tax, pots and runway are computed in the savings sheet.

| Malvern, no salary | HK$ |
|---|---:|
| **Monthly** | |
| Living costs, full budget (incl. mortgages HK$27,958) | 62,284 |
| Rents in, gross (Pine View 27,000 + Cecil Road 25,000) | −52,000 |
| Letting costs, both properties | 7,538 |
| Property tax (HK Property Tax 3,097 + UK tax on Cecil Road 1,968) | 5,064 |
| University reserve, years 1 to 6 (GBP 40,000 over six years) | 5,556 |
| **Monthly burn, full budget** | **28,442** |
| Living costs, lean budget (non-optional only) | 44,143 |
| **Monthly burn, lean budget** | **10,300** |
| **Pots (cash and cards 25 Sep 2026; ISAs and MPF July 2026)** | |
| Net cash | 788,273 |
| Cash + MPF | 2,032,972 |
| Cash + ISAs | 4,054,263 |
| Cash + ISAs + MPF | 5,298,962 |
| **Runway, full budget** | |
| Cash only | 27.7 months |
| Cash + MPF | 71.5 months (6.0 yrs) |
| Cash + ISAs | 159.7 months (13.3 yrs) |
| Cash + ISAs + MPF | 214.1 months (17.8 yrs) |
| **Runway, lean budget** | |
| Cash only | 81.8 months (6.8 yrs) |
| Cash + MPF | 344.2 months (28.7 yrs) |
| Cash + ISAs | 770.2 months (64.2 yrs) |
| Cash + ISAs + MPF | 1,032.5 months (86.0 yrs) |

Burns include the university reserve for years 1 to 6; after year 6 they fall to 22,886 (full) and 4,745 (lean) and the runway is piecewise.

**What is in the Malvern budget.** Two versions of the same budget: full is everything in the cashflows sheet's Malvern column; lean keeps only the rows the sheet classes as non-optional. Both mortgages are inside both versions and are the largest item.

| Malvern, budget, per month | Lean HK$ | Full HK$ |
|---|---:|---:|
| Pine View mortgage: principal 13,689 + interest 12,138 | 25,827 | 25,827 |
| Cecil Road mortgage interest | 2,131 | 2,131 |
| Dining (lean: meeting friends, with Sophia and Mum, Sophia's friends; full adds dining out and wine) | 5,000 | 9,589 |
| Groceries | 6,000 | 6,000 |
| Transport (lean: Sophia and essentials; full adds rail 2,000, taxis 1,000, car contribution 1,000) | 400 | 4,400 |
| Travel (lean: school trips; full adds UK holidays and HK trips) | 200 | 3,300 |
| Bills (lean: Mum's bills 1,000, Claude and Codex 400, mobiles, Evernote, Dropbox; full adds subscriptions and courses) | 1,877 | 3,238 |
| Hotel, two nights a week | 0 | 2,000 |
| Shopping, beauty, health, leisure, Amex (lean: gifts, Sophia's clothing, haircuts, gym, pocket money, clubs) | 2,708 | 5,800 |
| **Living budget** | **44,143** | **62,284** |
| Letting costs, both properties | +7,538 | +7,538 |
| Property tax | +5,064 | +5,064 |
| Rents in | −52,000 | −52,000 |
| University reserve, years 1 to 6 | +5,556 | +5,556 |
| **Burn** | **10,300** | **28,442** |

On either budget HK$28k of mortgage goes out each month and HK$52k of rent comes in. The rent covers the mortgages, the letting costs and the tax with HK$11k to spare. On the full budget that spare plus cash pays for HK$34k of actual living, leaving a burn of HK$22,886 before the university reserve and HK$28,442 with it; on the lean budget actual living is HK$16k, so the rents cover almost all of it and the burn is HK$4,745 before the reserve, HK$10,300 with it. The properties pay for themselves and part of the household, and Mum's house costs almost nothing. Both burns look lower than they feel because HK$13.7k a month is Pine View principal and HK$5.6k is the earmarked university reserve: in net-worth terms the full-budget loss is about HK$9k a month and the lean budget is net-worth positive. Lean also drops the car contribution and the rail ticket as discretionary, which is where the board-and-car caveat below bites hardest: a rural car is hard to call optional.

**Read.** Living at Mum's with both properties let, the rents nearly cover the mortgages and bare living, so cash barely moves. On the full budget, with the university reserve in the burn, the cash alone lasts 27.7 months (a little over two years) and cash plus ISAs 13.3 years.

**Where the Malvern figures are generous.** Three adjustments the sheet does not make, starting from the sheet's years 1 to 6 burn with the university reserve (27 Sep 2026):

| Malvern, no salary, per month | HK$ | Cumulative |
|---|---:|---:|
| Burn as modelled in the sheet, including reserve, years 1 to 6 | 28,442 | 28,442 |
| Board: sheet has HK$1,000 for Mum's bills; the financial model's honest figure is about £500 (HK$5,000) | +4,000 | 32,442 |
| Car: sheet has HK$1,000 contribution; the model's honest running cost is about £225 (HK$2,250) | +1,250 | 33,692 |
| Void allowance: one empty month per property per two-year tenancy, about HK$52,000 over 24 months | +2,170 | 35,862 |
| Commuting: hotel HK$2,000 and rail HK$2,000 exist only with a job | −4,000 | 31,862 |

Board and car are small lines, but Malvern's advantage is built from small lines, so the HK$5,250 uplift moves cash-only runway from 27.7 to 23.4 months. Malvern is the only scenario resting on two rents: a void month at Pine View costs HK$27,000 while management fees and rates continue, and HK$25,000 at Cecil Road. The university reserve is now in the sheet's burn for years 1 to 6 (27 Sep 2026), so it no longer needs adding here. The honest no-salary burn is about HK$32,000 to 36,000 a month in years 1 to 6, giving 22 to 25 months on cash alone rather than 27.7. Still the longest of the three, but by less than the raw figure suggests.

---

## 5. Caveats

- **Malvern assumes living with Mum.** Independent Malvern accommodation, bills and a car add roughly HK$10k a month and remove most of the lead.
- **Hong Kong assumes DBIS fees of HK$20k a month** and the sheet's HK salaries tax basis (basic allowance only). Claiming the child and single-parent allowances would add about HK$48,500 a year to every HK column.
- **FIG requires 2027/28 to be the first UK-resident year** and the evidenced 12 non-resident years; the four-year window runs from then regardless of claims.
- **Property rates are 2027/28** (22/42/47% on property income, 22% interest credit); salary tax is 2026/27, unchanged for salary.
- **Rents are targets, not signed:** Pine View HK$27,000, Cecil Road £2,500 a month. Voids and repairs are not modelled.
- **No salary growth, no investment returns, no starting pot, no pension contributions.** Pension contributions at £135k+ would restore some personal allowance.
- **Living-cost inputs were corrected by hand on 25 Sep** (housing of the lived-in home restored, DB figures updated, duplicate Wills and HK Oyster removed). Occupied-home housing is included in cashflow living inputs; savings property rows contain letting expenses only. Julian deleted the legacy income/burn blocks. See [[savings-v3-review]].

---

## 6. Model inputs and assumptions

Moved here from the former model companion on 27 Sep 2026 so this note and the sheet are self-contained. Living-cost itemisation stays in [[uk-relocation-expenses]].

### The two sheets

| Sheet | Role | Tab to use |
|---|---|---|
| [UK Relocation savings comparison v3](https://docs.google.com/spreadsheets/d/1TS-ve2WfgcBfNYrEaZCbl-4De_JdqHSqQbm_CdSZojM/edit) | The model: salary, tax, property rows, savings, cumulative, runway | "Formula validation" (formula-driven) |
| [UK Relocation Expenses](https://docs.google.com/spreadsheets/d/1HP-4Gm7TUqftlnCiXFqe34Wpp4torBt3NOZOb9BG4U4/edit) (renamed 27 Sep 2026; was UK Relocation Cashflows) | Living costs by location, itemised | "Cashflow comparison"; row 168 (full) and row 164 (lean) feed the savings sheet's living-cost inputs by hand |

**Do not use the burn rates in [[uk-move-financial-model]] section 0 as inputs. Those figures are superseded.**

### Property income by scenario

| Scenario | Julian lives in | Let | Rent in the model | Letting costs in the model | Lived-in home costs |
|---|---|---|---|---|---|
| Hong Kong | Pine View | Cecil Road | £30,000/yr | £4,140/yr | DB management, rates and insurance: HK$44,722/yr in living costs (expenses sheet) |
| London | Cecil Road | Pine View | HK$324,000/yr | HK$49,046/yr | Council tax, buildings and contents insurance: GBP2,652/yr in living costs (expenses sheet) |
| Malvern | Mum's | Both | £30,000 + HK$324,000 | £4,140 + HK$49,046 | None; hotel HK$2,000/mo for hybrid commuting stays in living costs |

Mortgage interest (Pine View HK$12,138/mo, Cecil Road £213/mo) and Pine View principal (HK$13,689/mo) sit inside living costs in every scenario. The principal builds equity but reduces cash.

### Assumptions

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
| Letting costs, Pine View | Annual basis: DB management 24,648 + rates 14,348 (B59) + buildings insurance 3,300 + agent fee 6,750 (HK$13,500 per two-year tenancy): HK$49,046/yr. Monthly equivalents 2,054 / 1,196 / 275 are rounded; use the annual figures |
| Letting costs, Cecil Road | Brinkleys £3,240 + rent protection £432 + buildings insurance £469 = £4,141 by arithmetic; sheet input retained at £4,140 (£1 rounding) |
| Living costs | Expenses sheet "Expenses total" row 168 per location (full) and "Non-optional expenses total" row 164 (lean); mortgage payments retained; held constant, no inflation. Itemisation: [[uk-relocation-expenses]] |
| University reserve | GBP 40,000 over years 1 to 6 in every column, plus GBP 120,000 in the HK columns; earmarked, excluded from available savings; contributions stop after year 6 (in the sheet from 27 Sep 2026) |
| Salary growth, investment returns, pension, MPF, starting pot | Not modelled |

### Living-cost inputs (HK$ per month)

Typed snapshots, not live links. Include occupied-home housing and mortgage payments.

| Monthly HKD | London | Malvern | Hong Kong |
|---|---:|---:|---:|
| Full living inputs, B66:B68, from expenses row 168 | 70,234.47 | 62,284.47 | 86,498.30 |
| Lean living inputs, B110:D110, from expenses row 164 | 47,952.97 | 44,142.97 | 69,004.97 |

---

## 7. Mirrored sheet tables and runway mechanics

Mirror of the sheet's Formula validation tab so any agent can resume or review without re-deriving. Values as of 27 Sep 2026; university reserve excluded in years 1 to 6; TTI columns T and U are in §2.

### Salary, tax and annual net savings (HK$ per year)

Annual net savings before university reserve = net take-home + (UK property income − UK property running costs) × 10 + HK property income − HK property running costs − HK Property Tax − UK tax on property (use) − living costs. Annual available savings after reserve, years 1 to 6 = that less the annual university reserve (66,666.67 in London and Malvern, 266,666.67 in Hong Kong, shown rounded below).

| | Lon Zero | Lon Low | Lon Med | Lon 135k | Lon High | Lon Extra High | Mal Zero | Mal Low | Mal Med | Mal 135k | Mal High | Mal Extra High | HK Zero | HK Low | HK Med | HK 135k | HK High | HK Extra High |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| Gross salary (GBP) | 0 | 75,000 | 110,000 | 135,000 | 150,000 | 200,000 | 0 | 75,000 | 110,000 | 135,000 | 150,000 | 200,000 | 0 | 75,000 | 110,000 | 135,000 | 150,000 | 200,000 |
| Gross salary (HKD) | 0 | 750,000 | 1,100,000 | 1,350,000 | 1,500,000 | 2,000,000 | 0 | 750,000 | 1,100,000 | 1,350,000 | 1,500,000 | 2,000,000 | 0 | 750,000 | 1,100,000 | 1,350,000 | 1,500,000 | 2,000,000 |
| UK property income (GBP) | 0 | 0 | 0 | 0 | 0 | 0 | 30,000 | 30,000 | 30,000 | 30,000 | 30,000 | 30,000 | 30,000 | 30,000 | 30,000 | 30,000 | 30,000 | 30,000 |
| UK letting expenses (GBP) | 0 | 0 | 0 | 0 | 0 | 0 | 4,140 | 4,140 | 4,140 | 4,140 | 4,140 | 4,140 | 4,140 | 4,140 | 4,140 | 4,140 | 4,140 | 4,140 |
| HK property income (HKD) | 324,000 | 324,000 | 324,000 | 324,000 | 324,000 | 324,000 | 324,000 | 324,000 | 324,000 | 324,000 | 324,000 | 324,000 | 0 | 0 | 0 | 0 | 0 | 0 |
| HK letting expenses (HKD) | 49,046 | 49,046 | 49,046 | 49,046 | 49,046 | 49,046 | 49,046 | 49,046 | 49,046 | 49,046 | 49,046 | 49,046 | 0 | 0 | 0 | 0 | 0 | 0 |
| Income tax (HKD) | 0 | 174,320 | 334,320 | 469,530 | 537,030 | 762,030 | 0 | 174,320 | 334,320 | 469,530 | 537,030 | 762,030 | 0 | 84,850 | 144,350 | 186,850 | 212,350 | 297,350 |
| NI / HK salaries tax (HKD) | 0 | 35,106 | 42,106 | 47,106 | 50,106 | 60,106 | 0 | 35,106 | 42,106 | 47,106 | 50,106 | 60,106 | 0 | 0 | 0 | 0 | 0 | 0 |
| Net take-home (HKD) | 0 | 540,574 | 723,574 | 833,364 | 912,864 | 1,177,864 | 0 | 540,574 | 723,574 | 833,364 | 912,864 | 1,177,864 | 0 | 665,150 | 955,650 | 1,163,150 | 1,287,650 | 1,702,650 |
| Living expenses (HKD), including occupied housing | 842,814 | 842,814 | 842,814 | 842,814 | 842,814 | 842,814 | 747,414 | 747,414 | 747,414 | 747,414 | 747,414 | 747,414 | 1,037,980 | 1,037,980 | 1,037,980 | 1,037,980 | 1,037,980 | 1,037,980 |
| HK Property Tax (HKD) | 37,158 | 37,158 | 37,158 | 37,158 | 37,158 | 37,158 | 37,158 | 37,158 | 37,158 | 37,158 | 37,158 | 37,158 | 0 | 0 | 0 | 0 | 0 | 0 |
| UK tax on property, no FIG (HKD) | 0 | 51,269 | 82,736 | 60,026 | 60,026 | 60,026 | 23,615 | 201,155 | 198,655 | 175,945 | 175,945 | 175,945 | 23,615 | 23,615 | 23,615 | 23,615 | 23,615 | 23,615 |
| UK tax on property, use (HKD) | 0 | 50,280 | 30,280 | 0 | 0 | 0 | 23,615 | 153,269 | 138,629 | 115,919 | 115,919 | 115,919 | 23,615 | 23,615 | 23,615 | 23,615 | 23,615 | 23,615 |
| **Annual net savings before university reserve (HKD)** | **-605,018** | **-114,724** | **88,276** | **228,346** | **307,846** | **572,846** | **-274,633** | **136,287** | **333,927** | **466,427** | **545,927** | **810,927** | **-802,995** | **-137,845** | **152,655** | **360,155** | **484,655** | **899,655** |
| Annual university reserve, years 1 to 6 (HKD) | 66,667 | 66,667 | 66,667 | 66,667 | 66,667 | 66,667 | 66,667 | 66,667 | 66,667 | 66,667 | 66,667 | 66,667 | 266,667 | 266,667 | 266,667 | 266,667 | 266,667 | 266,667 |
| **Annual available savings after reserve, years 1 to 6 (HKD)** | **-671,684** | **-181,390** | **21,610** | **161,680** | **241,180** | **506,180** | **-341,299** | **69,621** | **267,261** | **399,761** | **479,261** | **744,261** | **-1,069,661** | **-404,511** | **-114,011** | **93,489** | **217,989** | **632,989** |

The two TTI columns (T and U) carry the same three rows: before reserve 1,152,005 / 1,322,005, reserve 266,667, after reserve 885,339 / 1,055,339 (see §2).

### Cumulative savings Y1 to Y10 (HK$)

Years 1 to 4 use the FIG-reduced tax where a claim is made; years 5 to 10 use the no-FIG tax. Years 1 to 6 accumulate the available savings after the university reserve; from year 7 the full before-reserve savings are added. Values as of 27 Sep 2026.

| Year | Lon Zero | Lon Low | Lon Med | Lon 135k | Lon High | Lon Extra High | Mal Zero | Mal Low | Mal Med | Mal 135k | Mal High | Mal Extra High | HK Zero | HK Low | HK Med | HK 135k | HK High | HK Extra High |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| Y1 | -671,684 | -181,390 | 21,610 | 161,680 | 241,180 | 506,180 | -341,299 | 69,621 | 267,261 | 399,761 | 479,261 | 744,261 | -1,069,661 | -404,511 | -114,011 | 93,489 | 217,989 | 632,989 |
| Y2 | -1,343,369 | -362,781 | 43,219 | 323,359 | 482,359 | 1,012,359 | -682,599 | 139,241 | 534,521 | 799,521 | 958,521 | 1,488,521 | -2,139,323 | -809,023 | -228,023 | 186,977 | 435,977 | 1,265,977 |
| Y3 | -2,015,053 | -544,171 | 64,829 | 485,039 | 723,539 | 1,518,539 | -1,023,898 | 208,862 | 801,782 | 1,199,282 | 1,437,782 | 2,232,782 | -3,208,984 | -1,213,534 | -342,034 | 280,466 | 653,966 | 1,898,966 |
| Y4 | -2,686,737 | -725,561 | 86,439 | 646,719 | 964,719 | 2,024,719 | -1,365,197 | 278,483 | 1,069,043 | 1,599,043 | 1,917,043 | 2,977,043 | -4,278,645 | -1,618,045 | -456,045 | 373,955 | 871,955 | 2,531,955 |
| Y5 | -3,358,421 | -907,940 | 55,593 | 748,373 | 1,145,873 | 2,470,873 | -1,706,496 | 300,218 | 1,276,278 | 1,938,778 | 2,336,278 | 3,661,278 | -5,348,306 | -2,022,556 | -570,056 | 467,444 | 1,089,944 | 3,164,944 |
| Y6 | -4,030,106 | -1,090,320 | 24,746 | 850,026 | 1,327,026 | 2,917,026 | -2,047,796 | 321,952 | 1,483,512 | 2,278,512 | 2,755,512 | 4,345,512 | -6,417,968 | -2,427,068 | -684,068 | 560,932 | 1,307,932 | 3,797,932 |
| Y7 | -4,635,123 | -1,206,032 | 60,567 | 1,018,347 | 1,574,847 | 3,429,847 | -2,322,428 | 410,354 | 1,757,414 | 2,684,914 | 3,241,414 | 5,096,414 | -7,220,962 | -2,564,912 | -531,412 | 921,088 | 1,792,588 | 4,697,588 |
| Y8 | -5,240,141 | -1,321,745 | 96,387 | 1,186,667 | 1,822,667 | 3,942,667 | -2,597,061 | 498,755 | 2,031,315 | 3,091,315 | 3,727,315 | 5,847,315 | -8,023,957 | -2,702,757 | -378,757 | 1,281,243 | 2,277,243 | 5,597,243 |
| Y9 | -5,845,158 | -1,437,457 | 132,208 | 1,354,988 | 2,070,488 | 4,455,488 | -2,871,693 | 587,157 | 2,305,217 | 3,497,717 | 4,213,217 | 6,598,217 | -8,826,951 | -2,840,601 | -226,101 | 1,641,399 | 2,761,899 | 6,496,899 |
| Y10 | -6,450,176 | -1,553,170 | 168,028 | 1,523,308 | 2,318,308 | 4,968,308 | -3,146,326 | 675,558 | 2,579,118 | 3,904,118 | 4,699,118 | 7,349,118 | -9,629,946 | -2,978,446 | -73,446 | 2,001,554 | 3,246,554 | 7,396,554 |

### Runway blocks (how the two cash-burn tables are built)

Both blocks sit below the "Numeric model inputs" on the Formula validation tab, appended 25 Sep 2026. Interpretation is in §3.

**Inputs (balances B71:B77, pot combinations B80:B83).** Cash balance 1 HK$721,000, cash balance 2 HK$120,000, three card bills (1,504 + 40,839 + 10,384 = 52,727), ISAs 3,265,990, MPF 1,244,699. Derived: cash total 841,000, net cash 788,273, net cash + MPF 2,032,972, net cash + ISAs 4,054,263, net cash + ISAs + MPF 5,298,962. Cash and cards as of 25 Sep 2026; ISAs and MPF still July 2026 values. Full living inputs are B66:B68. The university reserve inputs (baseline target GBP 40,000, additional HK target GBP 120,000, years contributing 6, and the derived annual HK reserve) sit in the "University reserve inputs" block below the lean block.

**Table 1, full burn.**
- Annual savings, years 1 to 6 = the Zero columns' "Annual available savings after reserve, years 1 to 6" row (London, Malvern, HK); after year 6 = the "Annual net savings before university reserve" row.
- Monthly burn including reserve, years 1 to 6 = −annual available savings ÷ 12. Post-reserve annual burn = −annual net savings before reserve.
- Runway is piecewise, for four pot combinations (cash; cash + MPF; cash + ISAs; cash + ISAs + MPF). If the pot depletes within six years, months = pot ÷ monthly burn including reserve. Otherwise years = 6 + (pot − six years of that burn) ÷ post-reserve annual burn, and months = years × 12. Cash + MPF added 26 Sep 2026: the "spend the pension before the ISAs" case.
- If burn is zero or negative the cell shows "No depletion". The MPF combination shows "n/a while in HK" for the HK column because MPF is only accessible on permanent departure.

**Table 2, lean burn.**
- Lean living costs per month (B110:D110) are typed snapshots of the expenses sheet's "Non-optional expenses total" row164 (London F, Malvern G, HK E), read 26 Sep 2026: 47,952.97 / 44,142.97 / 69,004.97. Not live-linked; refresh by hand after changing the expenses budget.
- Lean annual savings before reserve = Zero annual savings before reserve + full annual living costs - lean monthly living costs x12. Lean available savings, years 1 to 6 = that less the annual university reserve: −404,306 / −123,601 / −859,741. HK contents insurance is excluded through the lean living input. Rents, tax and resulting burn are unchanged.
- Burn and runway rows then follow Table 1's piecewise formulas on the lean figures.
- As of 27 Sep 2026 both runway tables are populated on the after-reserve figures for years 1 to 6 and the before-reserve figure after year 6; every validation check on the sheet reads OK.

**Not modelled in either:** rent voids, inflation, investment returns, a salary starting part-way, the board and car uplift the financial model applies to Malvern (see §4).

---

## 8. Change log

| Date | What changed |
|---|---|
| 2026-10-06 | Added [Savings chart](https://docs.google.com/spreadsheets/d/1TS-ve2WfgcBfNYrEaZCbl-4De_JdqHSqQbm_CdSZojM/edit?gid=106202607), a line graph of Y1 to Y10 cumulative HKD savings for E, K, M, V, W, X and Y. Chart reads the source ranges directly, so updates automatically. Existing cells unchanged. |
| 2026-10-06 | Executive summary: TTI downside and exit scenarios bullet added (W, X, Y at year 10); heading redated. |
| 2026-10-06 | Applied revised §10 changes 1 to 7 including 6b: exact headers, V/W/X/Y formulas, both assumptions. All 41 cells read back; 40 validation checks OK. Maximum differences W HK$3, X/Y HK$4, permitted rounding. §2 W/X/Y figures refreshed. New assumption row inserted after W assumption; existing formulas adjusted automatically, results and formats preserved. |
| 2026-10-06 | Applied §10 changes 1 to 5 to Formula validation: headers V/W and lower T/U, V Y1 formula, W Y1 to Y10 formulas, and assumption A56:B56. All 17 cells read back exactly; all 40 validation checks OK. W differs from expectations by at most HK$3 (rounding); other cells, formats and wrapping unchanged. |
| 2026-10-06 | Column Y specified (TTI 230 for two years, then Malvern 135k): expected year 10 HK$5.40M. |
| 2026-10-06 | Column X specified (TTI 250 for two years, then Malvern 135k from year 3; home-fee university reserve): expected year 10 HK$5.74M; added to the 6/8/10-year table and §10. |
| 2026-10-06 | Column W redefined as the TTI worst case (job lost after year 3, back to Malvern 135k in year 5, overseas university rates years 1 to 6); added to the 6/8/10-year table. Year 10 HK$3.73M against Malvern 135k HK$3.90M. |
| 2026-10-06 | Columns T and U relabelled TTI 230 and TTI 250 to match the v3 sheet (the university reserve is in every column, so "+ UNI" dropped); TTI 250 defined as salary plus HK$200k schooling, or the HK$2.5M consulting fee (Julian). New sheet columns V and W noted. All sheet references confirmed as v3. |
| 2026-09-27 | University reserve built into the sheet by Codex (GBP 40,000 every column plus GBP 120,000 HK, over six years, earmarked): new reserve and after-reserve rows, cumulative and runway recalculated piecewise. Every table in this note re-read from the sheet. HK total confirmed by Julian as 160,000 later the same day. |
| 2026-09-27 | HK-return comparison block: HK rows re-derived with a £120k university reserve over six years (degree plus possible masters, Julian's instruction). Sheet B125 still 90,000, to update. UK rows carry no university reserve; noted as a like-for-like gap. |
| 2026-09-27 | Added the HK-return comparison block at 6, 8 and 10 years (Malvern and London at 135k and Extra High; TTI + UNI and TTI(S) + UNI derived from annual figures). Mirrors the executive summary in HK-Return-BRAIND. |
| 2026-09-27 | Absorbed the model companion: §6 inputs and assumptions, §7 mirrored tables and runway mechanics moved in from the former uk-relocation-cashflows note, which is now [[uk-relocation-expenses]] and covers the expenses sheet only. |
| 2026-09-27 | Added the "What is deductible where" table to §2 after the Claude cross-check, so this note carries the letting-versus-occupied and UK-versus-HK rule itself. |
| 2026-09-26 | Restored occupied-home housing to living inputs and letting-only property rows. Full/lean runway, tax and savings unchanged. HK actual letting expenses feed UK overseas-rental profit; HK Property Tax uses its separate statutory calculation. |
| 2026-09-26 | Earlier, superseded: Housing running costs separated from living inputs; hotel moved to discretionary Transport. Combined spending, savings and runway unchanged. |
| 2026-09-26 | Added TTI + UNI and TTI(S) + UNI; extra GBP20,000 schooling support treated as gross salary, existing fees and university reserve retained. |
| 2026-09-25 | **Runway tables added** (full and lean, no salary), fed by the Zero columns and the 25 Sep cash and card balances; §4 explains them. HK living costs refreshed to 86,498.30/mo (HK figures moved by HK$10). |
| 2026-09-25 | **v3 sheet replaces the July model.** New file ([UK Relocation savings comparison v3](https://docs.google.com/spreadsheets/d/1TS-ve2WfgcBfNYrEaZCbl-4De_JdqHSqQbm_CdSZojM/edit)), 18 columns (135k band added to each location), property income and letting expenses in their own rows, HK Property Tax and UK property tax rows (with and without FIG, and the "use" choice), FIG expiry after four years in the cumulative rows, HK basic allowance HK$145,000 (2026/27 onward), living costs from the cashflows expense totals with the lived-in home's housing restored. Codex adversarial review: [[uk-relocation-savings-v3-codex-review-2026-09-25]]; deliverable record [[savings-v3-review]]. Tax working: [[tax-rental-incomes]]. This note rebuilt around the new results; the July findings are superseded. |
| 2026-08-04 | Added zero-income stress columns, formula-driven cumulative rows, the Malvern false-economy caveat, and moved findings out of the sheet into this note. |
| 2026-07-17 | Initial sheet and findings note. |

---

## 9. How to update

1. Change inputs in the v3 sheet's "Numeric model inputs" block or the property rows; everything else recalculates. The full and lean living-cost inputs are typed values from the expenses sheet's rows 168 and 164 and must be refreshed by hand.
2. University reserve: edit the baseline and HK-additional targets and the years in the reserve inputs block; the reserve row and everything below recalculates.
3. Confirm both validation rows read OK.
4. Update the §2, §6 and §7 tables here and add a change log row; if a living cost changed, update [[uk-relocation-expenses]] too.
5. Keep findings here, not in the sheet.

---

## 10. Sheet changes for Codex, 6 Oct 2026

**Applied, 6 Oct 2026 (changes 1, 2, 3, 4, 5, 6, 6b and 7).** Sheet: [UK Relocation savings comparison v3](https://docs.google.com/spreadsheets/d/1TS-ve2WfgcBfNYrEaZCbl-4De_JdqHSqQbm_CdSZojM/edit), tab "Formula validation". Identify rows by the label in column A, not by row number. Year rows Y1 to Y10 are the cumulative block at the top. Row labels used below:

- **RB** = "Annual net savings before university reserve (HKD)"
- **RR** = "Annual university reserve, years 1 to 6 (HKD)"
- **RA** = "Annual available savings after reserve, years 1 to 6 (HKD)"
- **TN** = "UK tax on property, no FIG (HKD)"; **TF** = "UK tax on property, FIG claimed (HKD)"

| # | Cells | Change |
|---|---|---|
| 1 | Top header row, columns V and W | V: "TTI 250 - MAL 135". W: "TTI worst case (lost after Y3)". |
| 2 | Lower header row (the one starting "Lon Zero" above "Gross salary (GBP)"), columns T and U | T: "TTI 230" (was "TTI + UNI"). U: "TTI 250" (was "TTI(S) + UNI"). |
| 3 | V, Y1 (blank today) | Formula: U(Y1) minus K(Y1), the same pattern as V's Y2 to Y10. Expected 655,578. |
| 4 | W, Y1 to Y10 (typed values today) | Replace with formulas, cumulative: Y1 = T[RA]. Y2 = W(Y1) + T[RA]. Y3 = W(Y2) + T[RA]. Y4 = W(Y3) + N[RA]. Y5 = W(Y4) + K[RB] - T[RR]. Y6 = W(Y5) + K[RB] - T[RR]. Y7 = W(Y6) + K[RB]. Y8 = W(Y7) + K[RB]. Y9 = W(Y8) + K[RB] - (K[TN] - K[TF]). Y10 = W(Y9) + K[RB] - (K[TN] - K[TF]). |
| 5 | Assumptions block, new row at the end | Label "TTI worst case (column W)". Value: "Hong Kong on TTI 230 for years 1 to 3; job lost; no salary in year 4 in Hong Kong while Sophia finishes GCSEs; back to Malvern on 135k from year 5. Overseas university reserve (HK column rate) in years 1 to 6, because Sophia loses UK home-fee status. FIG assumed in years 5 to 8 (return after more than ten years non-resident restarts the window); no FIG in years 9 and 10." |

| 6 | X, header and Y1 to Y10 (new column) | Header: "TTI 250 2 yrs then MAL 135". Formulas, cumulative: Y1 = U[RB] - K[RR]. Y2 = X(Y1) + U[RB] - K[RR]. Y3 to Y6 = previous + K[RA]. Y7 to Y10 = previous + K[RB] - (K[TN] - K[TF]). |
| 6b | Y, header and Y1 to Y10 (new column) | Header: "TTI 230 2 yrs then MAL 135". Same formulas as X with column T in place of U: Y1 = T[RB] - K[RR]. Y2 = Y(Y1) + T[RB] - K[RR]. Y3 to Y6 = previous + K[RA]. Y7 to Y10 = previous + K[RB] - (K[TN] - K[TF]). |
| 7 | Assumptions block, new row after change 5 | Label "TTI two-year exit (columns X and Y)". Value: "Hong Kong for years 1 and 2 (X on TTI 250, Y on TTI 230), then Malvern on 135k from year 3 with no gap (the planned exit before Sophia's GCSE courses). Home-fee university reserve (HK$66,667 a year) in years 1 to 6, because the return comes in time to keep UK home-fee status. FIG assumed in years 3 to 6 (return after more than ten years non-resident restarts the window); no FIG in years 7 to 10." |

**Expected values for readback (column W, Y1 to Y10):** 885,339 / 1,770,677 / 2,656,016 / 1,586,355 / 1,786,115 / 1,985,875 / 2,452,302 / 2,918,729 / 3,325,130 / 3,731,531. **Expected values for readback (column Y, Y1 to Y10):** 1,085,338 / 2,170,677 / 2,570,437 / 2,970,197 / 3,369,958 / 3,769,718 / 4,176,119 / 4,582,520 / 4,988,921 / 5,395,322. **Expected values for readback (column X, Y1 to Y10):** 1,255,338 / 2,510,677 / 2,910,437 / 3,310,197 / 3,709,958 / 4,109,718 / 4,516,119 / 4,922,520 / 5,328,921 / 5,735,322. Small rounding differences (under HK$5) are acceptable; anything larger is a wrong reference.

**Leave unchanged:** every other cell, formats and wrapping. Validation rows must still read "OK".

**Readback, 6 Oct 2026:** changes 1, 2, 3, 4, 5, 6, 6b and 7 complete. All 41 written cells match; all 40 validation checks read OK. V Y1 = 655,578. W Y1 to Y10: 885,339 / 1,770,677 / 2,656,016 / 1,586,355 / 1,786,116 / 1,985,876 / 2,452,304 / 2,918,731 / 3,325,133 / 3,731,534. X: 1,255,339 / 2,510,677 / 2,910,438 / 3,310,199 / 3,709,960 / 4,109,720 / 4,516,122 / 4,922,523 / 5,328,925 / 5,735,326. Y: 1,085,339 / 2,170,677 / 2,570,438 / 2,970,199 / 3,369,960 / 3,769,720 / 4,176,122 / 4,582,523 / 4,988,925 / 5,395,326. Maximum differences from expectations: W HK$3, X and Y HK$4, all permitted rounding. Assumption row 57 inserted immediately after the W assumption. Before/after A1:Z160/A1:Z161 comparison confirms other entered values unchanged except automatic formula-reference adjustments; existing numeric results, formats and wrapping preserved.

## Related

- [[uk-relocation-expenses]] - the expenses sheet: itemised living costs by location, full and lean totals, refresh procedure
- [[tax-rental-incomes]] - the property tax computation behind the tax rows
- [[uk-relocation-savings-v3-codex-review-2026-09-25]] - the independent check of the sheet
- [[uk-relocation-project]] - the project this feeds
- [[uk-move-financial-model]] - runway and pot modelling
