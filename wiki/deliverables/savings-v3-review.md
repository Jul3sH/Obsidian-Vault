This records the independent review of the v3 relocation savings spreadsheet. Julian requested it to check the revised rental-tax treatment before using the comparison; read the linked review for findings and corrections. Internal only, `send: NEVER`.

# Savings v3 Review

## Key Takeaways

- Serves [[uk-relocation-project]] and its financial comparison.
- As of 25 Sep 2026: review complete; findings in [[uk-relocation-savings-v3-codex-review-2026-09-25]]. Agreed spreadsheet repairs and appended runway tables completed and independently verified; completion records below.
- As of 27 Sep 2026: Claude cross-check of the restored expense structure passed; no material defects, no sheet change. Section below.
- As of 27 Sep 2026, later: university reserve built into every column of the sheet by Codex; companion note re-read from the sheet. HK reserve total confirmed as 160,000. Section below.

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

### Restored split authorised, 26 Sep 2026

Julian instructed: non-deductible expenses remain in cashflow living expenses; property expense rows contain rental expenses only. Restore occupied costs to living inputs, preserve mortgage handling and distinguish UK overseas-property deductions from HK statutory Property Tax. Parent implements and verifies all20 scenarios and both runway tables. Supersedes the earlier housing transfer.

### Companion restructure authorised, 27 Sep 2026

Julian confirmed he reads the savings companion and sheet and opens the expenses sheet only when a cost may have changed, so both must be self-contained. Scope: move the model inputs, assumptions, mirrored tables and runway mechanics from uk-relocation-cashflows into [[uk-relocation-savings-comparison]]; add the "What is deductible where" table there; slim the remainder to an expenses-sheet companion and rename it [[uk-relocation-expenses]]; rename the Google Sheet to UK Relocation Expenses (Julian); repoint every inbound link. No spreadsheet values change.

### Visible rules authorised, 27 Sep 2026

Julian requested subagents and clear rules within both spreadsheets. Luna adds visible rules in unused space; parent checks wording and unchanged existing calculations. No numerical assumptions change.

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

## Occupied-home costs restored, 26 Sep 2026

- Savings B18:G18 and N20:U20 zero; rental inputs retained. B64:B66 restored from cashflow168: 70,234.466667 / 62,284.466667 / 86,498.30. Lean B108:D108 restored from164: 47,952.966667 / 44,142.966667 / 69,004.966667. D110 now `=N31+N26-D108*12`; obsolete A132:B132 cleared.
- Cashflow housing remains part of living costs. Obsolete excluding-housing outputs A169:H170 cleared without deleting rows. Source notes identify full168 and lean164; hotels remain Transport.
- Property labels/notes distinguish rental cash expenses used for UK rental profit from HK Property Tax's rates plus statutory allowance. Occupied-home costs no longer enter property-tax expense rows. Existing annual rental inputs retained, not reconstructed from rounded monthly descriptions.
- Verification: fresh live before/after comparison of440 outputs, zero differences above0.001 and no formula errors. All40 validation cells remain OK. Formatting preserved through field-specific writes; API-only visual check. No broader tax-rate or university-reserve changes.
- Remaining evidence point as of26 Sep: cashflow calls its HK charge "Gov rates & rent" while tax input B59 treats HKD14,348 as rates. Confirm the rates-only component from the bill; government rent must not reduce HK Property Tax. No unsupported numerical change made.

## Visible rules added, 27 Sep 2026

Luna added matching rules panels at savings B134:H143 and cashflow B170:H179: occupied-home versus rental costs, UK versus HK tax deductions, count each cost once, mortgage treatment, full/lean source rows and manual refreshes, and rates-only confirmation. HMRC/IRD links included. Parent reviewed all wording and compared all existing cell values and formulas across savings A1:U132 and cashflow A1:H168: zero differences. New panels use wrapped merged cells; API formatting checked, native render unverified.

## Claude cross-check of the restored structure, 27 Sep 2026

