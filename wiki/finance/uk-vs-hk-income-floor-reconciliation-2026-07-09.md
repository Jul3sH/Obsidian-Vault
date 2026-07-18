---
type: analysis
status: reviewed
created: 2026-07-09
reviewed: 2026-07-09
authority: claude-reviewed
currency: mixed (HKD + GBP, 10:1)
decision: UK Relocation Decision
tags: [finance, uk-relocation, cost-comparison, income-floor]
---

# UK vs HK Income Floor Reconciliation - 2026-07-09

> **Reviewed 2026-07-09 (Claude hostile review):** two workbook bugs corrected; symmetric HK net-worth rows added. The corrected numbers change the headline: HK$100k/month gross and the UK £120k role are the **same ~£120k gross** and produce **broadly comparable surpluses**. HK is slightly ahead on the recent-trend denominator, but trails on the 12-month mean. The UK's real floor advantage is a **lower break-even gross** (~£77.5k vs ~£90-95k-equivalent in HK on recent actuals), not clearly more surplus at equal pay. Full review: [[uk-vs-hk-income-floor-reconciliation-claude-review-2026-07-09]].

## Key Takeaways

- The focused spreadsheet has been created: [[uk-vs-hk-income-floor-reconciliation-2026-07-09.xlsx]].
- The workbook now opens on a **Side by Side** sheet: Hong Kong and UK costs are shown in adjacent columns by category, with a variance column and validation notes for each row.
- **Housing corrected 2026-07-10:** the old visual row compared HK housing at ~£2,900 against UK housing at ~£1,289, which mixed owner costs, rent offsets, mortgage principal, and agency fees. The workbook now has a **Housing Mechanics** sheet and the side-by-side row uses net monthly property cash: HK-stay ~£1,172/mo vs London ~£1,231/mo. London is ~£59/mo worse on ongoing housing before the one-off DB letting agency fee (~£1,100).
- **Helper / cleaner / babysitting corrected 2026-07-10:** babysitting was not explicitly modelled. The workbook now splits the old HK Bills line into household utilities, Domestic help / cleaner, and Babysitting / childcare cover. HK helper cost is shown separately at HK$3,000/mo (~£300); UK cleaner remains a £300/mo placeholder; UK babysitting is a separate £0 placeholder until Julian sets an expected monthly amount.
- The workbook uses the canonical [[money-tracker|Money Tracker]] / [[budget|Budget]] categories as the category spine, not the simplified relocation-model categories.
- **Reviewed finding (corrected):** "HK has no cheap floor" is wrong and must go. HK$100k/month gross (= ~£120k/year, the same as the UK "strong" role) produces a **similar cash surplus to UK £120k** once Cecil Road rent is offset. It beats UK £120k on recent-trend actuals, but trails on the 12-month mean.
- **The UK's real floor edge** is a **lower break-even gross** (survive on ~£77.5k in the UK vs ~£90-95k-equivalent in HK on recent actuals) - not more surplus at equal pay.
- "Weak recovery floor" is still accurate relative to a **senior** HK role (HK$125-150k), but not relative to the UK £120k role; the two are equivalent money.
- The biggest open uncertainties: which HK actuals denominator to trust (trend 83,940 vs mean 92,196 = 8,256 HKD/mo swing), and whether London runs a car (would shift the UK burden by £300-500/mo).
- **Decision impact: none.** This narrows the UK floor gap further and reinforces the [[uk-vs-hk-earning-comparison]] conclusion that income is not a decisive reason to move.

## Why This Exists

Julian challenged a mismatch:

> If HK and London cost roughly the same, why does HK$100k/month in Hong Kong look unviable while £120k/year in the UK looks comfortable?

The first-pass answer is: the old narrative was mixing layers:

- HK actuals versus UK forecast.
- HK gross salary versus UK net salary.
- HK outgoings without consistently offsetting Cecil Road rent.
- Cash-flow burn versus net-worth burn.
- Budget provisions versus actual recurring spend.

## Workbook Structure

| Sheet | Purpose |
|---|---|
| Side by Side | Human-facing visual comparator: category rows with Hong Kong £/mo, UK £/mo, UK-minus-HK variance, higher-side flag, and validation notes. |
| Housing Mechanics | Splits DB flat and Cecil Road costs into common owner obligations, rent/tax flows, DB principal/equity, and the one-off DB letting agency fee. Feeds the housing row in Side by Side. |
| Inputs | Editable assumptions and source-derived constants. |
| Category Map | Canonical category alignment across HK budget, HK relocation categories, HK actual allocation, and UK forecast. |
| Scenario Summary | Income-floor scenarios, including HK$100k/month with and without Cecil Road rent offset. |
| Audit Flags | Items requiring review before the model should update the relocation verdict. |
| Source Notes | Source files used for workbook inputs. |

## Housing Mechanics Correction

The Side by Side sheet originally failed Julian's intended use case because the housing row was not like-for-like:

