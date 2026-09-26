This records the independent review of the v3 relocation savings spreadsheet. Julian requested it to check the revised rental-tax treatment before using the comparison; read the linked review for findings and corrections. Internal only, `send: NEVER`.

# Savings v3 Review

## Key Takeaways

- Serves [[uk-relocation-project]] and its financial comparison.
- As of 25 Sep 2026: review complete; findings in [[uk-relocation-savings-v3-codex-review-2026-09-25]]. Agreed spreadsheet repairs and appended runway tables completed and independently verified; completion records below.

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

### Runway extension authorised, 25 Sep 2026

Julian approved appending formula-based cash-burn/runway tables to the savings sheet, then explicitly authorised Sol to build and Luna to verify. Existing cells (including rows1:66), the cashflow spreadsheet and charts are outside this edit. Editable HKD inputs: cash721,000 and120,000; card bills1,504,40,839,10,384; retained ISAs3,265,990 and MPF1,244,699. Net cash must calculate to788,273. Runway uses the Zero salary scenarios, excludes MPF while staying in HK, guards non-positive burn and identifies retained July pot values. Done when all inputs drive formulas, every runway result is independently verified and the pre-edit snapshot proves existing cells unchanged. Verifiers: Luna independently, then parent handback; Julian reviews presentation.

### Housing split authorised, 26 Sep 2026

Julian chose the simplest split and resumed it after deleting redundant cashflow/burn rows: move occupied-home running costs out of the living-expense inputs and into savings property rows, while retaining mortgage principal/interest in cashflow. Move Malvern hotels to discretionary Transport. Retain the Housing supporting subtotal and add an excluding-housing expense output. Include TTI columns and preserve the lean exclusion of discretionary HK contents insurance. Sol implements both live sheets; Luna and parent verify unchanged annual savings, cumulative results, tax and both runway tables. Existing companion files describe the final split. No new financial assumptions or unrelated deletions.

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

## Runway tables completed, 25 Sep 2026

