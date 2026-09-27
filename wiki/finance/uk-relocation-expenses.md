---
type: reference
tags: [finance, uk-relocation, expenses, living-costs]
created: 2026-07-17
updated: 2026-09-27
source: UK Relocation Expenses Google Sheet
---

# UK Relocation Expenses

> **What this is.** The companion to the **[UK Relocation Expenses Google Sheet](https://docs.google.com/spreadsheets/d/1HP-4Gm7TUqftlnCiXFqe34Wpp4torBt3NOZOb9BG4U4/edit)** (file ID 1HP-4Gm7TUqftlnCiXFqe34Wpp4torBt3NOZOb9BG4U4, tab "Cashflow comparison"): the itemised monthly living budget for Hong Kong, London and Malvern, and the two totals that feed the savings model.
> **Why it exists.** The sheet holds the line items; this note says what is in each location's column, which rows feed the savings sheet, and how to refresh them. Slimmed 27 Sep 2026 from the former uk-relocation-cashflows note, whose model content moved to [[uk-relocation-savings-comparison]] §6 and §7.
> **How it is used.** Open only when a living cost may have changed. Julian's primary surface is [[uk-relocation-savings-comparison]]. Internal only.

**Map:** §1 sheet structure · §2 the totals · §3 what differs by location · §4 what is not in this sheet · §5 refresh procedure · §6 change log.

---

## 1. Sheet structure

- Columns: A category, B item, C cost estimate (working notes, not summed), D HK last 12 months (actuals, not summed), **E Hong Kong, F London, G Malvern** (the three scenario budgets), H notes.
- Every category has a non-optional block and a discretionary block, each with its own subtotal, then a category total.
- Rows 164, 166 and 168 sum the scenario columns: **Non-optional expenses total (lean), Discretionary expenses total, Expenses total (full)**.
- Rows 170 to 179 hold the cost and tax rules panel added 27 Sep 2026 (occupied versus letting costs, count once, mortgage treatment, refresh instructions, rates check), matching the panel in the savings sheet.
- Sheet renamed 27 Sep 2026 from "UK Relocation Cashflows" (earlier "Relocation Cash Flows"); the file ID and all links are unchanged.

## 2. The totals (HK$ per month, as of 27 Sep 2026)

| Row | HK (E) | London (F) | Malvern (G) | Feeds |
|---|---:|---:|---:|---|
| 164 Non-optional total (lean) | 69,004.97 | 47,952.97 | 44,142.97 | Savings sheet B108:D108 |
| 166 Discretionary total | 17,493.33 | 22,281.50 | 18,141.50 | Nothing; the gap between lean and full |
| 168 Expenses total (full) | 86,498.30 | 70,234.47 | 62,284.47 | Savings sheet B64:B66 |

Both totals include the occupied home's running costs and both mortgages. Verified against the itemised rows on 27 Sep 2026 ([[savings-v3-review]]).

## 3. What differs by location (HK$ per month)

| Item | Hong Kong | London | Malvern |
|---|---:|---:|---:|
| Occupied-home housing | 3,726.83 (DB management 2,054, rates 1,196, buildings 275, contents 201.83 discretionary) | 2,210 (council tax 1,640, contents 180, buildings 390) | 0 |
| School fees | 20,000 (DBIS) | 0 | 0 |
| Home help (discretionary) | helper 3,000 | cleaner 4,600, babysitter 2,150 | 0 |
| Bills, non-optional | 2,514.17 | 3,477.17 | 1,877.17 (includes Mum's bills 1,000) |
| Transport | 2,025 (essentials 400, taxis 1,000, Octopus 625) | 3,790 (essentials 400, taxis 1,000, car 1,890, Oyster 500) | 6,400 (essentials 400, taxis 1,000, car contribution 1,000, rail 2,000, hotels 2,000) |
| Travel | 2,200 | 3,300 | 3,300 |
| Health and fitness | 2,225 (DB clubs) | 1,100 | 1,100 |
| Medical | 700 | 0 | 0 |
| Bills, discretionary other | 4,860.83 | 8,110.83 | 1,360.83 |

Identical in every column: Pine View principal 13,689; mortgage interest 14,268.80 (Pine View 12,138, Cecil Road 2,130.80); dining 9,589; groceries 6,000; shopping 1,600; beauty 925; leisure 1,508; Amex 666.67.

Caveats carried from [[uk-relocation-savings-comparison]] §4: Malvern's rail, hotel and Octopus/Oyster lines exist only with a job; Mum's board and the car contribution are below the financial model's honest figures.

## 4. What is not in this sheet

- **Letting costs of a let property** (Cecil Road £4,140/yr, Pine View HK$49,046/yr) live in the savings sheet rows 18 and 20, never here. The column C lines "HK Lettings fee 1,125" and "UK Letting/management 2,460" are stale working notes with no scenario values; ignore or clear them.
- **Rent, property tax, salary tax and runway** are all in the savings sheet.
- **Transport labels:** "Weekly Octopus when working" and "Weekly Oyster 1-3 when working" are summed in the discretionary subtotal whatever their category label says.

## 5. Refresh procedure

1. Change the line item in column E, F or G. Subtotals and rows 164 to 168 recalculate.
2. Type the new row 168 values into savings sheet B64:B66 (London F, Malvern G, HK E) and row 164 into B108:D108 in the same order. They are snapshots, not links.
3. Confirm the savings sheet's validation rows still read OK, then update §2 and §3 here and the living-cost inputs in [[uk-relocation-savings-comparison]] §6.

## 6. Change log

| Date | What changed |
|---|---|
| 2026-09-27 | Note renamed from uk-relocation-cashflows and slimmed to the expenses sheet only; model inputs, assumptions, mirrored tables and runway mechanics moved to [[uk-relocation-savings-comparison]] §6 and §7. Google Sheet renamed to UK Relocation Expenses. |
| 2026-09-26 | Occupied-home housing restored to living expenses; obsolete excluding-housing outputs 169/170 cleared; rules panel to follow. Earlier the same day, superseded: Housing separated out and hotels moved to discretionary Transport (the hotel move stands). |
| 2026-09-25 | Duplicate Wills and HK Oyster removed; occupied-home housing corrected (HK 2,054 / 1,196 / 275, London 1,640 / 180 / 390); let-property charges removed from scenario columns. |
| 2026-07-17 | Note created as the companion to the then 9-column earnings model built from this sheet's row 177. |

---

## Related

- [[uk-relocation-savings-comparison]] - the savings model: findings, inputs, assumptions, mirrored tables, runway
- [[savings-v3-review]] - deliverable record and verification trail
- [[uk-relocation-project]] - the project this feeds
- [[uk-move-financial-model]] - July runway and pot modelling, superseded for burn rates
