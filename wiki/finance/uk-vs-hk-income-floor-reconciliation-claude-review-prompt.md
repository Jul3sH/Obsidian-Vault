---
type: prompt
status: ready
created: 2026-07-09
tags: [finance, uk-relocation, adversarial-review, prompt]
---

# UK vs HK Income Floor Reconciliation - Claude Review Prompt

## Key Takeaways

- Use this prompt to ask Claude for a hostile review of the new income-floor reconciliation workbook.
- The central question is whether HK$100k/month gross is genuinely a weak recovery floor, or whether Codex has now over-corrected away from the move case.
- Claude should review the spreadsheet formulas, category mapping, and source documents, then say whether the UK floor advantage survives.

## Copy-Paste Prompt

```text
ROLE
You are a hostile, independent financial reviewer. Your job is to break a relocation income-floor model, not to agree with it.

CONTEXT
This review feeds a real Hong Kong to London relocation decision. A previous narrative model said Hong Kong had "no cheap floor" and that a lower-paid HK role around HK$100k/month gross did not really cover life. Julian challenged this because Hong Kong and London costs now appear roughly similar, and HK taxes are lower.

Codex has created a spreadsheet-backed reconciliation and found that the old wording was too strong: HK$100k/month gross looks survivable once Cecil Road rent is offset, but it may still be only a weak recovery floor.

Your job is to verify or break that correction.

PRIMARY FILE TO REVIEW
- wiki/finance/uk-vs-hk-income-floor-reconciliation-2026-07-09.xlsx
- wiki/finance/uk-vs-hk-income-floor-reconciliation-2026-07-09.md

SOURCE FILES TO CHECK
- wiki/finance/budget.md
- wiki/finance/money-tracker.md
- wiki/finance/uk-move-financial-model.md
- wiki/finance/uk-vs-hk-cost-comparison.md
- wiki/finance/london-monthly-budget.md
- wiki/finance/financial-status-2026-07-07.md
- wiki/career/uk-vs-hk-earning-comparison.md
- wiki/career/uk-vs-hk-earning-comparison-jh-clarifications-2026-07-09.md
- wiki/projects/uk-relocation-decision.md

KNOWN ISSUE TO TEST
The first-pass workbook says:
- HK$100k/month gross at ~15 percent tax gives ~HK$85k/month net.
- If Julian stays in HK, Cecil Road net rent should be offset at about £1,736/month, or about HK$17,360/month.
- Against recent HK actuals of HK$83,940/month, that gives about HK$18,420/month surplus.
- Against 12-month mean actuals of HK$92,196/month, that gives about HK$10,164/month surplus.
- UK £120k gross gives about £76,158/year net, or about HK$63,465/month, and London cash burn is about HK$46,100/month, giving about HK$17,365/month surplus.

CHECK THESE NUMBERS FROM SCRATCH.

ATTACK CHECKLIST
1. Category alignment
   - Does the workbook correctly use money-tracker.md and budget.md as the category spine?
   - Are any HK costs double-counted or dropped when moving from budget.md to the relocation model?
   - Are UK forecast categories mapped to comparable HK categories, or are some UK costs hidden in broad placeholders?

2. HK actuals versus HK budget
   - The HK canonical budget shows HK$146,674/month total and HK$61,738/month HSBC-account lens.
   - The financial model uses actual mean HK$92,196/month and recent trend HK$83,940/month.
   - Explain which number is the right denominator for testing HK$100k/month viability.
   - Identify whether the HK$56k/month Travel provision and HK$24.5k/month Tax provision should be excluded, resized, or retained for forward-looking income-floor tests.

3. Cecil Road rent offset
   - Verify that HK-stay scenarios should include Cecil Road net rental income.
   - Verify whether £1,736/month is the correct net offset, or whether it should be £1,725, £1,814, £2,194, or another figure.
   - Check whether the tax treatment of Cecil Road rent is consistent with the source files.

4. HK$100k/month role
   - Recompute net salary after HK salaries tax for HK$1.2M/year.
   - Is 15 percent effective tax too high, too low, or acceptable?
   - Does HK$100k/month gross become survivable, cash-flow neutral, or genuinely wealth-rebuilding after rent offset?

5. UK £120k comparison
   - Recompute UK net salary on £120k gross.
   - Check whether the UK comparison should use cash burn (£4,610/month) or net-worth burn (~£3,241/month).
   - Check whether the UK forecast omits cleaner, car, Sophia activities, dental, prescriptions, school extras, or one-off moving costs.

6. Helper, cleaner, and Sophia costs
   - HK has helper HK$3,000/month and school fee around HK$6,100-6,900/month.
   - UK has no school fees, but may need a part-time cleaner and extra-curricular activities.
   - Check whether the workbook handles these on a fair like-for-like basis.

7. Cash flow versus net worth
   - DB flat principal is a cash outflow but equity accumulation.
   - Decide whether the income-floor question should use cash-flow burn, net-worth burn, or both.
   - State which is relevant for "can I live on this income?" versus "am I rebuilding safety?"

8. Bias direction
   - Hunt both directions.
   - Did the original model over-favour moving by forgetting the Cecil Road rent offset?
   - Did Codex now over-correct toward staying by treating HK$100k/month as too comfortable?
   - Which way does the remaining uncertainty lean?

OUTPUT REQUIRED
1. Verdict: Is the new workbook defensible, still pro-move biased, or now over-corrected toward stay?
2. Corrected monthly surplus table for:
   - HK$100k gross, recent actuals, no Cecil offset
   - HK$100k gross, recent actuals, with Cecil offset
   - HK$100k gross, 12-month actuals, with Cecil offset
   - HK$100k gross, with Clodagh contribution
   - UK £77.5k gross, London cash burn
   - UK £120k gross, London cash burn
   - UK £120k gross, London net-worth burn
3. Corrections table: error, direction, monthly magnitude.
4. State whether "HK has no cheap floor" should be replaced by "HK$100k/month is a weak recovery floor."
5. State whether the UK still wins the cost-covering floor, and with what confidence.
6. State whether the relocation decision or reopen-condition conclusion should change now, or whether more data is needed first.

Be hostile. Do not validate Codex unless the numbers survive.
```

## Related

- [[uk-vs-hk-income-floor-reconciliation-2026-07-09]]
- [[uk-vs-hk-income-floor-reconciliation-2026-07-09.xlsx]]
- [[uk-vs-hk-cost-comparison]]
- [[uk-move-financial-model]]
- [[budget]]
- [[money-tracker]]
- [[uk-relocation-decision]]