Appended [runway inputs and tables](https://docs.google.com/spreadsheets/d/1TS-ve2WfgcBfNYrEaZCbl-4De_JdqHSqQbm_CdSZojM/edit?gid=835277357&range=A68:D93) in rows68:93. Edit B69:B75 for cash balances, card bills, ISAs and MPF. Formula totals give cash841,000 less cards52,727 = net788,273; combined pots4,054,263 and5,298,962 HKD. ISA/MPF inputs retain July assumptions. No cashflow-sheet changes or chart added.

| Measure | London | Malvern | HK |
|---|---:|---:|---:|
| Monthly burn, HKD | 50,418.13 | 22,886.05 | 66,916.22 |
| Cash only, months | 15.6 | 34.4 | 11.8 |
| Cash + ISAs, years | 6.7 | 14.8 | 5.0 |
| Cash + ISAs + MPF, years | 8.8 | 19.3 | n/a while in HK |

Verification: Sol built; Luna independently reread live cells and compared 1,254 original cells in A1:S66 to the pre-edit snapshot, with zero differences. All16 numeric month/year outputs passed independent arithmetic, also checked by the parent. Formula guards cover non-positive burn. July brief expected runway is superseded by the updated net cash; HK burn66,915 is superseded by66,916.22 after the earlier contents correction. Existing source figures and validation cells are unchanged. Cash-only and combined-pot runway assume constant Zero-scenario burn, not a new time-varying forecast.

### Added-cell values and formulas

This manifest records every nonblank added cell; formulas reference editable inputs. B81:H81 and B93:L93 are merged note ranges within the appended area.

| Cell | Value or formula |
|---|---|
| A68 | `Runway inputs (HKD)` |
| A69 | `Cash balance 1` |
| B69 | `721000` |
| A70 | `Cash balance 2` |
| B70 | `120000` |
| A71 | `Credit card bill 1` |
| B71 | `1504` |
| A72 | `Credit card bill 2` |
| B72 | `40839` |
| A73 | `Credit card bill 3` |
| B73 | `10384` |
| A74 | `ISAs` |
| B74 | `3265990` |
| A75 | `MPF` |
| B75 | `1244699` |
| A76 | `Cash balances total` |
| B76 | `=SUM(B69:B70)` |
| A77 | `Credit card bills total` |
| B77 | `=SUM(B71:B73)` |
| A78 | `Net cash available` |
| B78 | `=B76-B77` |
| A79 | `Net cash + ISAs` |
| B79 | `=B78+B74` |
| A80 | `Net cash + ISAs + MPF` |
| B80 | `=B79+B75` |
| A81 | `Balance dates` |
| B81 | `Cash and cards supplied 25 Sep 2026; ISA and MPF values retain July 2026 assumptions.` |
| A83 | `Runway with no salary` |
| A84 | `Measure` |
| B84 | `London` |
| C84 | `Malvern` |
| D84 | `HK` |
| A85 | `Annual net savings (HKD)` |
| B85 | `=B31` |
| C85 | `=H31` |
| D85 | `=N31` |
| A86 | `Monthly burn (HKD)` |
| B86 | `=-B85/12` |
| C86 | `=-C85/12` |
| D86 | `=-D85/12` |
| A87 | `Cash only (months)` |
| B87 | `=IF(B86<=0,"No depletion",$B$78/B86)` |
| C87 | `=IF(C86<=0,"No depletion",$B$78/C86)` |
| D87 | `=IF(D86<=0,"No depletion",$B$78/D86)` |
| A88 | `Cash + ISAs (months)` |
| B88 | `=IF(B86<=0,"No depletion",$B$79/B86)` |
| C88 | `=IF(C86<=0,"No depletion",$B$79/C86)` |
| D88 | `=IF(D86<=0,"No depletion",$B$79/D86)` |
| A89 | `Cash + ISAs + MPF (months)` |
| B89 | `=IF(B86<=0,"No depletion",$B$80/B86)` |
| C89 | `=IF(C86<=0,"No depletion",$B$80/C86)` |
| D89 | `n/a while in HK` |
| A90 | `Cash only (years)` |
| B90 | `=IF(ISNUMBER(B87),B87/12,B87)` |
| C90 | `=IF(ISNUMBER(C87),C87/12,C87)` |
| D90 | `=IF(ISNUMBER(D87),D87/12,D87)` |
| A91 | `Cash + ISAs (years)` |
| B91 | `=IF(ISNUMBER(B88),B88/12,B88)` |
| C91 | `=IF(ISNUMBER(C88),C88/12,C88)` |
| D91 | `=IF(ISNUMBER(D88),D88/12,D88)` |
| A92 | `Cash + ISAs + MPF (years)` |
| B92 | `=IF(ISNUMBER(B89),B89/12,B89)` |
| C92 | `=IF(ISNUMBER(C89),C89/12,C89)` |
| D92 | `n/a while in HK` |
| A93 | `Assumptions` |
| B93 | `No salary; rental income and property tax per Zero location; constant burn; no investment returns; balances HKD; MPF accessible only on permanent departure from HK.` |

## Calculation explanation added, 25 Sep 2026

Julian requested plain-language calculation notes under the runway table. Appended A95:B101 (explanations merged across B:L): exact no-salary annual net savings from B31/H31/N31, included rental/property/living costs, monthly burn, available pots, months/years formulas and constant-burn limitations. Numerical explanations link to live cells with TEXT formulas so they remain current. Readback verified; original model and tables unchanged. Incremental token effort unmeasured.

## Lean runway added, 25 Sep 2026

Julian authorised a second table for lean burn. Appended A103:D117 in the savings sheet; previous tables and the cashflow sheet are unchanged. B105:D105 are editable snapshots of cashflow row175 in London/Malvern/HK order: 47,952.966667 / 44,142.966667 / 69,004.966667 HKD monthly. Notes explicitly say these inputs are not live-linked.

Lean annual savings adds back the original annual living costs to B31/H31/N31 and subtracts lean inputs x12, preserving rental/tax treatment. Monthly burn is 28,136.63 / 4,744.55 / 49,422.88 HKD; cash-only runway28.0 / 166.1 / 15.9 months. Uses the existing balances; MPF excluded in HK and non-positive burn guarded. Classification follows the source exactly, including exclusion of Malvern hotels and HK contents insurance. Very long combined-pot runway is constant-burn arithmetic, not a changing lifetime forecast.

Verification: live readback plus separate reconciliation against the source discretionary totals and all16 numeric runway outputs passed. Incremental tokens unmeasured.

## TTI + UNI scenario added, 26 Sep 2026

Julian confirmed GBP230,000 annual gross salary (row15), existing HK school fees retained, plus GBP90,000 reserved for future university over the first six years. Added column T, labelled TTI + UNI. Inputs B120=90,000, B121=6; B122 calculates annual HKD reserve using B56. HK salary/property treatment retained explicitly despite the different column label.

At FX10: annual university reserve150,000HKD; salary tax345,000HKD (standard-rate cap); annual unearmarked savings1,002,005.40HKD in years1:6, then1,152,005.40 from year7. Ten-year unearmarked savings10,620,054HKD, with900,000HKD separately reserved. Reserve is not current university expenditure. Salary continues throughout; retiring at61 is not assumed. T26 includes the reserve for initial-year presentation; notes explain the timing.

Verification: all10 cumulative outputs independently recalculated, both scenario checks OK, zero NI and HK non-resident UK-property treatment verified. Original source column S unchanged. Incremental token effort unmeasured.

## TTI(S) + UNI added, 26 Sep 2026

Julian authorised column U at GBP250,000 annual gross, comprising GBP230,000 base plus GBP20,000 schooling support. Treated as taxable gross salary; existing school expenses and six-year university reserve unchanged. Rationale in row125 and [[uk-relocation-savings-comparison]]. All10 cumulative results independently verified; both validation checks OK. Annual available savings1,172,005.40HKD for years1:6 and1,322,005.40 thereafter. Incremental tokens unmeasured.

## Cash + MPF runway added, 26 Sep 2026

User brief authorised the fourth pot combination and native row insertion with reference checks. Net cash+MPF is HKD2,032,972. Full runway: London40.3222 months/3.3602 years, Malvern88.8302/7.4025. Lean: London72.2536/6.0211, Malvern428.4857/35.7071. HK is n/a while in HK. Matches requested rounded expectations (lean Malvern428.5 months at one decimal).

Parent independently reread live new formulas/results and compared all60 row12/31/32 results against pre-edit snapshot: unchanged. Builder checked original lower-block results/styles. Native inserts automatically adjusted24 T/U formula references to university parameters now B125:B127; original logic/results unchanged, so formulas above the block are reference-adjusted rather than text-identical. Explanation now lists four pot combinations and describes spending pension before ISAs. No housing changes in this operation.

### Added cells (final coordinates)

| Cell | Value/formula |
|---|---|
| A79 | `Net cash + MPF` |
| B79 | `=B78+B75` |
| A89 | `Cash + MPF (months)` |
| B89 | `=IF(B87<=0,"No depletion",$B$79/B87)` |
| C89 | `=IF(C87<=0,"No depletion",$B$79/C87)` |
| D89 | `n/a while in HK` |
| A93 | `Cash + MPF (years)` |
| B93 | `=IF(ISNUMBER(B89),B89/12,B89)` |
| C93 | `=IF(ISNUMBER(C89),C89/12,C89)` |
| D93 | `n/a while in HK` |
| A113 | `Cash + MPF (months)` |
| B113 | `=IF(B111<=0,"No depletion",$B$79/B111)` |
| C113 | `=IF(C111<=0,"No depletion",$B$79/C111)` |
| D113 | `n/a while in HK` |
| A117 | `Cash + MPF (years)` |
| B117 | `=IF(ISNUMBER(B113),B113/12,B113)` |
| C117 | `=IF(ISNUMBER(C113),C113/12,C113)` |
| D117 | `n/a while in HK` |

## Housing split completed, 26 Sep 2026

User resumed the agreed split after deleting redundant cashflow/burn blocks, then requested cheaper subagents. Sol stalled without edits and was stopped. Parent captured fresh snapshots and gave Luna an exact implementation brief; Luna completed the changes. Parent independently compared440 model outputs, including all20 scenario annual savings,200 cumulative results, taxes, validation rows and both runway tables, with no differences above0.001HKD.

- Cashflow: hotel moved from row111 to139, discretionary Transport; Housing remains a supporting breakdown at113, HK3,726.833333/month, London2,210, Malvern0. Original total at168 unchanged. Full excluding-housing output169: HK82,771.466667, London68,024.466667, Malvern62,284.466667. Lean output170: HK65,479.966667, London45,742.966667, Malvern44,142.966667. Mortgages remain in the living budget.
- Savings: B64:B66 use full excluding-housing snapshots; B18:G18 contain GBP2,652/year occupied UK costs; N20:U20 contain HKD44,722/year occupied HK costs, including both TTI columns. Letting costs unchanged. Lean B108:D108 use excluding-housing inputs; D110 adds back B132=HKD2,422/year so discretionary HK contents insurance remains excluded. Notes and both companion MDs updated.
- Independent Luna verification also passed all savings/runway invariants. A124:C124 (unused HK Tax estimate, no scenario amounts) was cleared between snapshots outside the delegate's write ranges; treated as an external edit and left intact, consistent with Julian's ongoing cleanup. The row was not structurally deleted.
- Row139 category label corrected to Transport discretionary after parent readback. Source hotel subtotal auto-expansion was caught and repaired during the move, before final verification.

## Time and Token Log

| Date | Who / what | Effort | Notes |
|---|---|---|---|
| 2026-09-25 | Codex interactive thread | 214,260 tokens measured at bookkeeping checkpoint | Per-thread peak `total_usage_tokens` in `~/.codex/logs_2.sqlite`; thread `01a0d888-485e-78b0-8818-2f76c850d1ad`. Includes earlier column-edit and connector discussion turns; review-only effort is unmeasured. No external CLI or subagent run. |
| 2026-09-25 | Codex follow-up verification | Unmeasured incremental tokens | Same thread; live reads, formula comparisons and 198 savings checks. |
| 2026-09-25 | Parent thread through delegated repairs | 247,200 cumulative tokens; 32,940 since prior measured checkpoint | Includes intervening follow-ups; do not add the cumulative total to the earlier checkpoint. Delegate token effort unmeasured. |
| 2026-09-25 | Runway build and independent review | Incremental effort unmeasured | Parent cumulative log checkpoint 247200; no new usage beyond prior checkpoint exposed. Sol/Luna delegate totals unavailable. |
| 2026-09-26 | Housing split parent checkpoint | 236269 cumulative tokens reported by current thread log | Not an incremental task total; not summed with prior checkpoints. Delegate usage unmeasured. |
| 2026-09-25/26 | Julian, attended | 480 min (about 8 h over two days) | Self-reported at handback 26 Sep. Much of it re-reading old files, understanding their structure, deciding the restructure, and relaying edits between Claude and Codex. |
| 2026-09-25/26 | Claude interactive session (Fable 5.1) | 7,731,749 tokens (output 550,383 + cache-write input 7,181,366) | Session `e0e3227a`, 458 assistant messages, summed from the transcript JSONL. Cache reads (176.7M) omitted as not effort. The same session also carried the [[tax-rental-incomes]] work on the morning of 25 Sep, which has no deliverable file; roughly a third of the session by message count. |
| 2026-09-25/26 | Codex, later threads | unmeasured | `~/.codex/logs_2.sqlite` rows for the later threads did not expose `total_usage_tokens`; Julian reports running out of Codex allowance three times. |

## Session Synopsis

**Julian (26 Sep 2026): 4 / 5.** About eight hours over two days, spread across getting my head round old files I hadn't seen for a while, understanding how they were structured, and deciding how to restructure them. Less time understanding new concepts than the tax document; this one was many iterations working out the best structure as we went. The output has been good and there were far fewer mistakes than with the tax work. The reason it is a 4 and not a 5: I had to sit in the middle. Claude cannot edit Google Sheets, so I ran two windows and pasted Claude's proposed updates into Codex, with several iterations each way, and I ran out of Codex allowance three times on the $20 subscription because it was doing the heavy lifting while the thinking was still happening in Claude on the $100 subscription. That is frustrating. In future maybe do the work directly in Codex and have Claude review it.

**Claude (beneath, 26 Sep 2026).** Fair rating. The substantive numbers were right and stayed right, and the two-agent relay was the main cost. Two things on my side cost time: I introduced the double-count at the living-cost step and then declared the sheet done before re-reading the scope amendment that would have caught it, and I asked Julian for evidence twice when my connector's cached preview was the problem, not his sheet. The relay itself was avoidable: sharing the sheets with the service account would have let me edit in place. The rest of the iterations were genuine design decisions (housing split, lean versus full, what belongs in which sheet) that only Julian could make, and those went quickly once the numbers were visible in one table.
