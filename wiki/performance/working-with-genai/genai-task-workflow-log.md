---
type: log
created: 2026-09-03
updated: 2026-09-04
status: active
tags: [working-with-genai, routing, log]
---

## Purpose

A record of routed GenAI work, its checks, outcomes and mechanical lessons.

# GenAI Task Workflow Log

This is the journal of work run through the [[genai-task-workflow]] chain: one
entry per run, with what happened and the lesson. It covers failure at any step -
admission oversized or fragmented, work type misclassified, verification
misjudged, routing wrong, steering wrong -
so it is the single repository checked when scoping new work ("I tried something
like this before and here is why it went wrong"), and lessons compound into the
models instead of scattering. It is read at task creation when routing is being decided, and
written in the same operation as the deliverable's Time and Token Log row whenever a run
was routed. Vocabulary: work types from [[mm-work-types]], check forms from
[[mm-verification]] - this file records instances and defines nothing.

**Entry format:** the heading is the scannable digest - `date · work type ·
outcome · deliverable` - and the bullets carry the detail, one or two lines
each. Outcome values: **Worked / Partly / Failed**. The Lesson line names which
chain step went wrong (admission / work type / verification / routing /
steering) so the log is queryable by step as well as by type. Newest first.

---

## 2026-10-02 · Review prompt · Worked · [[TTI-board-risk-Astra]]

- **Work:** Prepared the requested standalone Claude review prompt, saved within the existing deliverable.
- **Check:** Matched the user's original scenario, job decision and formal-narrative instruction; excluded prior model conclusions.
- **Outcome:** As of 2 October: prompt delivered; no Claude run. Incremental tokens unmeasured separately.
- **Lesson:** Verification: preserve independent judgement by handing over the brief and original evidence rather than the first review's conclusions.
- **Deliverable:** [[TTI-board-risk-Astra#Claude review prompt]].

## 2026-10-02 · Critique amendment · Worked · [[TTI-board-risk-Astra]]

- **Work:** Applied Julian's instruction to treat the rejection rationale as an untrusted formal narrative.
- **Check:** Re-read the review; distinguished rejection, stated explanations and inferred motives; removed reassurance inferred from earlier supportive comments. Checked the project summary for the same issue.
- **Outcome:** As of 2 October: review and project updated. Territorial resistance remains plausible; a board coalition remains unestablished. Incremental tokens unmeasured; cumulative thread checkpoint 221,484 includes the prior run.
- **Lesson:** Verification: formal correspondence establishes what was communicated; treating its rationale or diplomatic encouragement as genuine motivation can create false reassurance.
- **Deliverable:** [[TTI-board-risk-Astra]].

## 2026-10-02 · Research + Critique · Worked · [[TTI-board-risk-Astra]]

- **Work:** One independent review of TTI board/succession risk and Julian's exposure in a Horst-mandated role.
- **Check:** Astra traced public claims to TTI/HKEX documents and read the verbatim rejection plus earlier supporting calls; checked counterevidence and distinguished reported interests from votes. Single-review scope requested by Julian; no separate reviewer.
- **Outcome:** As of 2 October: review delivered; operating support and employment protections remain unagreed. Hostile takeover is not the base case; employment exposure does not require one. Julian's assessment pending. Thread usage 204,555 tokens at checkpoint, including earlier model-selection work; review-only usage unmeasured.
- **Lesson:** Verification: check the original correspondence before adopting political explanations; supportive earlier calls can materially qualify a later rejection. A faction label is not evidence of a voting coalition.
- **Deliverable:** [[TTI-board-risk-Astra]].

## 2026-10-02 · Build + Verification · Worked · [[nbj-youtube-notebooks]] Aug & Sep 2026

- **Work:** `/youtube-notebook` loaded 36 Nate B Jones long-form videos (1 Aug - 30 Sep 2026) into a new NotebookLM notebook with one native briefing each.
- **Check:** Mechanical: dual-path enumeration PASS (0 gaps) and four-way reconciliation PASS (36/36). Briefing content deliberately not reviewed, by Julian's call.
- **Outcome:** Clean single run, no resume needed. 169,143 session tokens.
- **Lesson:** None new; the skill's mechanical verification was sufficient for this work type.
- **Deliverable:** [[nbj-youtube-notebooks]].

## 2026-09-30 · Testing a model-drafted intuition summary against the raw captures · Worked · [[uk-relocation-project]]

- **Work:** the model drafted six insights from the counterfactual runs for
  [[HK-Return-BRAIND]]; a Sonnet subagent extracted themes blind from the raw
  captures in [[HK-Return-Intuition]] (18 themes); Codex then tested the six
  insights adversarially against the same captures.
- **Check:** independence by design: the blind pass never saw the draft, and the
  Codex pass was told to hunt for evidence against each insight first. Codex
  quotes spot-checked against the files by the main thread.
- **Outcome:** Worked. Codex rated all six insights "mixed": "stable" and "every"
  overreached, a model-prompted answer had been counted as Julian's, and a
  session was mislabelled clear-headed. The blind pass found five themes the
  draft had left out. Julian then edited the summary point by point.
- **Lesson:** a summary drafted from one source (the runs) reads tidier than the
  raw record supports; a blind extraction plus an against-first adversarial pass
  caught both overreach and omission cheaply (about 185k tokens). Separately,
  naming missing factors straight after a counterfactual answer flipped that
  answer: record the first answer before any model comment.

---

## 2026-09-30 · Filing and adversarial review of Julian's home fee research · Worked · [[uk-relocation-project]]

- **Work:** Julian's own research (60 min with an AI research tool) filed into the
  wiki by a Sonnet subagent with a two-year date correction, then reviewed by an
  Opus subagent against its own fourteen sources; ten findings applied one at a
  time with Julian (60 min).
- **Check:** Opus adversarial review, read-only, findings in
  [[uk-home-fee-status-opus-review-2026-09-30]]; nine of fourteen official sources
  opened and checked, five unopenable and marked as such.
- **Outcome:** Worked. Rules confirmed correct; the review's value was in omissions
  (a provision the research missed, Julian's primary plan absent) and in catching
  the filing agent's overstated takeaways. Julian rated the piece 4/5.
- **Lesson:** Sonnet is enough for filing, Opus was needed for the review; the
  filing agent's summary lines are a content-producing stage and need the review
  to cover them, which it did. Separately: a one-line user reply ("I do not qualify")
  had been logged on 28 Sep as a settled conclusion without a reason; record the
  reason or record it as unexplained.
- **Deliverable:** [[uk-relocation-project]] (home fee status; not a deliverable
  file, logged on the project page).

## 2026-09-29 · Wiki drafting (tool definition + decision run record) · Pending · [[HK-Return-BRAIND]]

- **Work:** Two wiki files drafted by the model in an interactive session under
  the admission fast lane: a tool definition ([[counterfactual-questioning]]) and
  a decision run record ([[HK-Return-Counterfactuals]]).
- **Check:** Independent adversarial review by a subagent before Julian's
  sign-off.
- **Outcome:** As of 29 Sep 2026: the review returned 19 findings, none fatal,
  mostly overreach in the model's readings and a lean towards one option. Fixes
  applied the same day. A second review, of the move of detail into two
  supporting files, returned 9 serious and 10 minor findings, none fatal: the
  moves were lossless, but model-written one-line verdicts overstated or
  presented inference as Julian's view. Fixes applied. Pending Julian's review.
- **Lesson:** None recorded yet.
- **Deliverable:** [[HK-Return-BRAIND]].

## 2026-09-28 · Card review + reasoning · Worked, at a cost · [[bias-history-review]]

- **Work:** Julian read four register-derived bias cards with Claude; Claude
  reworded two in his words, checked the evidence behind a third, retired it,
  and built a new bias card for the pattern Julian identified instead.
- **Check:** Julian's own judgement on each card (Taste work); grep for stale
  copies of every changed one-liner; mirror diff on the skill.
- **Outcome:** Worked. Julian 15 attended minutes, rated 3/5. About 140k
  tokens (output + cache write). Two cards clearer, one retired, one created,
  skill trigger widened.
- **Lesson:** Step at fault: reasoning, Claude's. Twice Claude mapped an
  instance (TTI) to the nearest existing card without asking what caused it,
  and Julian had to separate cause (wishful thinking) from effect (eggs in one
  basket). When assigning an instance to a bias, ask "what drove this?" before
  "which card is closest?". Reuse-before-build worked: the reopen test and the
  eggs card were found, not rebuilt.

## 2026-09-27 · Refactor · Worked, at a cost · [[savings-v3-review]] companion restructure

- **Work:** Claude reviewed the restored expense structure, then refactored two
  existing wiki notes: moved the model inputs, assumptions and mirrored tables into
  the savings comparison, renamed the cashflows note to uk-relocation-expenses and
  slimmed it, repointed ten links, indexes and the project surface.
- **Check:** Claude re-derived every figure by value; Julian read the outcome.
- **Outcome:** Worked. Content right first time, 30 attended minutes. Cost: about
  1.1M effort tokens on the main Fable thread for what was mostly mechanical
  execution.
- **Lesson:** Step at fault: routing. The review needed the main thread; the
  refactor did not, and it ran inline anyway. Brief a subagent on a cheaper model
  for execution and keep the main thread for the brief and the check
  ([[mm-token-economics]] "delegate the grinding"). Memory:
  feedback-delegate-execution-to-subagents.
- **Deliverable:** [[savings-v3-review]].

## 2026-09-27 · Build + Verification · Worked · [[savings-v3-review]] visible rules

- **Work:** Luna added visible rules panels in both spreadsheets, at Julian's request for cheaper delegation.
- **Check:** Parent reviewed every rule and compared all existing values/formulas against fresh snapshots; unchanged. Clarified tax jurisdiction during review.
- **Outcome:** Classification and refresh instructions live beside the model. Incremental tokens unmeasured.
- **Lesson:** Verification: the word deductible needs a named tax jurisdiction when two tax systems apply.
- **Deliverable:** [[savings-v3-review]].

## 2026-09-26 · Build + Verification · Worked · [[savings-v3-review]] restored housing

- **Work:** Restored occupied-home housing to living costs and rental-only property expense rows; aligned both companion notes.
- **Check:**440 live before/after output comparisons; no differences or formula errors. Tax sources distinguish UK overseas-rental expenses from HK statutory deductions.
- **Outcome:** Requested simpler structure restored. Incremental tokens unmeasured.
- **Lesson:** Steering: define both the cash-cost owner and tax jurisdiction before moving expenses between sheets. Unchanged totals alone do not establish correct classification.
- **Deliverable:** [[savings-v3-review]].

## 2026-09-26 · Build + Verification · Worked · [[savings-v3-review]] housing split

- **Work:** Coordinated housing cost transfer, hotels to Transport, lean classification preserved, both companions updated. Sol stalled and was interrupted; exact edits handed to Luna at Julian's request for cheaper execution.
- **Check:** Parent live comparison of440 outputs against fresh snapshots; Luna independent verification. Native cut/paste expanded a housing sum incorrectly; corrected before final check.
- **Outcome:** Savings, taxes and runway unchanged; living inputs exclude Housing. Parent token checkpoint in deliverable; delegate usage unmeasured.
- **Lesson:** Routing/verification: use a bounded cell-level brief and snapshots; inspect automatic range expansion after moving cells.
- **Deliverable:** [[savings-v3-review]].

## 2026-09-26 · Build + Verification · Worked · [[savings-v3-review]] Cash + MPF

- **Work:** Added fourth pot and full/lean runway cases.
- **Check:** Parent independently verified eight new numeric results and60 original model/validation values against snapshots.
- **Outcome:** Passed; native row insertions shifted university references without changing results. Incremental tokens unmeasured.
- **Lesson:** Verification: row insertion shifts formula references but not prose references; check both.
- **Deliverable:** [[savings-v3-review]].

## 2026-09-25 · Build + Verification · Worked · [[savings-v3-review]] lean table

- **Work:** Appended lean no-salary runway and source/explanation notes.
- **Check:** Source row175 snapshots, burn reconciliation against discretionary totals and all16 numeric runway results independently calculated.
- **Outcome:** Verified; previous tables unchanged. Inputs explicitly identified as editable snapshots. Incremental tokens unmeasured.
- **Lesson:** Verification: preserve source budget classification and disclose its consequences, rather than silently reclassifying spending.
- **Deliverable:** [[savings-v3-review]].

## 2026-09-25 · Build + Verification · Worked · [[savings-v3-review]] runway extension

- **Work:** Sol appended editable balance inputs and formula-based no-salary runway tables; Luna independently verified live output.
- **Check:** Before/live comparison of1,254 original cells, all16 numeric runway outputs, formula dependencies, guards and HK MPF exclusion; parent arithmetic cross-check.
- **Outcome:** Complete, original cells unchanged, net cash788,273. Inputs B69:B75; exact manifest in deliverable. Incremental token effort unmeasured.
- **Lesson:** Verification: retain a full pre-edit cell snapshot before append-only work so preservation is measurable.
- **Deliverable:** [[savings-v3-review]].

## 2026-09-25 · Build + Verification · Worked · [[savings-v3-review]] delegated repairs

- **Work:** User-authorised Sol savings-formula repairs and Luna exact cashflow edits on separate spreadsheets.
- **Check:** Parent independently reread both sheets, matched source inputs and recalculated 198 annual/cumulative outputs. Delegate tested date and FX changes and restored inputs.
- **Outcome:** Agreed changes complete with no discrepancies. Parent cumulative token checkpoint recorded in deliverable; delegate effort unmeasured.
- **Lesson:** Routing: give each delegate a separate write target and explicit cells, then verify cross-file dependencies at the parent level.
- **Deliverable:** [[savings-v3-review]].

## 2026-09-25 · Critique · Worked · [[savings-v3-review]] follow-up

- **Work:** Checked Julian's updated savings tab and outstanding cashflow edits, read-only.
- **Check:** 108 formula comparisons and 198 savings calculations, plus source tracing.
- **Outcome:** Main corrections work; cashflow unchanged. Flagged unused date inputs, hardcoded annual FX and minor contents mismatch. Incremental tokens unmeasured.
- **Lesson:** Verification: test parameter dependencies and distinguish anticipated source corrections from live source values.
- **Deliverable:** [[savings-v3-review]].

## 2026-09-25 · Critique · Worked · [[savings-v3-review]]

- **Work:** Independently reviewed all 18 v3 relocation savings scenarios, using the supplied briefing and accepted prior rental-tax review.
- **Check:** Separate arithmetic for each tax scenario, live formula and cashflow tracing, official HMRC/IRD sources; Julian adjudicates the findings. Report: [[uk-relocation-savings-v3-codex-review-2026-09-25]].
- **Outcome:** Annual property-tax arithmetic agrees; found expired FIG relief carried into years 5 to 10, an outdated HK allowance, hardcoded taxes and smaller source-budget flags. Sheets unchanged. Thread usage 214,260 tokens at checkpoint, including earlier work; review-only effort unmeasured.
- **Lesson:** Verification: an identity check can say OK while repeating the model's error. Check relief duration and input-to-tax dependencies separately from cashflow arithmetic.
- **Deliverable:** [[savings-v3-review]].

---

## 2026-09-23/24 · Research + Analysis · Partly · [[uktax-srt-fy26-27]]

- **Work:** UK Statutory Residence Test position for Julian and Sophia, 2026/27 and forward exposure. ~1,600 lines plus a derived negotiation brief. Nine review passes: seven Fable peer reviews against primary sources, two Codex adversarial (GPT-5.6, then gpt-6-astra at high effort).
- **Check:** layered adversarial review against FA 2013 Sch 45 and the HMRC RFIG manual, plus Julian's own line-by-line verification reading over two days.
- **Outcome:** Partly. The legal analysis verified correct at every round - all fourteen original claims held. But ~40 corrections were needed, two were legal errors, and the final pass found a blocking item (Sophia's unverified 2024/25 day count) that had been sitting in the document's own register marked "worth confirming".
- **Lesson:** **Verification** - the chain step that failed. Output carried ~40 errors, of which only one traced to a missing fact; the rest were generation faults - two legal errors, fact-sensitive judgements repeatedly written as settled, omissions, self-contradictions, and three rebuilds of things already in the wiki. Nine automated review rounds each caught real defects but **did not substitute for a human reading for meaning**: the highest-yield check of the two days was Julian questioning jargon and undefined terms, which surfaced substantive errors while ostensibly asking about wording. **Automated adversarial review and plain-language reading catch different error classes**, and the first does not cover the second. Secondary: the fact base was not closed before the analysis opened, which caused three answer reversals and meant each correction invalidated the review of what it replaced - a contributor to the rework volume, not its main cause.
- **Cards created:** [[mm-facts-first]], [[mm-fluency-bias]], [[mm-write-for-the-stranger]]
- **Deliverable:** [[uktax-srt-fy26-27]]

---

## 2026-09-24 · Build + Wiki ops · Partly · [[genai-governance-recall-repair]]

- **Work:** repaired the governance-recall gap found during [[uktax-srt-fy26-27]] - SessionStart directory hook, work-handback hook moved user-level, `## Session Synopsis` added to the three define-* templates, two new cards, `bias-check` renamed and widened to `behaviour-check` over both indexes.
- **Check:** Julian steering in-session; three proposals caught and reversed before shipping.
- **Outcome:** Partly. The artefacts are sound. The process was not: three times the model proposed building something the wiki already held - [[mm-token-economics]] (delegation keeps the main transcript small), [[genai-task-workflow-log]] itself (per-run lessons), and [[mm-admission-qualification]] (retroactive records for work that drifted out of exempt). Each was caught by Julian asking the model to check, not by the model checking.
- **Lesson:** **Routing** - the chain step that failed. The model reasoned from first principles in a domain where a written index existed, because nothing surfaced it. Biases had a dispatcher and mental models did not; that asymmetry is the root cause and `behaviour-check` is the fix. Secondary: the whole session ran outside the vault, so AGENTS.md never loaded - governance that only loads in one directory is governance that silently fails.
- **Deliverable:** [[genai-governance-recall-repair]]

---

## 2026-09-19 · Build + Wiki ops · Worked · [[bias-history-review]]

- **Work:** Three-tier bias mining pipeline over Julian's full session history
  (183 transcripts, 213MB pre-filtered to 2,694 of his own messages): 20 Haiku
  scanners seeded with 8 priors, a merge stage, 10 Sonnet adversarial verifiers
  (three-way verdicts, quote-grepping against source). Then the estate build:
  12 bias cards, 3 renames, biases-index, behaviour-check skill, narrative-fill
  memory, card-floor rule.
- **Check:** Sonnet refuters per candidate (caught 1 fabricated quote, 1
  double-count, 1 simulated dialogue misattributed as real speech); Fable
  spot-check of kills and uncertains; separate adversarial agent over the
  written artefacts; Julian's verdicts on the mapping table before writing.
- **Outcome:** Worked - 122 raw candidates reduced to 4 confirmed, 2 uncertain
  (both ruled real-but-narrower), 4 refuted. Scan runs: 52,814 (failed run) +
  2,237,963 tokens. One mechanical failure: workflow args arrived as a string,
  scanners built zero chunks, pipeline completed "successfully" in 5s with
  empty output.
- **Lesson:** Two. (1) A pipeline that runs to completion with zero input looks
  identical to success - guard loudly on empty inputs (the fix: throw on bad
  args). (2) The adversarial verify layer paid for itself: without it, a
  fabricated quote and an inverted reading of real quotes would have entered
  the wiki as documented biases.

## 2026-09-09 · Critique · Worked · [[ddg-caio-involvement-recommendation]]

- **Work:** Codex (gpt-5.6-sol, effort high, read-only) ran an adversarial review
  of the DDG alternative-proposal draft v1, hunting bias in both directions,
  while Julian read the draft in parallel. Findings in
  [[ddg-alternative-proposal-codex-review-2026-09-09]].
- **Check:** Independent second-model review per the multi-agent protocol; Julian
  judges each finding before any is applied.
- **Outcome:** Worked - 11 ranked findings incl. a genuine arithmetic error
  (30-50 vs 18-50 consultant-weeks) and a strawman of the client's own brief.
  Verdict RESTRUCTURE. 44,232 tokens.
- **Lesson:** Two mechanical failures preceded the run: the model name needed a
  newer Codex CLI, and after upgrading, the plugin's long-running app-server was
  still the old binary and had to be restarted. Check runtime versions, not just
  installed versions, when a model is rejected.

- **Work:** Authored [[mm-admission-qualification]] (step-0 model compressing
  the AGENTS.md admission tiers) plus chain-table and index wiring, prompted by
  the exempt-vs-fast-lane confusion at the close of the Avios compile.
- **Check:** Deterministic (six-slot sections present, links resolve, every
  chain step now has a model) plus Julian's scope review before creation and
  read-through after.
- **Outcome:** Worked - 15 attended min, 131k tokens. Scope and filename agreed
  before writing; no corrections needed after.
- **Lesson:** Agreeing the scope slot-by-slot before writing the file made the
  review trivial - the cheap move is scoping out loud, not drafting and
  repairing. Also the model's own origin lesson: doctrine without a reach-for
  layer generates repeat confusion however canonical the text.

## 2026-09-04 · Wiki ops · Worked · [[airmiles-mental-model]]

- **Work:** Compiled Julian's BA Avios note into the vault's first Finance
  mental model ([[mm-airmiles-redemption]] + [[ba-avios-redemption]], two-tier),
  then two extensions dictated by him in-session (principle rationales, the
  human/LLM split for running the model live).
- **Check:** Deterministic (files, links, indexes, ops-log row) plus Julian's
  close-out read-through.
- **Outcome:** Worked - 30 attended min, 333k tokens. One error: the
  worked-example route was inferred from currency clues (guessed Hong Kong to
  Bangkok; it was Bangkok to London) and only Julian's review caught it.
- **Lesson:** Step at fault: steering. In a compile, a fact absent from the
  source is a question for Julian, not a gap to fill by inference - same rule
  as verify-before-writing, applied to context the model supplies itself.

## 2026-09-03 · Taste work (admission ceremony) · Failed · [[ai-engineering-patterns]] Deliverable 2

- **Work:** Defining the D2 enabler (task-routing skill) through the standard
  ceremony. Spread across four sessions (24 Aug - 3 Sep); the definition never
  completed, and Julian paid the context re-acquaintance cost three times
  ("remind me the scope", "what have we defined so far", "tell me about the
  skill again").
- **Check:** n/a - nothing was ever routed, because admission never finished.
  That is the failure.
- **Outcome:** Failed - defining the work cost more of Julian's time than
  doing it would have (the machine does the doing).
- **Lesson:** Step at fault: admission. Deciding what and why is Taste work - only Julian can do it. The
  process made too much of it (a full interview for a machine-built 2h box)
  and split it across four sessions, paying the forgetting tax each time.
  Keep admission small, do it in one sitting, build immediately. Fix: the
  AGENTS.md Admission Fast Lane, created from this failure.

## 2026-09-03 · Build + Wiki ops · Worked · [[routing-work-system]]

- **Work:** Built the routing-work system in one interactive session: three new
  wiki files, chain edits across five mental models, an AGENTS.md rule, a
  SessionStart hook, register rows.
- **Check:** Deterministic - hook branches pipe-tested, links resolve, mirrors
  match source, formats validate.
- **Outcome:** Worked - 60 attended minutes + 819k tokens for work that would
  have taken a day-plus by hand; nothing needed rework.
- **Lesson:** Deterministic-check work delegates profitably at volume. Direct
  contrast with the 1 Sep entry: same week, same tools, opposite outcome,
  separated only by check profile.

## 2026-09-01 · Taste work · Partly · [[uk-relocation-project]] (BAU Kanban cards)

- **Work:** Claude drafted the text of a batch of BAU Kanban task cards and
  created the board; the task list itself was already mine.
- **Check:** Human judgement only - card text had to match my terse operational
  register, and only I can judge that.
- **Outcome:** Partly - the board mechanics were fine, but every card came back
  verbose despite the AGENTS.md writing rules, and I rewrote all of them
  (~120 focused minutes, more than writing them myself would have cost).
- **Lesson:** Step at fault: work type. Text in my register is taste work even
  when it looks like mechanical ops. Split next time: I write the card text,
  Claude does the Jira creation. An instruction (the length rule) is not a
  guarantee. Extends hold-the-pen beyond personal messages.

## 2026-08-21 · Critique · Worked · [[tti-comms-log]]

- **Work:** Claude critiqued and fact-checked a message I had drafted myself to
  Stephan/Ty.
- **Check:** Human judgement, cheap - I read each finding and judged it in
  seconds.
- **Outcome:** Worked - the critique caught a claim in my draft that was untrue
  against the record, before it was sent.
- **Lesson:** On voice work, critique and fact-check is where Claude's value is.
  Pair this with the entry below: same run, the two halves of hold-the-pen.

## 2026-08-21 · Taste work · Failed · [[tti-comms-log]]

- **Work:** Claude drafted personal messages to Stephan and Ty in my voice,
  iterating on tone and content.
- **Check:** Human judgement only - no external criterion for "sounds like me".
- **Outcome:** Failed - three drafts in a row rejected; I wrote my own and had
  Claude critique it instead (the entry above). Nine iterations were also burned
  polishing a message events then killed.
- **Lesson:** Step at fault: routing (should have been by hand). I hold the pen
  on my voice. And don't polish a pending message
  while events are still moving - draft close to the send moment.

## 2026-09-26 · Analysis + sheet build · Worked, at a cost · [[savings-v3-review]]

- **Work:** Rebuilt the relocation savings model: property tax and FIG into the
  sheet, runway blocks, wiki companions rewritten. Claude did the analysis and
  the wiki; Codex did the Google Sheet edits; Codex reviewed the sheet.
- **Check:** Codex independent recalculation of all 18 then 20 columns against
  Claude's figures; Claude re-reading the sheet after each Codex pass; Julian
  reading every table.
- **Outcome:** Worked. Numbers correct and reconciled across sheet, two wiki
  notes and the financial model. Cost: ~8 attended hours over two days, three
  Codex allowance exhaustions, and Julian relaying edits between two windows.
- **Lesson:** Step at fault: routing. Claude's Drive connector cannot write
  cells, so sheet work went to Codex with Julian as the relay. Either share the
  sheets with Claude's service account so it edits in place, or run sheet-heavy
  work in Codex with Claude as reviewer; do not split one task across both with
  a human in the middle. Second, verification: Claude declared the sheet done
  without re-reading the scope amendment, which named the double-count it had
  just introduced. Re-read the record before saying done.

## 2026-09-27 · Decision capture + file restructure · Worked · [[HK-Return-BRAIND]]

- **Work:** Julian dumped intuition on the return-to-HK question in chat; Claude
  logged it in his words, populated B and R from the August HK-BRAIND with each
  row sourced, built the 6/8/10-year comparison from the savings note, wrote the
  BRAIND file convention, then delegated the restructure of four files to a
  subagent.
- **Check:** Julian reading every table and row as it landed; subagent edits by
  exact-match assertion with a git diff of removed lines; Claude re-reading
  headings and banner after the subagent returned.
- **Outcome:** Worked. Julian 5/5, 15 attended minutes on the refactor. Session
  1.15M effort tokens plus 109k subagent tokens.
- **Lesson:** Step at fault: steering, twice, both Claude's. (1) Coined labels
  and bare claim numbers in summaries forced three clarification rounds; the
  plain-writing correction now has its third instance. (2) A one-word reading of
  "forget it" dropped a row Julian wanted kept; when an instruction is one word,
  confirm before deleting. Delegating the mechanical restructure with a fixed
  spec was the right routing and produced zero content errors.

## 2026-09-27 · Sheet change + companion re-read · Worked, with one self-inflicted loss · [[savings-v3-review]]

- **Work:** Codex built the university reserve into every column of the savings
  sheet; Claude read the sheet, briefed a subagent with every new figure, and the
  subagent re-read all nine sections of the companion note. Downstream files
  updated by Claude.
- **Check:** Sheet validation cells (all OK); subagent reported item by item and
  listed what it could not match; Claude spot-checked headings, tables and figures
  against the sheet; Julian confirmed the reserve total.
- **Outcome:** Worked. Julian 15 attended minutes. Codex about 699k tokens,
  subagent 126k. The subagent's "these tables do not exist" report exposed that a
  Claude edit earlier the same day had deleted two tables from the note; both
  rebuilt from the sheet.
- **Lesson:** Step at fault: verification, Claude's. A find-and-replace anchored on
  a generic table header ("| Scenario ") matched an earlier table and silently
  removed everything between it and the target. Anchor replacements on a unique
  heading, and diff the section count before and after any block replacement.
  Routing worked: sheet to Codex, companion re-read to a subagent with the
  figures in the brief, verification by the parent.
