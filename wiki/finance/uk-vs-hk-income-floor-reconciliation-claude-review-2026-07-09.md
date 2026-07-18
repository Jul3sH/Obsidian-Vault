---
type: review
authority: claude-reviewed
reviewer: Claude (Opus 4.8)
reviews: uk-vs-hk-income-floor-reconciliation-2026-07-09
created: 2026-07-09
currency: mixed (HKD + GBP, 10:1)
decision: UK Relocation Decision
tags: [finance, uk-relocation, cost-comparison, income-floor, review, adversarial]
---

# Income Floor Reconciliation - Claude Adversarial Review (2026-07-09)

> Hostile, independent review of [[uk-vs-hk-income-floor-reconciliation-2026-07-09]] and its workbook
> `uk-vs-hk-income-floor-reconciliation-2026-07-09.xlsx`, run against the [[uk-vs-hk-income-floor-reconciliation-claude-review-prompt|review prompt]].
> Numbers re-derived from source, not from Codex's summary. Findings flagged here only: the source
> workbook is not modified (see [[multi-agent-protocol|handoff discipline]]).

## Verdict

**The workbook is NOT over-corrected toward stay - the prompt's central worry is unfounded.** If anything, its *scenario rows* still under-credit Hong Kong. But its headline claim - that HK$100k/month is "survivable but less surplus-rich than UK £120k" - **does not survive**. It is an artifact of two spreadsheet errors plus one asymmetric treatment. Corrected, HK$100k/month gross produces a **similar-or-better** monthly surplus than the UK £120k role on cash, and **beats it** on net worth.

The single biggest thing the workbook obscures: **HK$100k/month gross = HK$1.2M/year = ~£120k/year gross = the exact same gross income as the "UK strong £120k role."** The workbook labels one a "weak floor" and the other "strong/comfortable" while they are the *same money*. That asymmetric framing is itself the confirmation-amplification the protocol warns about.

So: "HK has no cheap floor" is definitely too strong and must go. But "weak recovery floor" still undersells it. The honest, defensible UK advantage is **a lower break-even gross** (you can cover life in the UK on ~£77.5k; HK needs ~£90-95k-equivalent gross on recent actuals), **not** a bigger surplus at equal pay.

## Two hard spreadsheet bugs (both must be fixed before the workbook is cited)

### Bug 1 - Row 6 pulls a UK salary into an HK cost line (PRO-STAY error)
Scenario Summary `F6 = Inputs!$B$12`. But `B12` is **"UK floor role net annual GBP" = 55,508**, not an HK cost. The row is labelled "HK 100k role - mean actuals, with Cecil offset" and should reference `B13` (HK 12-mo mean, 92,196) or `B14` (HK trend, 83,940).

- As-built surplus: **+46,852 HKD/mo** (nonsense - it subtracts a UK annual net salary as if it were a monthly HK cost).
- Correct surplus (mean actuals): **+10,164 HKD/mo**.
- **This bug feeds summary cell `B18`**, so the workbook's own "mean actuals" headline reads +46,852 and makes HK look wildly comfortable. Overstatement: **+36,688 HKD/mo**.

### Bug 2 - "Trend" rows use the 12-month MEAN, not the trend (PRO-MOVE error)
Rows 4, 5, 7, 8 are all labelled "trend actuals" but reference `B13 = 92,196`, which the Inputs sheet itself labels **"HK actual 12-mo mean burn"**. The true recent-trend figure `B14 = 83,940` is **never referenced anywhere in the workbook**. So:

- The workbook's flagship "HK 100k, trend, Cecil offset" surplus is computed as **+10,164** (using the mean).
- The number the markdown companion *cites* - "roughly HK$18k/mo surplus against recent actuals" (+18,420 using 83,940) - **is not produced by any cell.** The doc quotes a figure the workbook does not compute.
- Also internally inconsistent: the Category Map sheet's `col D` sums to exactly **83,940** (trend), so the two sheets disagree on which actuals denominator is "the" number.

## One structural bias: asymmetric net-worth treatment (PRO-MOVE)

The workbook gives the UK £120k role **both** a cash-burn row (R10) and a net-worth row (R11, which strips the £1,369/mo DB-flat principal as equity, not consumption). It gives Hong Kong **only** a cash-burn view.