Read-only review by Claude (Fable 5.1) of the 26 to 27 Sep handover. Both live sheets were read by value through the Drive connector (formulas not visible, so formula preservation rests on Codex's 440-output comparison), plus the four companion files.

**Verdict: the expense structure is right, and the two sheets agree with each other and with the companions. No spreadsheet change needed.**

Confirmed by independent arithmetic:
- All four living inputs re-derived from the itemised cashflow to the cent (full 70,234.47 / 62,284.47 / 86,498.30; lean 47,952.97 / 44,142.97 / 69,004.97); annual living rows equal x12.
- Each property cost appears once per scenario: occupied-home costs sit in cashflow Housing (HK 3,726.83, London 2,210, Malvern 0) with savings rows 18/20 zero for the occupied home; letting costs appear only in rows 18/20 when let. Mortgage principal and interest are in cashflow only; the UK 22% interest credit and the HK no-deduction are both correct.
- Jurisdiction split correct: row 20 (49,046, rates included) feeds the UK overseas-property profit; HK Property Tax uses B59 rates and the 20% statutory allowance only. Sheet tax figures (Lon 135k 60,026; non-resident Cecil 23,615; Lon Zero 0) match the fuller-expense-set figures in [[tax-rental-incomes]] §3.
- Zero-column annual savings, HK Property Tax and both runway tables re-derived by hand; all agree.

Findings, none material to the location ranking:
1. **Rates versus government rent is bounded at +HK$646/yr.** Worst case (14,348 is the combined 5% rates plus 3% government rent bill) puts rates at 8,968 and HK Property Tax at 37,804. In salaried columns the extra HK tax becomes extra UK credit, so the combined bill is unchanged; only the Zero columns move, and cash-only runway by under 0.1 month. Plausibility favours rates-only: 14,348 at 5% implies a rateable value of about HK$23,900/mo, consistent with a HK$22-27k rent; at 8% it implies about HK$14,900/mo, too low. Confirm from the RVD demand note, which itemises the two. Downgraded from unresolved input to a bill check.
2. **[[tax-rental-incomes]] headline tables lag the sheet.** §1, §2 and Key Takeaways quote £6,475 / £152 / £2,343 on the narrower expense set; the sheet uses the fuller set (£6,003 / £0 / £2,361), as the article's own §3 note anticipates. Refresh them, or anyone quoting the article will differ from the model by about £470/yr. Not edited here.
3. **[[uk-relocation-project]] Trusted Artifacts described cashflow row 177 as the net-of-property-income cashflow.** Stale: that block was deleted 26 Sep and row 177 is now inside the rules panel. Corrected in this operation to rows 168 (full) and 164 (lean).
4. **[[uk-relocation-expenses]] (then uk-relocation-cashflows) §3 letting-cost lines were reconstructed from rounded monthly figures** (49,050 and £4,141 against sheet inputs 49,046 and 4,140). Restated on the annual basis in this operation.
5. Cosmetic, cashflow sheet, no numeric effect: column C estimates "HK Lettings fee 1,125" and "UK Letting/management 2,460" are stale against the savings inputs and unused; "Weekly Octopus when working" (E) is labelled non-optional but summed as discretionary, as is the unlabelled London Oyster line. Clear or relabel at the next budget refresh.

Not checked: formulas (values only); FIG eligibility and residence, which remain conditional per Prompt Zero.

## Companion restructure completed, 27 Sep 2026

- [[uk-relocation-savings-comparison]]: §2 gains "What is deductible where"; new §6 model inputs and assumptions (two sheets, property income by scenario, assumptions, living-cost inputs) and §7 mirrored tables and runway mechanics, moved verbatim from the old model companion; change log and how-to-update renumbered §8 and §9; purpose block and map updated.
- uk-relocation-cashflows renamed [[uk-relocation-expenses]] (git mv, history kept) and rewritten as the expenses-sheet companion: structure, totals rows 164/166/168, what differs by location, what is not in the sheet, refresh procedure, change log.
- Repointed: all `[[uk-relocation-cashflows` links renamed globally; live references in [[uk-move-financial-model]], [[tax-rental-incomes]], [[uktax-srt-fy26-27]], the HK U-turn reopen note (since folded into the project status log, 27 Sep) and the July number check now point at the savings comparison where the model content lives; finance index and project File Map and Trusted Artifacts rewritten. Historical status-log and ops-log rows keep the renamed link or their dated backticked mention.
- Google Sheet 1HP-4Gm7... renamed UK Relocation Expenses by Julian; file ID unchanged.

## University reserve built in, 27 Sep 2026

- Codex added to the savings sheet: "Annual net savings before university reserve", "Annual university reserve, years 1 to 6" (HK$66,667 in every UK column, HK$266,667 in every HK column) and "Annual available savings after reserve"; reserve inputs block (baseline GBP 40,000 all locations, additional GBP 120,000 if living in HK, six years); cumulative rows exclude the reserve in years 1 to 6; both runway tables are piecewise (reserve in the burn for six years, then not). The old GBP 15,000 reserve inside the TTI columns' living expenses was removed. All validation checks read OK; Codex reported the checks pass including the point where contributions stop.
- Claude read the sheet, then a subagent re-read every table in [[uk-relocation-savings-comparison]] from it (§1 to §9, change-log row added). Two §2 tables (cumulative after four and ten years) had been deleted by a Claude edit earlier the same day and were rebuilt from the sheet.
- Downstream: [[HK-Return-BRAIND]] executive summary (all six rows now sheet cells), [[Malvern-BRAIND]] Finance row, [[uk-relocation-project]] Trusted Artifacts and status.
- Confirmed by Julian at handback, 27 Sep: the HK reserve total is GBP 160,000 (40,000 baseline plus 120,000 additional), as the sheet carries it.

## Sheet changes applied, 6 Oct 2026

Julian authorised [[uk-relocation-savings-comparison]] §10 changes 1 to 5. Rows matched by column A labels. Written cells: V1:W1, T14:U14, V2, W2:W11, A56:B56. All 17 read back exactly; all 40 validation checks OK. W differences HK$0 to HK$3 are permitted rounding. Snapshot A1:Z160 confirms other entered values and all cell formats unchanged. No row insertion or formatting writes.

## Revised §10 applied, 6 Oct 2026

Changes 1, 2, 3, 4, 5, 6, 6b and 7 applied by column A labels. All 41 written cells match. All 40 validation checks OK. Maximum expected-value difference: W HK$3; X/Y HK$4, allowed rounding. New assumption row 57 inserted after W assumption. Before/after mapped comparison confirms existing results and formats preserved, with automatic reference adjustments only. Final year 6/8/10 values are in [[uk-relocation-savings-comparison]] §2.

## Time and Token Log

| Date | Who / what | Effort | Notes |
|---|---|---|---|
| 2026-10-06 | Codex, savings chart | Incremental tokens unmeasured | Added native line chart on new tab for E/K/M/V/W/X/Y, sourced directly from Y1 to Y10. Chart spec verified by API; existing cells unchanged. |
| 2026-10-06 | Codex, revised §10 including X/Y | Incremental tokens unmeasured | Exact native writes, 41-cell readback, mapped preservation and 30 expected-value checks. Task-specific usage unavailable. |
| 2026-10-06 | Codex, §10 sheet changes and readback | Incremental tokens unmeasured | Native edits and full bounded before/after comparison; task-specific usage unavailable. |
| 2026-09-27 | Julian, attended | 15 min | Self-reported at handback. University reserve piece: briefing Codex, reviewing the sheet result, handing the companion update to Claude. |
| 2026-09-27 | Codex, university reserve build | 699,140 tokens | Sum of per-thread peak `total_usage_tokens` in `~/.codex/logs_2.sqlite` for the four threads active 15:53 to 15:56 on 27 Sep (197,900 + 188,499 + 183,298 + 129,443). Earlier 06:07 threads excluded as a different task. |
| 2026-09-27 | Claude subagent, companion note re-read (Fable 5.1) | 126,073 tokens | One delegated pass over all nine sections of the companion note. Parent-session tokens for this piece are inside the session total logged in [[HK-Return-BRAIND]] and are not separated. |
| 2026-09-27 | Julian, attended | 30 min | Self-reported at handback 27 Sep: reviewing the handover, deciding the deductibility table and the companion restructure. |
| 2026-09-27 | Claude cross-check and companion restructure session (Fable 5.1) | 1,118,916 tokens (output 216,693 + cache-write 902,223) | Session `c82c95e1`, 60 assistant messages, summed from the transcript JSONL at the restructure handback. Cache reads (3.5M) omitted as not effort. Julian's attended minutes: pending at handback. |
| 2026-09-27 | Luna rules panels and parent verification | Incremental tokens unmeasured | Latest log checkpoint128541 for thread01a0d888-485e-78b0-8818-2f76c850d1ad is cumulative and not comparable with prior checkpoints; delegate usage unavailable. |
| 2026-09-26 | Codex restored housing split | Unmeasured incremental tokens | Direct native edits,440-output before/after verification; no new subagents. |
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

**Julian (27 Sep 2026): 3 / 5.** Thirty minutes of my time. Three because it used a lot more tokens than it should have. Important to log: this was a bit of refactoring of existing documents and it took far more tokens than it should have because Claude did not use subagents.

**Claude (beneath, 27 Sep 2026).** Agreed. The review itself was cheap and right; the restructure was mechanical (move sections, rename, repoint ten links) and I ran it inline in the main thread, which cost about 1.1M effort tokens for work a briefed subagent on a cheaper model could have done. Saved as the feedback-delegate-execution-to-subagents memory; the instance is logged against the routing card.

**Julian (27 Sep 2026, university reserve piece): 4 / 5.** Fifteen minutes. No further comment given.

**Claude (beneath, 27 Sep 2026).** Fair. The sheet-to-note handoff worked: Codex built the reserve, the subagent re-read every section from figures in its brief, and the checks came back clean. The point off is mine: an edit of mine earlier in the day had deleted two tables from the note, and it was the subagent's report, not my own checking, that found it. The gap between the HK return and the same job from Malvern was unchanged by the reserve, which is the finding that mattered.

