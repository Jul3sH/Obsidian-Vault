---
type: adversarial-review
reviewer: Fable
created: 2026-07-13
authority: fable-adversarial-review
decision: UK Relocation Decision - full-record consistency, alignment and completeness audit
scope: overnight unattended run; no source files edited; all corrections proposed here only
sources-reviewed: [uk-move-financial-model, uk-relocation-decision, decision-journal, uk-move-decision-risk-register-2026-07-12.xlsx, uk-move-risk-register-2026-07-12.xlsx, uk-vs-hk-income-floor-reconciliation-2026-07-09, uk-vs-hk-income-floor-reconciliation-2026-07-09.xlsx, uk-vs-hk-income-floor-reconciliation-claude-review-2026-07-09, uk-vs-hk-income-floor-reconciliation-codex-review-2026-07-10, financial-status-2026-07-07, financial-status-2026-06-22, uk-vs-hk-cost-comparison, london-monthly-budget, budget, money-tracker, uk-150k-feasibility-report, uk-150k-feasibility-jh-clarifications-2026-07-09, uk-job-market-remote-hybrid-split-2026-07-11, uk-job-market-remote-hybrid-split-2026-07-11.xlsx, cleared-defence-cyber-lane-assessment, target-role-profile, uk-ir35-contracting-feasibility-2026, uk-vs-hk-earning-comparison, uk-vs-hk-earning-comparison-jh-clarifications-2026-07-09, Uk-vs-hk-earnings-feasibility-codex-review-2026-07-09, fable-review, fable-review-london-vs-malvern, fable-review-unknowns, fable-review-malvern-reopen-2026-07-10, fable-review-jobdata-2026-07-11, london-vs-malvern, why-london, risks, decision-criteria-matrix, commitment-lock-protocol, sophia, clodagh, joanne, hanley-castle-high-school, sophia-malvern-activities, adzuna-uk-job-market-data-source, uk-move workspace _index, finance _index, career _index, log-2026-Q3]
tags: [uk-relocation, fable-review, consistency-audit, risk-register]
---

# Fable Consistency Review - UK Relocation Decision Record (13 Jul 2026, overnight)

> Unattended overnight audit of the entire UK relocation evidence base, with the new §0 canonical money summary in [[uk-move-financial-model]] scrutinised hardest, plus the risk register and RAID register (.xlsx). NO source file was edited; every correction is proposed in the tables below for the morning session. Hostile in both directions per [[multi-agent-protocol]].

---

## 1. Executive summary

