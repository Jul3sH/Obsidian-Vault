---
type: review
status: complete
created: 2026-07-10
authority: codex-reviewed
currency: mixed (HKD + GBP, 10:1)
decision: UK Relocation Decision
tags: [finance, uk-relocation, cost-comparison, income-floor, adversarial-review]
---

# UK vs HK Income Floor Reconciliation - Codex Review 2026-07-10

> **Post-review update, later 2026-07-10:** Julian corrected the DB letting agency fee: HK$11,000 one-off, not a recurring ~£60/mo allowance. The workbook now has a Housing Mechanics sheet and uses £4,550 ongoing London burn rather than £4,610. This review remains valid for the Claude formula fixes it checked, but its London-burn input table is superseded by [[uk-vs-hk-income-floor-reconciliation-2026-07-09]].

## Key Takeaways

- I agree with Claude on the three spreadsheet fixes: Row 6 was referencing the wrong input, the "trend" rows were using the mean, and HK needed symmetric net-worth rows.
- The corrected workbook formulas now match the intended mechanics, subject to one immaterial rounding difference: using £1,369 as the DB principal add-back gives HK$13,690, while the source mortgage split says HK$13,689.
- I do **not** fully agree with Claude's headline wording. HK is ahead of the UK £120k role only on the recent-trend denominator. On the 12-month mean denominator, HK trails the UK £120k role by about HK$7,201/month on both cash and net-worth basis.
- The defensible conclusion is: **at equal ~£120k gross, HK and UK are close, and the result depends on which HK actuals denominator is trusted. The UK's clearer edge is the lower break-even gross, not superior surplus at equal pay.**
- The companion document should be tightened before being treated as settled evidence: replace "HK beats UK on symmetric net-worth basis" with "HK beats UK on recent-trend net-worth basis, but trails on the 12-month mean."

## Verdict

Claude's spreadsheet corrections are **substantively correct**. Claude's revised interpretation is **partly overstated in HK's favour**.

This is not a return to the old "HK has no cheap floor" claim. That claim remains wrong. But the corrected numbers do not justify the broader claim that HK is simply ahead at equal gross. They justify a narrower claim:

> HK$100k/month with Cecil Road rent offset is viable and broadly comparable to a UK £120k role. It is marginally better than the UK role on recent trend actuals, and materially worse on the 12-month mean. The remaining fight is over the actuals denominator, not over a spreadsheet bug.

## Source Inputs Re-Derived

| Input | Source value | Used value | Verdict |
|---|---:|---:|---|
| HK 12-month mean burn | HK$92,196/mo | `Inputs!B13 = 92196` | Correct |
| HK 6-month trend burn | HK$83,940/mo | `Inputs!B14 = 83940` | Correct |
| Cecil Road net offset in HK-stay case | £1,736/mo in Test A; ~£1,725/mo in source model | `Inputs!B18 = 1736` | Defensible; Test A value is the current model value |
| DB flat principal | HK$13,689/mo | `Inputs!B21 * B4 = 1369 * 10 = HK$13,690` | Correct within HK$1 rounding |
| London cash burn | £4,610/mo | `Inputs!B19 = 4610` | Correct |
| London net-worth burn | £4,610 less £1,369 = £3,241/mo | `Inputs!B20 = 3241` | Correct |
| UK £120k net annual | ~£76.2k | `Inputs!B10 = 76158` | Correct |
| UK £77.5k floor net annual | £55,508 | `Inputs!B12 = 55508` | Correct |

Sources checked: [[uk-move-financial-model]], [[uk-vs-hk-cost-comparison]], [[london-monthly-budget]], [[uk-150k-feasibility-jh-clarifications-2026-07-09]], [[uk-150k-feasibility-report]].

## Formula Fix Verdicts

| Claude fix | Codex verdict | Reason |
|---|---|---|
| `Scenario Summary!F6` changed from `Inputs!B12` to `Inputs!B13` | Agree | Row 6 is labelled HK 100k mean actuals. `B12` is UK floor-role net annual salary, not an HK cost basis. `B13` is the HK 12-month mean burn, HK$92,196/mo. |
| Trend rows 4, 5, 7, and 8 changed from `Inputs!B13` to `Inputs!B14` | Agree | The rows are explicitly labelled trend actuals. The source model defines the recent trend as HK$83,940/mo in `B14`, while `B13` is the 12-month mean. |
| Row 7 changed to `Inputs!B14 - Inputs!B25` | Agree | This row tests the same trend case but assumes Clodagh pays HK$3,050/mo. Subtracting the contribution from cost basis is mechanically correct. |
| HK net-worth rows added for trend and mean | Agree | UK already had a net-worth row stripping out DB principal. HK actuals include the DB mortgage principal outflow, so a symmetric net-worth comparison needs the same add-back. |

## Corrected Scenario Table

| Scenario | Re-derived surplus HKD/mo | Re-derived surplus GBP/mo | Workbook / companion doc match? |
|---|---:|---:|---|
| HK 100k, recent trend, no Cecil offset | +1,060 | +106 | Yes |
| HK 100k, recent trend, with Cecil offset | +18,420 | +1,842 | Yes |
| HK 100k, 12-month mean, with Cecil offset | +10,164 | +1,016 | Yes |
| HK 100k, trend + Cecil + Clodagh half-fee | +21,470 | +2,147 | Yes |
| HK 125k senior, trend + Cecil | +39,670 | +3,967 | Workbook yes; omitted from companion table |
| UK £77.5k floor, London cash burn | +157 | +16 | Yes |
| UK £120k, London cash burn | +17,365 | +1,737 | Yes |
| UK £120k, London net-worth burn | +31,055 | +3,106 | Yes |
| HK 100k, trend + Cecil, net-worth basis | +32,110 | +3,211 | Yes, using rounded DB principal |
| HK 100k, mean + Cecil, net-worth basis | +23,854 | +2,385 | Yes, using rounded DB principal |

