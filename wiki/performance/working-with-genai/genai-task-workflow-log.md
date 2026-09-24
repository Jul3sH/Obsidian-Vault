---
type: log
created: 2026-09-03
updated: 2026-09-04
status: active
tags: [working-with-genai, routing, log]
---

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