- HK housing used the raw DB live-in line (~HK$29k/mo, ~£2,900/mo).
- UK housing used Cecil Road live-in cost plus DB let-out shortfall.
- That mixed three different things: owner costs that exist in both scenarios, rent income that changes by location, and DB mortgage principal that is cash outflow but equity repayment.

The workbook now separates those layers.

| Housing view | HK-stay | London | London minus HK |
|---|---:|---:|---:|
| Pure rent/tax flows, common owner costs excluded | -£1,995 | -£1,936 | +£59 |
| Full monthly property cash cost, one-off agency fee excluded | £1,172 | £1,231 | +£59 |
| Net-worth basis, DB principal added back both sides | -£197 | -£138 | +£59 |
| First-year average if DB agency fee is spread over 12 months | £1,172 | £1,322 | +£151 |

Interpretation:

- The ongoing housing comparison is close to a wash, with London about £59/mo worse.
- The one-off DB letting agency fee is HK$11,000 (~£1,100). It is not a permanent monthly burn; if spread across year one only, it adds about £92/mo for that first year.
- The old visual comparison of HK £2,900 versus UK £1,289 should not be used for decision logic.

## Corrected Scenario Summary

Corrected as of the Claude hostile review (2026-07-09), then updated 2026-07-10 for the DB letting agency fee correction. "Trend" rows now use 83,940 (6-mo); "mean" rows use 92,196 (12-mo); net-worth rows add back the DB-flat principal (HKD 13,690/mo) on both sides. UK monthly burn now uses £4,550 ongoing, not £4,610, because the former £60/mo DB agent allowance has been replaced by a one-off HK$11,000 fee.

| Scenario | Surplus HKD/mo | ~£/mo |
|---|---:|---:|
| HK 100k, recent trend (83,940), **no** Cecil offset | +1,060 | +106 |
| HK 100k, recent trend, **with** Cecil offset | **+18,420** | **+1,842** |
| HK 100k, 12-mo mean (92,196), with Cecil offset | **+10,164** | **+1,016** |
| HK 100k, trend + Cecil + Clodagh half-fee | +21,470 | +2,147 |
| UK £77.5k floor, London cash burn | +757 | +76 |
| UK £120k, London cash burn | **+17,965** | **+1,797** |
| UK £120k, London **net-worth** burn | +31,655 | +3,166 |
| HK 100k, trend + Cecil, **net-worth** (symmetric) | **+32,110** | **+3,211** |
| HK 100k, mean + Cecil, **net-worth** (symmetric) | **+23,854** | **+2,385** |

**Reading:** at equal ~£120k gross, HK on recent trend still beats UK £120k on cash (+18,420 vs +17,965) and on net worth (+32,110 vs +31,655), but only narrowly. HK on the conservative 12-mo mean trails on cash (+10,164 vs +17,965) and on net worth (+23,854 vs +31,655). The workbook's pre-correction "UK is more surplus-rich" claim was an artifact of the two bugs, but the corrected result is denominator-sensitive rather than a clean UK or HK win.

## Bugs Corrected in Workbook

| Bug | Effect | Fix |
|---|---|---|
| Row 6 (`F6`) referenced `B12` (UK floor net salary, £55,508) as the HK cost basis | Inflated "mean actuals" surplus to +46,852; fed garbage to the summary block | Changed to `B13` (HK 12-mo mean, 92,196) |
| "Trend" rows 4/5/7/8 referenced `B13` (12-mo mean) not `B14` (6-mo trend, 83,940) | Under-stated HK by 8,256/mo; the doc's cited +18,420 was computed by no cell | Changed to `B14` |
| Net-worth view existed for UK only (R11); no symmetric HK row | Manufactured the UK surplus lead on net-worth | Added R12 (trend) and R13 (mean) HK net-worth rows |

## Remaining Open Questions (do not affect decision)

1. Split HK actuals into recurring, one-off, and provision categories (resolves the trend-vs-mean denominator).
2. Reconcile the HK$56k/month Travel budget provision against actual transaction data.
3. Remove or resize the historical HK tax provision for forward-looking income-floor scenarios.
4. Decide the UK cleaner assumption and the UK babysitting / childcare-cover assumption. The workbook now has separate rows for domestic help / cleaner and babysitting.
5. Split Sophia UK activities into categories comparable with HK tuition, health and fitness, leisure, transport, and babysitting.
6. Confirm London car assumption (biggest remaining UK-side swing, -£300-500/mo).
7. Confirm signed DB tenancy, actual HK agent fee, and whether HK property tax estimate is correct.

## Related

- [[uk-vs-hk-income-floor-reconciliation-2026-07-09.xlsx]]
- [[uk-vs-hk-income-floor-reconciliation-claude-review-2026-07-09]] - the hostile review that identified these corrections
- [[uk-vs-hk-income-floor-reconciliation-claude-review-prompt]]
- [[budget]]
- [[money-tracker]]
- [[uk-move-financial-model]]
- [[uk-vs-hk-cost-comparison]]
- [[london-monthly-budget]]
- [[uk-vs-hk-earning-comparison]]
- [[uk-relocation-decision]]