## The Missed Error

Claude's corrected companion doc says:

> HK on the conservative 12-mo mean trails on cash (+10,164) but is ahead on net worth (+23,854).

That is arithmetically wrong if the comparator is the UK £120k net-worth row:

| Basis | HK 100k trend | HK 100k mean | UK £120k | Result |
|---|---:|---:|---:|---|
| Cash | +18,420 | +10,164 | +17,365 | HK trend ahead by +1,055; HK mean behind by -7,201 |
| Net worth | +32,110 | +23,854 | +31,055 | HK trend ahead by +1,055; HK mean behind by -7,201 |

The HK mean net-worth row beats the UK **cash** row, but it does not beat the UK **net-worth** row. That distinction should be corrected anywhere the conclusion is summarised.

## Cecil Road Offset

The workbook's £1,736/mo Cecil Road offset is defensible because it matches the current Test A value:

`£2,194 take-home rent - £213 mortgage - £46 insurance - £199 UK tax = £1,736`

The source model also contains a rounded version using ~£210 tax, giving ~£1,725. The difference is only £11/mo, or HK$110/mo at the workbook's FX rate. It is not load-bearing.

What would be wrong is using £2,194 as the offset, because that is before mortgage, insurance, and tax.

## DB Principal Add-Back

The DB-flat principal add-back is valid for a net-worth basis.

The source model gives:

| DB mortgage component | HKD/mo |
|---|---:|
| Total mortgage payment | 25,827 |
| Interest | 12,138 |
| Principal | 13,689 |

The workbook adds back `£1,369 * 10 = HK$13,690`. That is a HK$1/mo rounding difference from the source mortgage split, not a modelling issue.

The conceptual point is correct: if UK gets a net-worth row that treats DB principal as equity rather than consumption, HK must get the same treatment because HK-stay actuals include the DB mortgage outflow.

## Headline Conclusion

I partially agree with the revised headline.

Supported:

- "HK has no cheap floor" should stay deleted.
- HK$100k/month with Cecil Road rent offset is a viable income floor, not a cliff.
- The UK's real advantage is a lower break-even gross.
- At equal ~£120k gross, the UK is not obviously more surplus-rich once Cecil Road rent and DB principal are treated symmetrically.

Overstated:

- "HK beats UK on symmetric net-worth basis" is only true on recent trend actuals.
- On the 12-month mean, HK trails UK £120k by about HK$7,201/mo, or £720/mo.
- Therefore the conclusion should not be "HK is ahead"; it should be "HK is close, and the answer depends on whether the 6-month trend or 12-month mean is the better forward-looking denominator."

## Further Errors Or Risks Claude Missed

| Issue | Direction | Magnitude | Comment |
|---|---|---:|---|
| Companion doc says HK mean net-worth is ahead of UK net-worth | Pro-HK / pro-stay | HK$7,201/mo misstatement | This is the main correction. The number is in the table, but the prose reads it incorrectly. |
| DB principal rounding uses HK$13,690 instead of HK$13,689 | Trivial pro-HK | HK$1/mo | Not worth changing unless the workbook is being made exact. |
| Cecil offset could be £1,725 rather than £1,736 depending on tax rounding | Trivial pro-HK | £11/mo | Not material. Use Test A's £1,736 unless Test A changes. |
| HK effective tax rate fixed at 15% | Likely conservative against HK | Unknown, probably modest | HK salaries tax may be below 15% at HK$100k/mo depending deductions and allowances. Keep as conservative unless recalculated from actual tax rules. |
| UK £120k scenario does not yet test cleaner, car, or lumpy UK costs | Potentially pro-UK | £300-800/mo if car/cleaner included | This belongs in scenario sensitivity, not in the formula fix verdict. |
| HK actuals denominator remains unresolved | Ambiguous | HK$8,256/mo swing | This is now the central uncertainty. The model needs recurring vs one-off classification before the equal-gross surplus comparison is "settled." |

## Recommended Correction To Source Wording

Replace the companion document's strongest claims with:

> At equal ~£120k gross, HK$100k/month with Cecil Road rent offset is broadly comparable to the UK £120k role. On recent trend actuals, HK is slightly ahead on both cash and net-worth basis. On the 12-month mean, HK trails the UK by about HK$7.2k/month. The UK's clearer advantage is a lower break-even gross, not greater surplus at equal pay.

Do not restore "HK has no cheap floor." That statement remains unsupported by the corrected model.

## Related

- [[uk-vs-hk-income-floor-reconciliation-2026-07-09]]
- [[uk-vs-hk-income-floor-reconciliation-codex-review-prompt]]
- [[uk-vs-hk-income-floor-reconciliation-claude-review-2026-07-09]]
- [[uk-vs-hk-income-floor-reconciliation-claude-review-prompt]]
- [[uk-move-financial-model]]
- [[uk-vs-hk-cost-comparison]]
- [[london-monthly-budget]]
- [[uk-150k-feasibility-jh-clarifications-2026-07-09]]
- [[uk-relocation-decision]]
