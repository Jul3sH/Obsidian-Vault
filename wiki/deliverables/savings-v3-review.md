This records the independent review of the v3 relocation savings spreadsheet. Julian requested it to check the revised rental-tax treatment before using the comparison; read the linked review for findings and corrections. Internal only, `send: NEVER`.

# Savings v3 Review

## Key Takeaways

- Serves [[uk-relocation-project]] and its financial comparison.
- As of 25 Sep 2026: review complete; findings in [[uk-relocation-savings-v3-codex-review-2026-09-25]]. Agreed savings and cashflow corrections completed and independently verified; completion record below.

## Prompt Zero

Julian approved this record and the supplied briefing as the scope on 25 Sep 2026.

> Please review [the spreadsheet] referring to tax-rental-incomes.md and your previous adversarial review of the file tax-rental-incomes-codex-review-2026-09-25.md and this [briefing].

- **Outcome:** independently check all 18 v3 scenarios, property-tax rows, FIG choices, salary tax at £135k, annual savings and their cashflow inputs; identify corrected amounts and direction of error.
- **Non-goals:** no v2 review, no reopening settled findings in [[tax-rental-incomes-codex-review-2026-09-25]], no edits to the sheets or tax source.
- **Inputs:** accept the briefing's revised rents and annual expense inputs, including the known mismatch with the tax article's older tables. Treat residence and FIG eligibility as conditional.
- **Good enough:** every scenario checked by independent arithmetic; material discrepancies have cell references, amounts and direction; review saved and linked from the project.
- **Depth:** one bounded review, with official sources for tax mechanics; no broader relocation recommendation.
- **Verifier:** Codex independently recalculates the sheet; Julian adjudicates the findings. No sampling: all 18 scenarios.
- **Load-bearing assumption:** v3 models gross employment salary, not umbrella assignment revenue, with the stated tax-residence basis and no additional reliefs.

### Scope amendment, 25 Sep 2026

Julian authorised the follow-on corrections: remove the duplicate Wills cost and HK Oyster; restore occupied-home Housing costs with the specified insurance/council-tax corrections; remove let-property costs from cashflow; refresh savings inputs. Prior agreed corrections cover FIG expiry, the HK allowance and formula-based taxes, with every tax formula validated against the reviewed fixed values before replacement. This supersedes the original no-sheet-edits restriction for these two sheets only. Occupied-home expenses must be removed from the savings property rows when moved to Housing, so each cost is counted once. Verification: all 18 scenarios against frozen pre-change values, then independent recalculation of the corrected model; Julian's sign-off remains the handback check.

## Follow-up verification, 25 Sep 2026 (before delegated repairs)

Read-only check of Julian's updated savings tab: all 18 annual and 180 cumulative results agree with separate arithmetic. All 108 tax/conversion formulas match the staged formulas previously tested against fixed values (100 matches; eight intentional HKD 4 NI rounding corrections). HK allowance 145,000, FIG expiry after Y4, and removal of occupied-home expenses from property rows are correct at the current assumptions.

Remaining savings items: B61:B63 do not drive formulas, so FIG always starts in Y1; rows 31/32 hardcode FX 10 rather than B56. B66 should be 86,498.30 using source contents estimate C110 (201.833333/month), versus current 86,497.47. Notes B45/B46 need aligning with occupied-home costs being in living expenses and source cashflow still awaiting correction.

Cashflow edits outstanding: clear duplicate E157:G157 and HK Oyster E135; HK E102:E104 = 2054, 1196, 275 and E110 = C110; London F106:F108 = 1640, 180, 390. Clear corresponding let-property costs in other location columns and F110. Restore E109:G109 to sums of rows 101:108. Keep Malvern hotel G111 and mortgage principal/interest. Resulting monthly expense totals: HK 86,498.30, London 70,234.466667, Malvern 62,284.466667 HKD. Do not restore occupied-home charges to savings property rows 18/20.

Cashflow F165 remains 23,750 versus gross HK rent 27,000 in savings, and rental notes still point to Housing expenses. Reconcile before using cashflow row 183 as a complete rental cashflow; expense row 181 is unaffected.

## Delegated repairs completed, 25 Sep 2026

Julian explicitly authorised Sol/Luna delegation for the agreed changes. The savings delegate was requested on gpt-6-sol; the cashflow delegate on gpt-6-luna. Their tools do not expose runtime model identity for independent confirmation. Sol was assigned formula dependencies and scenario tests; Luna received exact cell/value edits. The parent retained independent cross-sheet verification. No additional agents were spawned.

- Savings: FIG dates/window B61:B63 now control annual tax selection and cumulative projections; rows31/32 use B56 for FX. Monthly inputs B64:B66 match corrected cashflow totals. Notes updated to explain the source snapshot, owner costs and FIG timing.
- Cashflow: duplicate Wills and HK Oyster removed; occupied-home housing corrected; let-property charges removed from scenario housing columns; housing totals restored. Mortgage principal/interest and Malvern hotel retained.
- Verification: parent independently read both live sheets and recalculated all 18 annual and 180 cumulative savings results with no discrepancies or formula errors. Source totals and savings inputs agree to floating-point precision. Delegate tested projection start2028, expired FIG2031 and FX12, then restored start2027 and FX10. Existing formats preserved; API formatting inspection used because CUA was unavailable.
- As of 25 Sep 2026: all agreed repairs above are complete. Cashflow rental-income rows164:173 remain outside this edit: F165 and notes still require reconciliation before using row183 as a complete net-rental cashflow. The corrected expense row181 and savings comparison do not depend on those income rows.

## Time and Token Log

| Date | Who / what | Effort | Notes |
|---|---|---|---|
| 2026-09-25 | Codex interactive thread | 214,260 tokens measured at bookkeeping checkpoint | Per-thread peak `total_usage_tokens` in `~/.codex/logs_2.sqlite`; thread `01a0d888-485e-78b0-8818-2f76c850d1ad`. Includes earlier column-edit and connector discussion turns; review-only effort is unmeasured. No external CLI or subagent run. |
| 2026-09-25 | Codex follow-up verification | Unmeasured incremental tokens | Same thread; live reads, formula comparisons and 198 savings checks. |
| 2026-09-25 | Parent thread through delegated repairs | 247,200 cumulative tokens; 32,940 since prior measured checkpoint | Includes intervening follow-ups; do not add the cumulative total to the earlier checkpoint. Delegate token effort unmeasured. |
| 2026-09-25 | Julian, attended | Unreported | Awaiting Julian's own minutes at handback. |

## Session Synopsis
