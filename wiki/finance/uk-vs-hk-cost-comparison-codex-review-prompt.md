---
type: prompt
status: living
created: 2026-07-09
decision: UK Relocation Decision
tags: [finance, uk-relocation, adversarial-review, codex]
---

# Codex Adversarial-Review Prompt - Test A (UK vs HK Cost Comparison)

> The prompt handed to **Codex** for an independent adversarial review of
> [[uk-vs-hk-cost-comparison|Test A]]. A [[uk-vs-hk-cost-comparison#8. Adversarial review (Fable, 2026-07-08) - the current answer|Fable review]]
> already ran; this is a second, independent attacker instructed to re-derive from source, check
> BOTH bias directions (residual pro-move tilt AND recent over-correction into pessimism), and rule
> on the reopen condition. Paste Codex's verdict into the "Codex verdict" section below when it returns.

## The prompt

```
ROLE
You are a hostile, independent adversarial financial reviewer. Your job is to break a
cost-comparison model that feeds a high-stakes, emotionally-charged relocation decision
(Hong Kong -> London). Be sceptical, quantitative, and specific. Do not be agreeable.
"Looks reasonable" is a failure; find what is wrong or unproven.

WORKING DIRECTORY
/Users/julianhart/Obsidian Vault/   (read the files directly)

TWO BIAS DIRECTIONS TO HUNT (this is critical)
1. The original model exhibited CONFIRMATION-AMPLIFICATION: every soft input leaned toward
   the owner's preferred answer (moving). A prior Fable review already caught this and cut a
   "~£1,000/mo cheaper" figure to "~£380/mo".
2. Since that review, the owner has fed in corrections (honest DB-flat cost, Clodagh school-fee
   split, repairs) that push the number the OTHER way - toward "the move is not worth it".
   So you must check BOTH directions: is the doc now OVER-corrected into pessimism, or is it
   still hiding a pro-move tilt? Call whichever way the evidence actually lands. Do NOT assume
   the pessimistic number is the honest one just because it is newer.
Do not simply repeat Fable's findings - re-derive the numbers independently from source and
reach your own verdict.

PRIMARY DOCUMENT UNDER REVIEW
wiki/finance/uk-vs-hk-cost-comparison.md   (the model, "Test A" - read every section incl. §8
   adversarial review and the Confirmed-inputs log)

SUPPORTING DOCUMENTS (read all - they hold the source numbers and context)
- wiki/finance/uk-move-financial-model.md          Source model; esp. §1 (HK burn actuals),
                                                   §9-10 (property P&L, runway, MPF), §11 (DB flat
                                                   hold-and-let), §12 (UK FIG tax on HK rent)
- wiki/finance/london-monthly-budget.md            The earlier, flawed budget Test A supersedes
- wiki/finance/financial-status-2026-07-07.md      Balance sheet: assets, liabilities, Cecil Road
                                                   income/costs, HK expense actuals, ISAs, MPF
- wiki/career/uk-150k-feasibility-report.md        "Test B": UK income feasibility (needed to judge
                                                   the reopen condition, see FINAL TASK)
- wiki/performance/decisions/decision-journal.md   The committed decision + the pre-set reopen
                                                   condition + the wobble log
- wiki/performance/decisions/commitment-lock-protocol.md   The F-N-M-T reopen test
- wiki/projects/uk-relocation-decision.md          Project status / current position
- wiki/relationships/clodagh.md                    Context for the school-fee-split contingency

KNOWN FACTS TO ANCHOR AGAINST (verify, do not just accept)
- Council tax: the earlier Band C / Montague Road bill was wrong. Correct bill supplied 2026-07-09:
  **48 Cecil Road, SW19 1JP, Band E**. Merton 2026/27 Band E = £2,616.19/yr = ~£218/mo
  (or £2,666.77/yr = ~£222/mo if the Wimbledon Common levy applies).
- ADDRESS DISCREPANCY: resolved. Remaining property-cost issue is house running cost: energy,
  maintenance / repairs, and possible Wimbledon Common levy.
- DB flat (HK) let-out net cost now booked at ~£1,030/mo (£970 computed shortfall + ~£60 agent fee).
- FX held at 10:1 HKD:GBP (real ~10.2-10.5).
- Clodagh (ex-wife) legally owes ~half of Sophia's HK school fee (~£305/mo) but is defaulting;
  an appeal is planned but not made.

THE MODEL'S CURRENT CLAIMS TO ATTACK
1. Bottom-line: London ~£325/mo cheaper (base case), flipping to roughly ~£15/mo more expensive if Clodagh pays her
   half, and NEGATIVE (London more expensive) if a car is run.
2. Property section: London is now ~£117/mo MORE expensive than staying, once the DB flat cost is
   honest. "Housing is a wash then tips against London."
3. The entire residual saving is Sophia's school fee (~£650/mo), which is itself contingent.
4. Ex-school-fee, London is ~£200-400/mo MORE expensive than HK.
5. ~£10-25k of one-off moving costs = 3-6 years payback.
6. Conclusion: cost is neutral-to-negative for the move; the decision rests entirely on income
   (Test B) + tax, NOT on cost.

ATTACK CHECKLIST (be exhaustive; add anything you find)
A. PROPERTY MECHANICS - re-derive independently from uk-move-financial-model §9-11 and the balance
   sheet. Both scenarios: HK-stay = live in DB flat + let Cecil Road; London = live in Cecil Road +
   let DB flat. Check: DB flat carrying cost (HK$25,827 mortgage split 12,138 interest/13,689
   principal + HK$2,054 mgmt + HK$1,196 rates); Cecil Road net rent (£2,194 take-home less £213
   mortgage, £46 insurance, UK rental tax); the £970 DB shortfall; the £60 agent fee; is the
   principal/equity treatment consistent across both sides? Is the -£117 London property figure right?
B. DOUBLE-COUNTING - the DB shortfall + agent fee were moved OUT of the "£635 adversarial correction
   bundle" and ONTO the property line, and the bundle was reduced to £475. Verify no item is counted
   twice AND nothing was dropped. Reconcile the bundle's components (FX, DB void, energy, dental,
   lumpy buffer) to the £475.
C. FX - 10:1 vs ~10.3. Which direction does it bias, and by how much across the HKD-denominated lines?
D. TAX - (i) non-resident-landlord personal allowance on Cecil Road rent (is it available to a British
   citizen? is the ~£178-199/mo figure right? note the source model contradicts itself: £360 vs £511
   interest credit); (ii) FIG 4-year exemption on the HK rent and the post-year-5 UK tax step-up
   (~£100-240/mo) - is the steady-state comparison silently assuming the 4-year shelter forever?
E. OMISSIONS - one-off moving costs (shipping, furnishing, tenant-eviction overlap); owner-occupier
   maintenance/repairs (owner states the London property has had heavy repairs recently - does the
   "cancels in the delta" claim hold?); DB flat void/vacancy risk; Cecil Road variable-rate reset risk;
   currency risk on HK-side income. Which are material?
F. DISCRETIONARY - are dining/groceries/utilities/transport/holidays honest, or has "held flat"
   hidden a real London premium (or, conversely, an unfair penalty)?
G. THE SCHOOL FEE - it is now larger than the entire net saving. Is £650/mo the right HK figure
   (source model says HK$6,500)? Is booking the base case at the full £650 (she defaults) correct,
   vs the contingent £305? Does moving to a free UK school change any separate child-maintenance
   obligation?
H. THE HALF-PRICE-THEN-NEUTRAL ARC - the number went £4,000 -> £1,000 -> £390 -> £325 -> "neutral".
   Is £325 a stable honest estimate or a way-station? Give YOUR central figure and an honest range.

OUTPUT (structured)
1. VERDICT: is the current model DEFENSIBLE, still PRO-MOVE BIASED, or now OVER-CORRECTED against
   the move? State your own central monthly cost delta + range.
2. CORRECTIONS TABLE: each error | direction (favours move / favours stay) | £/mo magnitude.
3. MATERIAL OMISSIONS: with rough £ figures and whether monthly or one-off.
4. THE ONE THING the model most wants to believe that is least supported by evidence.
5. WHAT SURVIVES: state plainly what is genuinely solid, so it is not over-discounted.
6. FINAL TASK - THE REOPEN CONDITION: the decision journal set a pre-agreed condition that the
   committed "move" decision may be legitimately reopened IF (a) London is not materially cheaper
   AND (b) London job odds are not materially better. Using Test A (cost) and Test B
   (uk-150k-feasibility-report), state whether BOTH legs are now met, and therefore whether a
   formal reopen is warranted under the F-N-M-T test in commitment-lock-protocol.md. Be explicit;
   do not hedge.
```

## Codex verdict

*(paste Codex's returned review here when it runs, then reconcile against the [[uk-vs-hk-cost-comparison#8. Adversarial review (Fable, 2026-07-08) - the current answer|Fable review]] and update Test A if warranted)*

## Related
- [[uk-vs-hk-cost-comparison|Test A - the document under review]]
- [[uk-150k-feasibility-report|Test B - UK income feasibility]]
- [[decision-journal|Decision Journal]] · [[commitment-lock-protocol|Commitment Lock Protocol]]