But in the HK-stay scenario Julian **lives in the DB flat and pays its full mortgage** - the ~29,000 HKD/mo housing line inside the 83,940 burn includes **~13,689 HKD/mo (£1,369) of principal**, the same equity accrual the UK row is allowed to add back. Denying HK the symmetric net-worth view understates HK's position by 13,689 HKD/mo and **manufactures the UK's surplus lead**. On a symmetric net-worth basis the ranking flips to HK-favoured (table below).

## Corrected monthly surplus table

All HK rows: net salary 85,000 (HK$100k gross @ 15%) + Cecil offset where shown − cost basis. Net-worth rows add back the 13,689 DB-flat principal on the HK side to match the UK row's treatment.

| Scenario | Basis | Cost basis HKD | Surplus HKD/mo | ≈ £/mo |
|---|---|---:|---:|---:|
| HK 100k, recent actuals (83,940), **no** Cecil offset | cash | 83,940 | **+1,060** | +106 |
| HK 100k, recent actuals, **with** Cecil offset | cash | 83,940 | **+18,420** | +1,842 |
| HK 100k, 12-mo mean (92,196), with Cecil offset | cash | 92,196 | **+10,164** | +1,016 |
| HK 100k, recent actuals, with Cecil offset + Clodagh half-fee | cash | 80,890 | **+21,470** | +2,147 |
| UK £77.5k floor, London cash burn | cash | 46,100 | **+157** | +16 |
| UK £120k, London cash burn | cash | 46,100 | **+17,365** | +1,737 |
| UK £120k, London **net-worth** burn | net-worth | 32,410 | **+31,055** | +3,106 |
| HK 100k, recent actuals, Cecil offset, **net-worth** (symmetric) | net-worth | 70,251 | **+32,109** | +3,211 |
| HK 100k, 12-mo mean, Cecil offset, **net-worth** (symmetric) | net-worth | 78,507 | **+23,853** | +2,385 |

**Reading:**
- On **cash**, at equal ~£120k gross, HK on recent actuals (+18,420) slightly **beats** UK £120k (+17,365); HK on the conservative 12-mo mean (+10,164) trails it. So the honest cash answer is "roughly equal, denominator-dependent," not "UK clearly ahead."
- On a **symmetric net-worth** basis, HK (+32,109 recent / +23,853 mean) is level-to-ahead of UK (+31,055). The workbook's asymmetry is the only thing that made UK look richer.
- The UK's **real** floor advantage shows in the £77.5k row: the UK breaks even on cash at **£77.5k gross**, whereas HK needs net ≈ 66,580 HKD/mo (burn 83,940 − Cecil 17,360), i.e. **~£90-95k-equivalent gross** on recent actuals (more on the 12-mo mean). The UK lets you survive on a **lower** gross - that is the genuine, narrower edge.

## Corrections table

| # | Error | Direction | Monthly magnitude |
|---|---|---|---:|
| 1 | Row 6 references `B12` (UK net salary) as HK cost basis | **Pro-stay** | +36,688 HKD overstated (feeds summary B18) |
| 2 | "Trend" rows use 12-mo mean (92,196), not trend (83,940); trend never computed | **Pro-move** | HK understated ~8,256 HKD vs its own trend |
| 3 | Net-worth view given to UK only, not HK, despite HK paying DB principal | **Pro-move** | HK understated 13,689 HKD; flips net-worth ranking |
| 4 | Category Map (83,940) vs Scenario Summary (92,196) disagree on actuals | Mixed | ~8,256 HKD denominator swing |
| 5 | Scenario UK burn £4,610 excludes cleaner (£300) + car; Category Map UK total ~£6,290 | **Pro-move** | UK surplus overstated up to ~3,000-8,000 HKD if car/cleaner apply |
| 6 | HK effective tax 15% vs computed ~13.6% on HK$1.2M (before MPF) | Pro-move | HK net understated ~1,370 HKD; ~offset by MPF 1,500 forced-saving |
| 7 | Cecil offset 1,736 vs the §9 more-careful 1,725 | Pro-stay | ~110 HKD - immaterial |

