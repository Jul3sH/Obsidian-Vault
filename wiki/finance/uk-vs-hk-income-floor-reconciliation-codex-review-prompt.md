---
type: review-prompt
created: 2026-07-10
tags: [finance, uk-relocation, income-floor, review-prompt]
---

# Codex Review Prompt - Income Floor Reconciliation (Claude Corrections)

## What this is

Claude (Opus 4.8) ran a hostile adversarial review of the income-floor reconciliation workbook
that Codex built on 2026-07-09. Claude found two hard spreadsheet bugs and one structural bias,
then fixed them. Your job is to independently verify that the fixes are correct and the resulting
numbers are defensible.

Read from the source files. Do not simply agree with Claude.

## What Claude found and fixed

### Bug 1 - Row 6 wrong cost-basis reference (was pro-stay)

`Scenario Summary!F6` was `=Inputs!$B$12`. But `B12` is "UK floor role net annual GBP" (55,508),
not an HK cost. The row is labelled "HK 100k role - mean actuals, with Cecil offset" and must
reference the HK 12-month mean burn.

Fix applied: `F6` changed to `=Inputs!$B$13` (HK 12-mo mean, 92,196).

Effect: the row surplus corrected from a nonsense +46,852 to the correct +10,164. This cell also
fed the summary block at B18, so the summary was showing garbage.

### Bug 2 - "Trend" rows used the 12-month mean, not the trend (was pro-move)

Rows 4, 5, 7, and 8 are all labelled "trend actuals" but referenced `B13` (12-mo mean, 92,196).
The true recent-trend figure is `B14` (6-mo trend, 83,940). `B14` was never referenced anywhere
in the workbook. The companion doc cited a +18,420 surplus for the "trend actuals with Cecil
offset" scenario, but no cell computed that number.

Fix applied: `F4`, `F5`, `F8` changed to `=Inputs!$B$14`; `F7` changed to
`=Inputs!$B$14-Inputs!$B$25`.

Effect: the flagship "HK 100k, trend, Cecil offset" scenario now produces +18,420 (matching the
doc's cited figure) rather than +10,164.

### Structural bias - net-worth view given to UK only (was pro-move)

The UK £120k role had both a cash-burn row (R10) and a net-worth row (R11, which strips the
£1,369/mo DB-flat principal as equity). HK had only cash rows, even though in the HK-stay
scenario Julian lives in the DB flat and pays that same ~HK$13,690/mo of principal.

Fix applied: two new rows added to Scenario Summary:
- R12: "HK 100k role - trend actuals, Cecil offset, net-worth basis" - cost basis uses
  `Inputs!$B$14 - Inputs!$B$21*Inputs!$B$4` (trend burn minus DB principal in HKD).
- R13: "HK 100k role - mean actuals, Cecil offset, net-worth basis" - same but with `B13`.

Effect: on a symmetric net-worth basis HK is ahead of the UK £120k role (HK trend +32,110 vs
UK +31,055; HK mean +23,854 vs UK +31,055).

## The headline conclusion that follows

HK$100k/month gross is ~£120k/year gross - the same as the "UK strong £120k role." At equal
gross, HK on recent trend produces a similar-or-better cash surplus to the UK role once Cecil
Road rent is offset, and beats it on a symmetric net-worth basis.

The UK's genuine floor advantage is a lower break-even gross (~£77.5k in the UK vs ~£90-95k
gross-equivalent in HK on recent actuals), not more surplus at equal pay.

"HK has no cheap floor" is wrong and should be deleted from all reports. "Weak recovery floor"
is accurate only relative to a senior HK role (HK$125-150k), not relative to the UK £120k role.

## Files changed

| File | Change |
|---|---|
| `wiki/finance/uk-vs-hk-income-floor-reconciliation-2026-07-09.xlsx` | Formulas fixed (R6, R4/5/7/8 trend refs); R12/R13 net-worth rows added; summary text corrected |
| `wiki/finance/uk-vs-hk-income-floor-reconciliation-2026-07-09.md` | Frontmatter updated; review callout added; Key Takeaways rewritten; corrected scenario table + bugs table replacing the old first-pass interpretation |
| `wiki/finance/_index.md` | One new index entry for the review file |
| `wiki/ai-os/logs/log-2026-Q3.md` | Two new log rows |
| `wiki/finance/uk-vs-hk-income-floor-reconciliation-claude-review-2026-07-09.md` | New file: the full hostile review document with all findings, corrections table, and answers to the original review prompt |

## Source files to cross-check against

- `wiki/finance/uk-move-financial-model.md` - HK actuals (§1: mean 92,196, trend 83,940), DB flat
  mortgage breakdown (§11: HK$13,689/mo principal), Cecil Road P&L (§9: net £1,736 in HK-stay case)
- `wiki/finance/uk-vs-hk-cost-comparison.md` - Cecil Road net rent calculation (§1: £1,736)
- `wiki/finance/london-monthly-budget.md` - London cash burn (£4,610/mo) and net-worth burn
  (£3,241/mo after DB principal)
- `wiki/career/uk-150k-feasibility-jh-clarifications-2026-07-09.md` - UK PAYE net estimates
  (£120k gross = £76,158 net; £77.5k gross = £55,508 net)

## What Codex should verify

1. Are the three formula fixes correct? Re-derive the intended cell values from the source files
   and confirm the new references produce the right numbers.
2. Is the DB-flat principal figure (HK$13,689/mo = ~£1,369) the right number to add back for
   a symmetric net-worth comparison? Check against uk-move-financial-model.md §11.
3. Is the Cecil Road net rent offset (£1,736/mo HK-stay case) the right figure? Check against
   uk-vs-hk-cost-comparison.md §1 and uk-move-financial-model.md §9.
4. Does the resulting corrected scenario table in the companion doc match what the fixed workbook
   would compute?
5. Is the revised headline conclusion ("UK's real edge is a lower break-even gross, not more
   surplus at equal pay") supported by the corrected numbers?
6. Are there any further errors Claude missed?

State whether you agree, disagree, or partially agree with each fix, and why. Do not validate
Claude unless the numbers survive re-derivation from source.

## Related

- [[uk-vs-hk-income-floor-reconciliation-2026-07-09]] - the corrected companion doc
- [[uk-vs-hk-income-floor-reconciliation-claude-review-2026-07-09]] - Claude's full review
- [[uk-vs-hk-income-floor-reconciliation-claude-review-prompt]] - the original hostile-review prompt
- [[uk-move-financial-model]] - primary source for HK actuals and property mechanics
- [[uk-vs-hk-cost-comparison]] - Test A; source for the Cecil Road offset
- [[multi-agent-protocol]] - protocol governing how review files relate to source files