1. **The single most important finding: the record is running on TWO different worlds at once.** On 12 Jul Julian decided to KEEP the Cecil Road tenants with notice timed for an **Aug 2027** move (RAID DEC-3; project status log 12 Jul). That decision makes "London-direct: live in Cecil Road now" **physically unavailable until Aug 2027**, and the RAID register itself says so ("'London-direct now' would need paid London rent until Cecil frees Aug 2027"). Yet the §0 canonical summary, written the day AFTER (13 Jul), still models London-direct as "lives in Cecil Road" with a £0-6k Sept-Nov temp-accommodation line, and the project Status header (frozen at 11 Jul) still says "the interim is DEMOTED; London-direct is the safer default". The canonical money surface, the project header, and the decision journal all describe a world the 12 Jul Cecil decision ended. Either DEC-3 stands (then §0's London-direct column, the pot derivation, and the header verdict are all wrong) or DEC-3 does not stand (then the RAID register and the 12 Jul log row are wrong). This must be resolved first; everything else is detail.
2. **Verdict on §0: NOT trustable as-is.** Its arithmetic is mostly sound and I could re-derive the load-bearing burns (£4,630 lean and £5,450 settled verified against the income-floor workbook formulas), but it contains one outright numerical error (Malvern runway incl. MPF "~8 yr+" uses the superseded £1,683 burn; the honest figure at its own £2,450-2,700 burn is ~5.5-6.1 yr), one internal contradiction (§0 says Malvern liquid runway ~20-22 mo while §10 in the same file says "~30 months"), a Banked/Hoped rule violation (Stay-HK pot includes the unbanked £12,475 rebate), a mis-stated build-up (settled is lean + £820, not lean + £900), stale Key Takeaways at the bottom of the same file that contradict §0, and, above all, the DEC-3 blindness in point 1. Detail in §3.
3. **The risk register .xlsx has NO formulas at all.** Every Score and the TOTAL row are hardcoded numbers, while the sheet's own instructions claim scores "recompute on I x P (recalc in Excel)". They will not. The income-floor workbook has the opposite defect: 92 formulas, none with cached values, so every computed cell reads empty in any tool that does not recalculate. Both flagged prominently in §4.
4. **The standing verdict is inconsistent across the four decision surfaces.** Project header (11 Jul): interim demoted, London-direct default. RAID register (12 Jul): "a genuine trade... the interim is more viable than the red-team's demotion implied... now Julian's judgment call". Decision journal: stops at 10-11 Jul, records neither the risk-register judgment nor DEC-3. §0 (13 Jul): silent on both. A morning reader gets a different answer depending on which file they open.
5. **The reassurance docs are dangerously stale.** [[why-london]] (the anchor doc Julian is instructed to re-read when doubting) still says ~£216k spendable and ~4 years of runway; [[london-monthly-budget]] still headlines £4,550/mo and "funded ~4 years"; [[london-vs-malvern]] (status: live) still carries £3,339/£905 burns and "funded ~5 yrs". The commitment-lock protocol requires anchors to hold "honest post-adversarial-review numbers only"; the anchor currently fails its own rule by roughly a factor of four on runway.
6. **Confirmation-amplification is still live, now in the interim's favour on narrative and in London's favour by omission.** The 12-13 Jul surfaces (RAID position, [JH] downgrades, "kills the drift trap", "natural bridge") all lean toward the interim, the direction Julian moved on 12 Jul, and the Sophia-midweek downgrade cites a "was to be 50/50 with her mother anyway" counterfactual that the wiki record contradicts. Meanwhile §0's failure to price DEC-3's London-rent consequence flatters London-direct. Both directions flagged in §5 and §6.
7. The floor-job mitigation ("~£77k covers costs") that underpins the London-direct synthesis is computed on the superseded £4,550 burn; nobody has recomputed it at £4,630/£5,450, let alone at a DEC-3 London-rent burn. At £5,450 the cash-flow floor is roughly £90-95k gross, which is at-median rather than comfortably below it, and materially weakens the mitigation.
8. Bottom line for the morning: fix the §0/DEC-3 collision, restate the project header, write the two missing journal entries (risk-register judgment; Cecil decision), and re-baseline the three stale reassurance docs. Then §0 can genuinely be the single source of truth. The prioritised list is §8.

---

## 2. Master discrepancy table (sorted by decision impact)

Canonical = what §0 or the latest reviewed source says; where §0 itself is wrong, the "correct" column says so.

| # | Figure | Canonical / correct value | Files that disagree and what they say | Proposed fix | Impact |
|---|---|---|---|---|---|
| D1 | **London-direct availability of Cecil Road** | Under RAID DEC-3 (12 Jul): tenants stay until **Aug 2027**; London-direct now requires paid London rent ~Sept 2026-Aug 2027 | [[uk-move-financial-model]] §0 + §9 + §10 pot derivation (models living in Cecil from ~Nov 2026, temp accommodation only £0-6k); [[uk-relocation-decision]] header + Next Actions (Merton short-let Sept-Nov premise); [[decision-journal]] (no DEC-3 entry); [[london-monthly-budget]] | Decide DEC-3's status explicitly, then re-model London-direct: either rescind DEC-3 or add a London-rent line (~£2.3-2.6k/mo out, +£1,725 Cecil net let income in) to §0's London column and re-derive its pot and runway | **Material** - changes which option is cheaper and whether "London-direct" as modelled even exists |
| D2 | Malvern runway incl. MPF | ~**5.5-6.1 yr** ((£55k+£124.5k)/£2,700-2,450) | §0 itself says "~8 yr+" (that is the £1,683-burn figure from the superseded 10 Jul block, which says 8.6 yr) | Correct §0 to ~5.5-6 yr | Material - overstates the interim's pension-preserving halo |
| D3 | Malvern liquid runway | §0: **~20-22 mo** (£55k at £2,450-2,700) | Same file §10 landing-pot paragraph: "the Malvern interim funds **~30 months**" (uses £1,683); RAID sheet 0: "~19-21mo (honest £2,600)"; project Next Action A: "~30 months" implication via §10; Drift sheets: 19.2-21.2 mo | Correct §10's "~30 months" to ~20-22 mo; align RAID wording | Material - the interim's core selling point varies by 50% between paragraphs of the SSOT file |
| D4 | Landing pots | London ~£50k, Malvern ~£55k, Stay-HK basis inconsistent | §0 Stay-HK pot "~£82,500" **includes the unbanked £12,475 rebate** (violates the lock-protocol Banked/Hoped rule; the London/Malvern pots correctly exclude it) and **excludes the £9,394 UK current account** that the £91,869 starting figure includes | State one basis: banked-only Stay-HK pot ~£79.4k (70,000+9,394), rebate as upside; or footnote the inconsistency | Material for the Stay-HK runway row (~11-12 mo would shrink to ~10.6-11.9 on banked-only) |
| D5 | London-direct liquid runway | ~9-12 mo depending on tier (50k/5,450=9.2; 50k/4,630=10.8) | §0 headline row says a single "~11 mo" (lean-tier only); 10 Jul block says 9-10 settled / 11-12 lean; project + RAID say "~11-12mo" | State the range 9-12 mo, not the lean-only point | Marginal but flattering-to-London presentation |
| D6 | London settled vs lean build-up | Settled £5,450 = base £4,550 + cleaner 460 + babysitting 215 + car 225; lean £4,630 = base + 80 residual help (workbook Inputs B45/B50) | §0 text says the settled figure adds cleaner+babysitting+car **to the lean tier** (4,630+900=5,530, not 5,450) | Reword §0's build-up sentence | Marginal - numbers right, derivation text wrong |
| D7 | Cecil net rent offset (Stay-HK / Malvern) | Pick one: £1,725 (§9 P&L), £1,730 (§0), £1,736 (workbook Inputs B18 + Test A), tax 199/200/210 variants | §0, §9, [[financial-status-2026-07-07]], [[uk-vs-hk-cost-comparison]], income-floor workbook all differ by £5-11 | Standardise on the §9 P&L build (or workbook 1,736) everywhere | Immaterial (rounding) but the SSOT should not carry three values |
| D8 | Honest Malvern search burn | §0/§9b: **£2,450-2,700**; registers use £2,600 point | [[london-vs-malvern]] table: "~£905/mo"; §9a: £1,683 presented pre-§9b; old 10 Jul block: £1,683; project 11 Jul log rows: £1,683 (historical) | Banner-supersede london-vs-malvern; §9a already cross-referenced to §9b, fine | Material only where presented as current (london-vs-malvern is status: live) |
| D9 | London burn variants in circulation | §0: £4,630 lean / £5,450 settled | £4,550: london-monthly-budget headline, feasibility report floor calc, income-floor workbook B19, both register Drift sheets, earning comparison; £4,427 and £4,610: historical; £4,400: why-london; £3,339: london-vs-malvern; £3,283: living-costs-only line (correct as a component) | Supersede-banners on london-monthly-budget, why-london, london-vs-malvern; recompute register Drift sheets at 4,630 (or note basis) | Material in aggregate - five different "London burn" figures are presented as current somewhere |
| D10 | Runway headline | §0: ~11 mo liquid London (pre-DEC-3 basis) | [[why-london]]: "~4 years", "£216k spendable"; [[london-monthly-budget]]: "~20 months / ~48 months, funded ~4 years"; [[uk-150k-feasibility-report]]: "funded for about 4 years... covered 2-4x"; [[uk-vs-hk-earning-comparison]]: "about 20 months... 47 months (~3.9 years)"; [[london-vs-malvern]]: "~5 years" | Supersede-banners pointing at §0 on all four; re-baseline why-london per lock protocol | **Material** - these are the docs Julian re-reads under stress |
| D11 | Cash-flow break-even floor | Needs recompute: at £4,630 ≈ £78-79k; at £5,450 ≈ £90-95k gross; at DEC-3 London-rent burn higher still | "~£76-77k" (feasibility report, computed at £4,550), "£77.5k" (income-floor workbook B11), "~£77-78k" (project log 9 Jul), "~£77k" (project synthesis, RAID, risk register mitigations) | Recompute the floor at the §0 burns and propagate one figure | Material - the floor-job mitigation carries the London-direct synthesis |
| D12 | MPF value | £124,470 confirmed (financial-status; §10) | [[financial-status-2026-07-07]] assets table ALSO carries a stale "~HK$1,000,000 / ~£100,000 estimated (to confirm)" row plus "MPF (~£100k)" in the floor section and open-item 3 "est. ~£100k"; model §2 "~1M HKD unlocks"; §9 "~£100k MPF unlock"; £124,500 vs £124,470 rounding | Delete/supersede the stale £100k rows inside financial-status (it contradicts itself in one table); leave historical model sections flagged | Marginal (direction understates the buffer) |
| D13 | Reachable London pool for the crash-padder | Two different measures both in circulation: ~2/3 of London (hybrid+remote reachable in principle) and ~25% (genuinely compatible after stripping fixed-day/client-site) | Project header uses 25%; project Waiting-on and hinges use ~2/3; xlsx Two-Pool caveat uses ~2/3; report banner says use 25% as planning figure | State both with their definitions wherever either is quoted ("reaches ~2/3 in principle; plan on ~25% genuinely compatible") | Marginal - but the 2.7x gap between the two figures changes the search-length story |
| D14 | Interim exit date | DEC-3: **Aug 2027** (notice timed for an Aug 2027 move; Sophia starts London school Sept 2027) | Fable reviews + project C4 + Next Actions: "Cecil let ending **Jun-Jul 2027**"; model §9b: "Jul-Aug 2027 window"; user.md memory: "school year boundary Aug 2027" | Reconcile: the reviews' Jun-Jul buffer requirement vs DEC-3's Aug date (an Aug hand-back leaves ~2-4 weeks before school start - tight; name it and accept or adjust) | Marginal-to-Material (execution risk, not option choice) |
| D15 | "£150k+ band % contract" | 85% (68/80), corrected 11 Jul | Project status log 11 Jul "THE HINGE ANSWERED" row still says 87% (one of the two log locations Fable's §7 named); log rows also still say 375 vs the report's 376 | Fix the remaining log row (or annotate it as historical) | Immaterial (historical rows) but Fable's §7 fix list is only part-executed |
| D16 | Indicative register totals | Risk register xlsx: London 49 / Malvern 92 / Stay 76; RAID (post-Cecil): London 49 / **Malvern 73** / Stay 76 | Project status log 12 Jul quotes 49/92/76 without noting the RAID re-score to 73 | When the header is rewritten, quote the current (post-Cecil) totals or drop totals entirely | Marginal - totals are explicitly indicative |
| D17 | Sophia-midweek downgrade justification | Julian's call to make (Impact 2 vs Fable's 4-5) | Register [JH] row cites "was to be 50/50 with her mother anyway" - no wiki source supports this; [[sophia]], [[clodagh]] and financial-status record sole responsibility, non-contribution, and Clodagh leaving for Ireland | Keep the downgrade if Julian owns it, but strike or evidence the 50/50 claim; per the risk framework, evidence columns must separate assumption from fact | Material for the interim's biggest human risk |
| D18 | HK burn "gap" wording | §1: actuals 92,196 mean / 83,940 trend vs category total 74,800 (gap ~9-17k) | Consistent across files; only note: budget.md housing figures flagged stale by financial-status (HK$29,279 vs authoritative 25,827) - flag still open | Leave; budget.md correction outstanding | Immaterial |

---

## 3. §0 canonical summary - line-by-line validation

Method: each §0 claim recomputed from its cited source (§1, §8, §9, §9b, §10, §11) and the income-floor workbook (formulas re-derived by hand because the workbook holds no cached values - see §4.3).

| §0 line | Recomputation | Verdict |
|---|---|---|
| Stay-HK burn ~£6,700-7,500 = HK outgoings £8,400-9,200 less Cecil net rent £1,730 | §1: 83,940 HKD ≈ £8,394; 92,196 ≈ £9,220. 8,400-1,730 = 6,670; 9,200-1,730 = 7,470 | **PASS** (arithmetic; note D7 on the 1,725/1,730/1,736 offset variants) |
| London-direct £4,630 lean / £5,450 settled | Workbook Inputs: B50 = 4,550+0+30+50 = **4,630**; B45 = 4,550+460+215+225 = **5,450** | **PASS on values; FAIL on §0's derivation text** (settled = lean + £820, not lean + cleaner/babysitting/car; see D6). **FAIL on world-model under DEC-3** (assumes living in Cecil; see D1) |
| Malvern £2,450-2,700 = 1,683 + board 500 + car 225 + schooling 50 | 1,683+500+225+50 = 2,458; top of range 2,700 is §9b's stated upper bound | **PASS** (range top is asserted, not built - acceptable as a hostile margin) |
| Stay-HK pot ~£82,500 | 70,000 + 12,475 = 82,475. Includes unbanked rebate; excludes the £9,394 UK account that £91,869 includes | **FAIL on basis consistency** (D4; Banked/Hoped rule) |
| London pot ~£50,000 / Malvern ~£55,000 | §10 bridge: 91,869 - 12,475 - ~6,500 - ~15,000 - (0-6,000) = ~£51.9-57.9k; stated ~£50-57k, Malvern at top | **PASS arithmetically**; but the £0-6k temp-accommodation line and hence the London pot are **invalid under DEC-3** (D1); moving one-offs still estimates (open item) |
| Stay-HK liquid runway ~11-12 mo | 82,500/7,500 = 11.0; 82,500/6,700 = 12.3 | PASS on its own pot basis (D4 caveat) |
| London liquid runway ~11 mo | 50,000/4,630 = 10.8; but 50,000/5,450 = 9.2 | **PARTIAL** - lean-only point estimate; honest range 9-12 (D5) |
| London runway incl. MPF ~2.7-3.2 yr | 174,500/5,450 = 32 mo; /4,630 = 37.7 mo | **PASS** |
| Malvern liquid runway ~20-22 mo | 55,000/2,700 = 20.4; /2,450 = 22.4 | **PASS**, but contradicted by §10's "~30 months" in the same file (D3) |
| Malvern runway incl. MPF ~8 yr+ | 179,500/2,700 = 66 mo = 5.5 yr; /2,450 = 73 mo = 6.1 yr | **FAIL** - "~8 yr+" is the superseded £1,683-burn figure (D2) |
| MPF +£124,500 on departure | Confirmed 1,244,699 HKD ≈ £124,470 | PASS (rounding) |
| "Why London costs more" £59/mo housing gap | Test A/workbook: HK-stay 1,172 vs London 1,231 | PASS (source-consistent) |
| "Is London > HK" reconciliation table | Row 1: 4,630-5,450 vs 6,700-7,500, HK higher - PASS. Row 2: HK residual 4,900 = 8,400-2,900-650 = 4,850 ≈ 4,900 - PASS. Row 3 London vs Malvern - PASS | **PASS** - this block is §0's best contribution; keep it |
| Crash-pad £1,083/mo as cost-of-earning | 100×4.33 + 150×4.33 ≈ 433+650 | PASS (inputs still unverified - open item) |
| Sources line "Last reconciled 2026-07-13" | §0 nowhere mentions DEC-3 (12 Jul Cecil decision), which invalidates its London-direct column and pot line | **FAIL on completeness** - reconciled against the 11 Jul world, not the 12 Jul one |
| Same file, Key Takeaways (bottom) | Still: "London's cost is forgone rent (~£2,600/mo net drawdown)... Decision gates on whether HK liquid savings cover a ~12-18 month London search (£31-47k) - see §9" | **FAIL** - the canonical file's own takeaways contradict its canonical table; §2's "~1M HKD MPF" and §9's "~£100k MPF unlock" also stale in place |

**Overall §0 verdict: structurally right, four substantive defects (D1 DEC-3 blindness, D2 8-yr error, D3 internal 20-22 vs 30 contradiction, D4 pot basis), plus wording and staleness defects. Do not treat it as authoritative until the morning fixes land. Its supremacy clause makes the D2/D3 errors actively dangerous: as written, the rule says other files must be "corrected" toward a wrong number.**

---

## 4. Risk register + RAID register audit

### 4.1 Risk register xlsx (uk-move-decision-risk-register-2026-07-12.xlsx)

- **FORMULAS: NONE. Prominently flagged as requested.** Every Score cell (E/H/K) and the TOTAL row (E19/F19/I19) is a hardcoded literal. The sheet's own how-to text (A21) says "the Score and colour recompute on I x P (recalc in Excel)". They will not recompute; if Julian edits an I/P cell in Excel or Google Sheets, the Score silently stays wrong. Either add real formulas (=C6*D6 etc.) to the live Google Sheet or delete the claim.
- **Arithmetic (as frozen): all correct.** Every Score equals I x P, and the three totals (49 / 92 / 76) sum correctly. The RAID copy stores every number as TEXT ('4' not 4), which will break SUM() the moment formulas are added - convert to numeric.
- **Header self-dating:** sheet note says "11 Jul 2026"; filename says 2026-07-12. Cosmetic.
- **RAG thresholds** (Green <=6, Amber 7-12, Red >=15) leave 13-14 undefined; harmless (no I x P product yields 13-14), but tidy it.
- **Framework conformance vs AGENTS.md Risk Framework: the .xlsx snapshot does NOT conform.** Missing: cause -> event -> effect chain (rows are single "Risk" phrases), the one-effect-two-mitigation-rows structure (Reduce Impact / Reduce Probability), residual columns (IMPR / ProbR / RiskR), financial exposure columns (Residual Impact HK$ / Prob % / Exposure), a RAG column (only colour thresholds), a **Decision Impact column (Material / Marginal / Immaterial - the framework's "most important column")**, and a Supporting Evidence / Due Diligence column. Mitigating context: the framework was formalised 13 Jul, AFTER this snapshot, and the File Map claims the live Google Sheet v2 is "structured with cause-event-effect-mitigation per risk-framework". **I cannot verify the Google Sheet from this run.** Morning action: confirm the live sheet actually has the framework columns; if not, the claim in the File Map is aspirational and should be softened.
- **Content gaps vs the rest of the record** (some may exist in the live v2 - verify): no French-gap row (13 Jul log says it was added to the Google Sheet only); no school-place risk (the pre-registered reopen condition); no MPF tax-timing / eMPF-blackout risk (the model calls it "the most time-sensitive financial action"); no sole-parent SPOF (will / guardian / life cover, the unknowns review's #3); no Joanne-under-move rows (only Stay-HK); no DB-flat consent-to-let or rent-shortfall row; no Sophia-suppression monitoring row distinct from midweek absence.
- **Drift & Run-rate sheet uses superseded burns:** London £4,550 (should be £4,630 lean per §0) and the months columns are computed at 4,550 (50k -> 11.0). Malvern £2,600 is a fair §9b midpoint. Recompute or annotate.
- **Judgment-row evidence defect:** the [JH] Sophia-midweek row justifies Impact 2 partly on "was to be 50/50 with her mother anyway" - unsupported by, and in tension with, [[sophia]] / [[clodagh]] / financial-status (sole responsibility, non-contribution, Ireland). The downgrade itself is Julian's to make; the cited evidence is not in the record (D17).

### 4.2 Risk register xlsx (uk-move-risk-register-2026-07-12.xlsx)

- **The most current statement of the decision anywhere in the vault**, and the only surface that has metabolised DEC-3. Its "Current position" ("a genuine trade... now Julian's judgment call") CONTRADICTS the project Status header ("interim DEMOTED; London-direct safer default"). One of them must give way; per Project Status Updates rules the header should have been rewritten on 12 Jul and was not.
- Decisions sheet is good practice (DEC-1..6, statuses, reopen conditions). But **DEC-3 (Cecil / Aug 2027) and the risk-judgment reframe exist ONLY here and in the project status log** - the decision journal has no entry for either, despite DEC-3 partially reversing the 7 Jul "notice SERVED" behavioural down-payment that anchored London-direct. Under the commitment-lock protocol, reversing a down-payment without a journal pass is exactly the silent-slide the protocol exists to catch. Write the journal entries.
- Risks sheet totals (49 / 73 / 76) are internally correct; Malvern's drop from 92 to 73 reflects the Cecil de-risk (tenancy 12->3, drift 12->4, extra-transition 10->8). Reasonable, but note the de-risk rests on TWO unconfirmed dependencies the register itself lists as open (DEP-3 tenants accept Aug 2027 notice; DEP-5 Mum's consent). The scores have banked mitigations that are not yet real - the same optimism-accounting pattern (lock-protocol bias #6) previously flagged in the other direction.
- All values stored as text; Drift sheet again at £4,550; sheet 0 "Key numbers" says Malvern runway ~19-21mo vs §0's 20-22 (D3 family).
- Assumptions sheet is genuinely good (A1-A11 with confidence + impact-if-wrong); A5/A6/A8/A9 correctly mark the load-bearing items unvalidated. It is the closest thing to the framework's Supporting Evidence discipline anywhere in the register set.

### 4.3 Income-floor workbook (uk-vs-hk-income-floor-reconciliation-2026-07-09.xlsx)

- **All 92 formula cells have no cached values** (created programmatically, never recalculated). Any reader or agent opening the file without a recalc engine sees blank results for every computed cell, including the load-bearing B45 (£5,450) and B50 (£4,630). This is presumably the "empty/broken formulas" a prior session hit. The companion doc's numbers check out when the formulas are re-derived by hand, but the workbook cannot self-evidence them. Fix: open once in Excel/Google Sheets and re-save, or bake values alongside formulas.
- Input staleness: B19 "London monthly cash burn 4550" is labelled "Latest London cash burn" - accurate when written, now the superseded base tier; fine internally (B45/B50 build on it) but the label invites misuse.
- The workbook remains the actual source of §0's London burns even though §0 cites the companion doc, which never states £4,630/£5,450. Add the two figures to the companion doc so the citation chain closes.

---

## 5. Per-cluster findings

### 5.1 Finance
- [[uk-move-financial-model]]: §0 defects in §3 above. Also historical-section staleness inside the SSOT file itself: §2 "MPF ~1M HKD", §9 "~£100k MPF unlock", §9 "runway test (open - gated on HK savings)" (resolved), the 10 Jul update block's Malvern £1,683 rows, and the Key Takeaways block. Since §0 declares supremacy, mark these blocks "historical - superseded by §0" or readers will keep tripping (the file is explicitly the one place they are told to trust).
- [[london-monthly-budget]]: headline £4,550, "~20 months / ~4 years", and the §4 comparison (HK stay £6,206 using the un-taxed £2,194 offset vs §0's £1,730 basis) all superseded; only §1's line items remain useful. Needs a §0-pointing banner (the 10 Jul banner only corrects the Test A headline, not the runway).
- [[why-london]]: fails the lock-protocol's own "honest post-review numbers only" requirement (~£216k / ~4 years / £4,400). This is the highest-priority re-baseline because its whole function is to be read during a wobble.
- [[uk-vs-hk-cost-comparison]] (Test A): internally consistent, well-maintained banners. Minor: uses 1,736 offset (D7).
- Income-floor reconciliation + Claude/Codex reviews: coherent set; "£77.5k floor" needs the D11 recompute; workbook issue in §4.3.
- [[financial-status-2026-07-07]]: contradicts itself on MPF within one table (D12); "non-ISA liquid + MPF, ~£192k" uses the stale £100k; Cecil availability paragraph ("served now... vacant ~November") superseded by DEC-3; open-item 3 (MPF balance) actually resolved. Needs a refresh or a dated supersede note; it is listed in the File Map as a live source-of-truth.
- [[budget]] housing figures remain flagged-stale (financial-status note); harmless while quarantined but still uncorrected.

### 5.2 Job market / career
- [[uk-job-market-remote-hybrid-split-2026-07-11]] + xlsx: in good shape post-corrections (85% fixed in doc and workbook; crash-pad banners present; caveats honest). Residual: the ~2/3 vs ~25% dual figure (D13) is used interchangeably by downstream surfaces.
- [[uk-150k-feasibility-report]]: "funded for about 4 years... covered 2-4x" (D10) and the £76-77k floor at £4,550 (D11) are stale inside an authority: Fable-reviewed doc; the 11 Jul update block is good.
- [[uk-vs-hk-earning-comparison]]: "20 months / 47 months" runway (D10). Otherwise consistent.
- [[cleared-defence-cyber-lane-assessment]]: the 11 Jul tiering correction is properly folded. Consistent.
- [[career/_index]]: rows 19-20 still carry the superseded verdicts ("Leans London-direct"; "leans London/West-Corridor, not Malvern") - index descriptions embedding verdicts is exactly the staleness the index doctrine bans. Trim to what each doc IS.
- The accessible-tier arithmetic Fable's §5 flagged (sponsored-SC perm from a Malvern base) remains un-run; with DEC-3 anchoring the interim to Aug 2027 it is now more relevant, not less.

### 5.3 Decision record
- [[decision-journal]]: stops functionally at 10-11 Jul. Missing: (a) a formal disposition of the contested reopen (Fable §8.1 - still open); (b) the 12 Jul risk-register judgment session ([JH] downgrades, reframe of the red-team as risk-surfacing); (c) DEC-3 Cecil, which both reverses a recorded down-payment and re-times the whole plan; (d) any note that the "notice SERVED 7 Jul" anchor was superseded. The journal is billed as the canonical record and is currently two material decisions behind the RAID register.
- [[commitment-lock-protocol]]: sound; but its Banked/Hoped rule is violated by §0's Stay-HK pot (D4) and its anchor-doc rule by why-london (D10). The retype-the-choice lock item is now noted open in five places (journal, project E, DEC-5, ISS-8, Fable §8.2) - it has been open since 7 Jul and "failed twice"; either do it or formally accept the decision is a lean, not a lock.
- [[london-vs-malvern]] is marked status: live but is a 7 Jul time capsule (£3,339/£905/5yr, "money is not the constraint"). Re-status to historical or banner it.
- [[uk-move/_index]]: missing entries for [[fable-review-unknowns]], [[fable-review-jobdata-2026-07-11]], and both .xlsx registers. As the workspace index this is a completeness defect.
- BRAINED stage docs (capture, analysis, alternatives, benefits, risks, need-time, reconciliation, b1, b7): fine as period records; no correction needed beyond their historical status being visible.
- The five prior Fable reviews are mutually consistent in narrative arc; the only fossil found: project status log 11 Jul row retains "87%" and "375" (D15) - acceptable if log rows are treated as immutable history, but Fable's §7 named that row for fixing, so the correction list is part-executed.

### 5.4 Project surface ([[uk-relocation-decision]])
- **Status header is two days and two decisions stale** (frontmatter status-updated: 2026-07-11; header "as of 2026-07-11"), despite 12 and 13 Jul log rows underneath recording the Cecil decision and the register work. This violates the Project Status Updates rule (header must be rewritten in the same operation) and produces the header/RAID contradiction in §4.2. The header's "interim DEMOTED... five-condition conjunction, conditions 1-3 look difficult" is no longer the standing position: per the 12 Jul rows, condition 3 (tenancy) is largely resolved by DEC-3, condition 4 (dated move-by) is delivered by the Aug 2027 anchor, and Julian has recorded his own judgment on 1-2. The header should present the RAID "genuine trade / judgment call" state, the DEC-3 consequence for London-direct (D1), and what remains open.
- Next Actions similarly stale: C3 (tenancy verification) and C4 (Jun-Jul 2027 let) predate DEC-3; execution items 2-3 (Merton short-let Sept-Nov, Sept 2026 school call) are incompatible with DEC-3 unless DEC-3 is rescinded - they need an explicit "only if DEC-3 reversed" tag or removal; the "this week" Stephan/TTI item references a Tuesday that has passed (TTI gate expires 17 Jul - three days away).
- File Map: good, but says the .xlsx register "is now a static snapshot" while the register row above it still claims editable-recompute behaviour (§4.1); the decision-criteria-matrix is consistently PLANNED everywhere (good).

### 5.5 Stakeholder / wellbeing
- [[sophia]] (7 Jul) is rich and internally consistent; nothing contradicts it except the register's 50/50 claim (D17). It predates the crash-pad plan; a short addendum on the midweek-absence design conditions (max 2 fixed nights etc.) would make it the enforcement surface Fable's red-team asked for.
- [[hanley-castle-high-school]] + [[sophia-malvern-activities]] (13 Jul): consistent, properly scoped as mitigation evidence for the interim; correctly cross-linked. Note both implicitly assume the interim; neither is wrong to.
- [[clodagh]] / [[joanne]]: consistent with the decision record. The Joanne "define the decision with a date" item remains open (execution item 5) with the month-9 reopen risk the unknowns review flagged.

---

## 6. Confirmation-amplification audit (both directions)

The documented failure mode: the record writes its strongest sentences in whichever direction Julian currently leans (7 Jul pro-London, 10 Jul pro-Malvern, 11 Jul pro-London, 12-13 Jul pro-interim).

**Leaning interim (current lean - found):**
1. RAID "Current position" argues the red-team demotion over-stated ("more viable than the red-team's demotion implied") while its own dependencies (DEP-3 tenant acceptance, DEP-5 Mum consent) are open - mitigations banked before they exist (bias #6).
2. "Kills the drift trap" (12 Jul log, RAID) is strong language for an anchor that currently rests on an unconfirmed tenant response and an undelivered notice.
3. The [JH] Sophia downgrade cites an unsupported counterfactual (D17).
4. "The Malvern crash-pad interim is the natural bridge" converts a cost consequence of DEC-3 into an argument for the interim without re-pricing London-direct-with-rent as the comparator (nobody has actually costed the alternative it displaces).
5. RAID Malvern total falling 92 -> 73 while London's stayed 49: the re-scores are individually defensible but all moved one way, in the week the lean moved that way. Same pattern flagged on 10 Jul (5 of 6) and 11 Jul (8 vs 4).

**Leaning London-direct (found):**
6. §0's London-direct column still shows the rent-free live-in-Cecil world and the ~11 mo lean-tier runway headline (D1, D5) - as written, the SSOT flatters London-direct against the DEC-3 reality.
7. The project header (most-read surface) still leads with the 11 Jul demotion verdict, giving a morning reader a stronger pro-London impression than the current record supports.
8. The floor-job mitigation (~£77k, "abundant roles") that carries the London synthesis is computed on the superseded burn (D11) - it understates London's landing bar.

**Net:** neither direction is clean. The record is not currently lying in one direction; it is split-brained, with narrative surfaces leaning interim and the canonical money surface leaning London by omission. That is arguably more dangerous than a single bias because each side can cite a file.

---

## 7. Completeness gaps and still-open items (deduplicated across all reviews and registers)

**Genuinely open (verified still unresolved tonight):**
1. **DEC-3 integration** (new, this review): re-model London-direct under kept-tenants; re-derive §0 London column, pot, runway; restate header/journal (D1).
2. **Retype the committed choice** (lock condition 1) - open since 7 Jul; named in 5 surfaces.
3. **TTI gate** - hard deadline 17 Jul; written terms + conversion intent or move executes. Three days out; the "Tuesday Stephan message" next-action text has aged out.
4. **Bank the £12,475 rebate** before departure (pot to ~£62-69k).
5. **Firm shipping quote** (pot swing ±£5k).
6. **Mum's consent + capacity recorded**; paid-carer contingency priced into the burn (the register assumes the contingency but no cost line exists in any burn table).
7. **Tenants accept the Aug 2027 notice** (DEP-3) - the whole de-risk rests on it.
8. **Malvern in-year school place** for Sophia (ISS-5) - no evidence of a call yet; hanley-castle doc says "to confirm current provision".
9. **Crash-pad inputs** - real train fare (season vs flexible) + midweek room quote; §9b says likely above estimate.
10. **Hybrid-role fixed-night tolerance** - test live JDs against the 2-3-night constraint (ISS-7; the interim's internal contradiction).
11. **Tax adviser + MPF timing / eMPF blackout** - flagged time-critical since 7 Jul, still unbooked per every surface.
12. **DB flat consent-to-let (HSBC)** + signed tenancy confirming HK$22k rent and the one-off fee.
13. **Will / guardian / life cover** (unknowns review #3; execution item 6 "Ask Jamie") - no evidence of progress.
14. **Joanne decision with a date** - open; month-9 reopen risk.
15. **Fidelity ISA composition** (possible ~£800-1k/mo natural yield without breaching the ring-fence) - open since 7 Jul.
16. **Recompute the cash-flow floor at §0 burns** (new, this review; D11).
17. **Formal journal disposition of the contested reopen** (Fable 11 Jul §8.1) - still absent.
18. **Time-to-fill pull** (optional; converts the pool-size proxy into the named hinge metric).
19. **Trend-vs-mean HK denominator** (HK$8.3k/mo swing) via recurring-vs-one-off split - open, affects Stay-HK burn and all HK-baseline comparisons.
20. **Accessible-tier cleared-perm arithmetic** (Fable 11 Jul §5) - never run; more relevant post-DEC-3.

**Quietly resolved (no longer open - stop listing):** pot derivation (done 11 Jul); symmetric Malvern costing (done §9b); "HK has no cheap floor" deletion (done); MPF exact balance (confirmed £124,470 - financial-status just needs its stale rows removed); MPF-vs-PR question (resolved 10 Jul, caveats logged); tenancy vacant-possession *legal* verification in its original form (recast by DEC-3 into item 7 above plus a lighter solicitor check of notice mechanics); 87%->85% and 375->376 in the living docs (residual fossils in log rows only).

---

## 8. Consolidation readiness (the four planned hubs)

| Hub | Exists? | Should feed it | Archive / supersede once folded |
|---|---|---|---|
| **financial-model** ([[uk-move-financial-model]] §0) | Yes (13 Jul) but §3 defects | Income-floor workbook + companion (as Tier-3 refs); Test A; financial-status (refreshed); london-monthly-budget §1 line items; DEC-3 re-model | [[london-monthly-budget]] (headline+runway sections), [[financial-status-2026-06-22]] (already superseded), the model's own §2/§9/§10-block stale fragments (mark historical), pre-review sections of Test A (already banner-quarantined) |
| **job-market-analysis** | **No - does not exist yet** (AGENTS.md names it; nothing at that name) | [[uk-job-market-remote-hybrid-split-2026-07-11]] (+xlsx) as spine; [[uk-150k-feasibility-report]] (floor/target); [[cleared-defence-cyber-lane-assessment]]; [[uk-vs-hk-earning-comparison]]; [[target-role-profile]] + [[adzuna-uk-job-market-data-source]] as Tier-3 | The two jh-clarifications docs, the codex review, [[uk-ir35-contracting-feasibility-2026]] (fold key IR35 verdict into the hub), career/_index verdict-rows trimmed |
| **decision-register** (journal + criteria matrix merged) | Partial (journal live; matrix PLANNED) | Journal (after the two missing entries land); decision-criteria-matrix build (after risks complete); why-london re-baselined as the anchor; the five Fable reviews as Tier-3 review record | BRAINED stage docs -> historical/archive status; [[london-vs-malvern]] archived; workspace _index updated to list everything (currently missing 2 reviews + 2 xlsx) |
| **raid-register** | Yes (Google Sheet live; xlsx snapshots) | RAID xlsx structure is the right skeleton; add the framework columns (cause/event/effect, residual, Decision Impact, evidence); add the missing risk rows (§4.1 content gaps); real formulas | The 12 Jul risk-register xlsx (label clearly as superseded snapshot in the File Map - half-done), risks.md kept as BRAINED history only |

---

## 9. Prioritised morning action list

1. **Resolve DEC-3's status and cascade it** (D1): confirm keep-tenants/Aug-2027 stands; then (a) re-model London-direct with a rent line and re-derive §0's London column + pot + runway, (b) rewrite the project Status header to the RAID position with today's date, (c) write the DEC-3 journal entry (it reverses the 7 Jul down-payment - run it through the lock protocol properly), (d) tag Next-Action items 2-3 and C3-C4 as superseded-or-conditional.
2. **Fix §0's four numeric/basis defects**: Malvern-incl-MPF ~5.5-6 yr (D2); §10 "~30 months" -> 20-22 (D3); Stay-HK pot basis (D4); London runway stated as 9-12 range (D5); plus the D6 wording and the stale Key Takeaways in the same file.
3. **Write the missing journal entries**: reopen disposition (17), 12 Jul register judgment, DEC-3.
4. **Re-baseline the three reassurance docs** ([[why-london]] first - lock-protocol requirement; then london-monthly-budget and london-vs-malvern banners).
5. **Recompute the floor-job figure at §0 burns** (D11) and propagate one number; this directly conditions the London-direct synthesis.
6. **Repair the register mechanics**: real formulas in the live Google Sheet (verify its framework columns while in there); numeric not text cells; Drift sheets to §0 burns; strike or evidence the 50/50 claim (D17).
7. **Chase the three cheap swing items before departure**: rebate banking, shipping quote, tenant acceptance of the Aug 2027 notice.
8. **TTI gate discipline**: 17 Jul is Friday-minus; the pre-committed rule is written - execute it as written, whatever the answer.
9. Housekeeping batch: workspace _index additions; career/_index verdict-row trim; financial-status MPF row cleanup; income-floor workbook recalc-and-resave; remaining 87%/375 fossils annotated.

## 10. Open questions only Julian can answer

1. **Does DEC-3 stand?** Keep the tenants to Aug 2027 (interim becomes near-forced, London-direct means ~a year of paid rent), or revert to vacating ~Nov 2026 (restores the modelled London-direct)? The whole record currently straddles this.
2. **Do you own the Sophia-midweek Impact-2 judgment without the 50/50 justification?** If yes, say so in your own words in the register; if the 50/50 expectation is real, evidence it (it appears nowhere in the record and the record leans against it).
3. **Mum's consent**: has the conversation actually happened? Every surface still says unrecorded.
4. **The retype lock item**: will you write the committed choice in your own words this week, or accept on the record that the position is a lean and stop calling it committed?
5. **Aug 2027 vs Sept 2027 mechanics**: an Aug hand-back leaves weeks, not months, before a Sept school start (refurb, furniture, address proof for admissions). Is that buffer acceptable, or should the notice target Jun-Jul 2027 as the 10 Jul review specified?
6. **What is the TTI answer**, and does it clear the pre-committed written-artifact bar by 17 Jul?

## Related
- [[uk-relocation-decision]] - project surface this review audits
- [[uk-move-financial-model]] - §0 canonical summary (validation in §3 above)
- [[fable-review-jobdata-2026-07-11]] - prior review; its §7 correction list is part-executed (see D15)
- [[commitment-lock-protocol]] - the rules §0 and why-london currently breach (D4, D10)