**What is sound (credit where due):**
- **No double-count** between the Cecil offset and the HK burn. The 83,940 burn's housing line is the **DB flat** mortgage; the Cecil Road costs (£213 interest, £46 insurance, £199 UK tax) are netted *inside* the £1,736 offset. The two do not overlap. This was the biggest risk and it is handled correctly.
- **Cecil offset choice (1,736)** is the right one for an HK-stay case - it is the non-resident-landlord figure with UK tax applied, not the pre-mortgage £2,194 or the FIG-exempt UK-resident figure. Consistent.
- Tax treatment is coherent: FIG (4-year UK exemption) correctly does **not** apply to the HK-stay case (Julian is HK-resident; UK taxes the UK-source rent via NRL with personal allowance).

## Direction of remaining uncertainty

The prompt asks which way the residual lean goes. **The scenario rows lean pro-move** (mean-not-trend, no HK net-worth view, possibly-light UK burn). **The summary block leans pro-stay** solely because of the Bug-1 garbage number. Net across the workbook: the "UK is more surplus-rich" conclusion is unsupported and reverses under correct, symmetric treatment. The largest single real-world swing that is *not* a bug is **which HK actuals denominator you trust** (trend 83,940 vs mean 92,196 = 8,256 HKD/mo), followed by **whether London runs a car** (−£300-500/mo, a UK-side swing already flagged in Test A).

## Answers to the prompt's required outputs

1. **Verdict:** Defensible in *direction* (HK$100k survivable), but its supporting numbers are wrong and its "UK is more surplus-rich" headline does not hold. Not over-corrected toward stay; still under-credits HK on the scenario rows.
2. **Corrected surplus table:** above.
3. **Corrections table:** above.
4. **Replace "HK has no cheap floor"?** Yes - delete it. But **do not** replace it with "weak recovery floor" unqualified. Accurate replacement: *"HK$100k/month gross (= £120k/year, the same gross as the UK 'strong' role) covers life with a similar-or-better cash surplus than that UK role once Cecil Road rent is offset, and builds more net worth via lower tax plus DB-flat equity. It is 'weak' only relative to a senior HK role, not relative to the UK £120k role."*
5. **Does UK still win the cost-covering floor?** Yes, but for a different reason and narrower than stated: the UK **break-even gross is lower** (~£77.5k vs ~£90-95k-equivalent in HK on recent actuals), not that the UK yields more surplus at equal pay. **Confidence: medium** - it hinges on the actuals denominator, on the £4,610 London burn holding (excludes car and cleaner), and on the 15% HK tax / £1,736 offset assumptions.
6. **Should the decision or reopen-condition change now?** **No.** The corrected numbers *reinforce* the already-published [[uk-vs-hk-earning-comparison|earning comparison]] conclusion ("income is not a decisive reason to move; the floor edge is real but narrow"). The reconciliation just narrows the floor gap further on cash and reverses it on net worth - which only strengthens the existing position that the decision rests on **P(landing a role) + the non-income pillars**, never on the cost floor. No new data is required to hold the MOVE direction. The highest-value data to *sharpen* the floor question (not to change the decision) is: split the HK travel provision to fix the denominator, and settle the London car assumption.

## Key Takeaways

- **Two hard bugs:** Row 6 subtracts a UK salary as an HK cost (pro-stay, +36,688 HKD overstatement, feeds the summary); the "trend" rows silently use the 12-month mean, so the +18,420 figure the doc quotes is computed nowhere.
- **One structural bias:** the net-worth view is granted to the UK only; giving HK the same symmetric treatment (add back the DB-flat principal it also pays) flips the net-worth ranking to HK-favoured.
- **The framing tell:** HK$100k/month gross and the "UK strong £120k role" are the **same £120k gross**. Calling one a weak floor and the other comfortable is confirmation-amplification.
- **Corrected answer:** at equal gross, HK ≈ UK on cash and beats it on net worth. The UK's genuine edge is a **lower break-even gross**, medium confidence.
- **Decision impact: none.** The correction reinforces the standing "income is not the reason to move" conclusion. Fix the two bugs and the asymmetry before the workbook is cited anywhere.

## Related

- [[uk-vs-hk-income-floor-reconciliation-2026-07-09]] - the reviewed source
- [[uk-vs-hk-income-floor-reconciliation-claude-review-prompt]] - the prompt run
- [[uk-move-financial-model]] · [[uk-vs-hk-cost-comparison]] · [[london-monthly-budget]]
- [[uk-vs-hk-earning-comparison]] - the published head-to-head this reconciliation feeds
- [[uk-relocation-decision]] · [[multi-agent-protocol]]
