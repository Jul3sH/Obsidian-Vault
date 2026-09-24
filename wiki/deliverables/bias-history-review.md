---
type: deliverable
kind: task
created: 2026-09-19
status: in-progress
size: 2
lane: fast-lane
tags: [deliverable, bias, working-with-yourself, ai-os]
---

# Bias History Review

This is the fast-lane record for a machine-executed review of Julian's full Claude session history (his own messages only) to identify personal biases, verify them adversarially, and turn the confirmed ones into practical steering artefacts (mental-model cards, a biases index, a checking skill). It was created 2026-09-19 under the AGENTS.md Admission Fast Lane after a 30-minute design discussion in place of full define/Prompt-Zero ceremony. Julian reads this file to see the brief, the done-criteria, and the effort log; the pipeline results and verdicts are appended here as work completes.

## Brief (Admission Fast Lane, agreed 2026-09-19)

**Why (one sentence):** Julian's biases are currently documented ad hoc (some in memory, some as articles); mining the full session history gives an evidence base to document them properly and steer future behaviour and decisions practically.

**Pipeline (hierarchical by reasoning load):**
1. Pre-filter script: extract Julian's own messages (with dates, session IDs) from `~/.claude/projects/` transcripts. His words only, not model output.
2. Haiku scanner sub-agents sweep the extracted text in chunks, seeded with the known priors, returning candidate biases with verbatim dated quotes.
3. Merge/dedup stage consolidates candidates across chunks.
4. Sonnet adversarial verifiers attempt to refute each candidate; three-way verdict (refuted / confirmed / uncertain). Uncertain escalates to Fable; Fable spot-checks a sample of kills.
5. Fable (main session, in-context) compares survivors to known priors, asks Julian clarification questions where evidence is ambiguous, drafts cards.
6. Julian gives the final verdict per bias and nominates memory backstops.

**Output design (agreed):**
- Card floor: every confirmed bias gets an mm card (six-slot format, listed in mental-models-index). Detail articles only where evidence warrants. Rule to be written into `documentation-conventions.md` Part 1.
- `wiki/performance/biases-index.md` (agreed name): one row per bias - trigger situation + card link.
- A `behaviour-check` dispatcher skill whose trigger description covers every index row's situation type; adding an index row includes checking/widening the skill trigger in the same operation.
- Memory backstop reserved for the most critical AND most common biases (in case the skill doesn't fire), nominated by Julian.
- Daily mm-refresher hook covers training for decisions made outside sessions (already exists; new cards enter automatically).

**Load-bearing assumption:** Julian's messages in these transcripts are a faithful sample of how he actually decides, not just of how he talks to Claude.

**Named verifiers (adversarial coverage):**
- Candidate biases: Sonnet refutation agents (stage 4).
- Drafted cards / index / synthesis output: one adversarial review pass before Julian sees them (synthesis is a content-producing stage; per AGENTS.md it does not reach sign-off unchecked).
- Final sign-off: Julian.

## Done-Criteria

1. Transcripts pre-filtered to Julian's own messages (with dates); Haiku scanners sweep them, seeded with known priors; every candidate carries quoted, dated evidence.
2. Every candidate passes an adversarial refutation pass before reaching Julian; survivors presented with evidence, clarification questions asked where ambiguous.
3. Known priors (visual-representation, overanalysis, commitment-stalling, decision-reopening, build-don't-adopt, assumption-blindness) each get a confirmed / weakened / unchanged verdict.
4. Every confirmed bias gets an mm card (six-slot, listed in mental-models-index) and a biases-index row; detail articles only where evidence warrants; card-floor rule written into documentation-conventions.md.
5. behaviour-check skill built, trigger covering every index row's situation type, documented and mirrored per the skills rule.
6. Julian nominates which biases (if any) get the memory backstop.

## Status

⚠ As of 19 Sep 2026 (evening): pipeline run, all artefacts built, artefact-level adversarial review complete - 12 findings, all fixed same day (an invented fourth contact in mm-recency-bias; scan verdicts misattributed as "confirmed" in the two ruled-uncertain cards; a paraphrase presented as a verbatim quote in mm-overanalysis-bias; unverified chunk-counts stated as confirmed evidence in three cards + the memory; a register hypothesis stated as fact in mm-commitment-by-proxy-bias; a near-verbatim unattributed register restatement in mm-optimism-accounting-bias; five biases-index rows uncovered by the behaviour-check skill's triggers - trigger list widened seven to twelve). One accepted legacy defect: mm-fear-disguise-bias's six Evidence links resolve to raw/_processed/ lessons-learnt files, not wiki/ (pre-existing before the rename; Obsidian resolves them vault-wide). Awaiting Julian's final read-through and sign-off.

## Prior Verdicts (criterion 3, recorded 19 Sep 2026)

| Prior | Verdict from evidence |
|-------|----------------------|
| visual-representation-bias | Confirmed, unchanged (11 chunks; already fully built) |
| overanalysis | Confirmed (12 chunks, enacted) - promoted from memory-only to card |
| commitment-stalling | Confirmed (11 chunks) - promoted from memory-only to card; options-preservation identified as likely mechanism |
| decision-reopening | Confirmed but managed - strongest instances clean (5 Jul, 7 Jul, 18 Aug); half the scanned instances were legitimate updating on new facts; all within one saga |
| build-dont-adopt | Real but narrower than framed - one unambiguous instance (Jira, 22 Jul); folder-structure counter-example shows forcing functions beat it |
| assumption-blindness | Weakened / managed - evidence shows Julian actively surfacing assumptions, clustering after the 28 Jul memory; no card, memory stays as control |
| confirmation-bias (classic) | Refuted as a personal analytical tilt (one fabricated quote killed; record shows him commissioning hostile reviews) - the real form is confirmation-amplification via the helper model (register #4), now carded |
| stories-arent-evidence | Confirmed as the most broadly evidenced bias (15 chunks, enacted) - renamed to narrative-fill-bias, promoted to memory backstop |

Scan stats: 183 transcripts → 2,694 Julian messages → 122 raw candidates → 10 merged → 4 confirmed / 2 uncertain / 4 refuted. New-candidate discoveries (strategic-narrative-construction, autonomy-options-prioritisation) both refuted; the second folded into commitment-stalling as mechanism.

## Card Mapping (proposed 19 Sep 2026; approved by Julian same day; executed - see Status)

Rule applied (agreed 19 Sep): every bias has its own six-slot mm card with "bias" in the name; the card links to detail and countermeasure, never restates them. All personal bias cards live in `wiki/performance/working-with-yourself/`; generic-tier cards stay in `the-human-mind/`.

**New cards (12):**

| Card | Evidence source | Links to (detail / cure) |
|------|----------------|--------------------------|
| mm-overanalysis-bias | Scan: confirmed, 12 chunks | Cure: decision-feeds test, [[ai-os/skills/prompt-zero/SKILL\|prompt-zero]], [[mm-timebox-the-rabbit-hole]] (rabbit-holing folded in as mechanism) |
| mm-commitment-stalling-bias | Scan: confirmed, 11 chunks | Detail: [[commitment-avoidance]]; cure: [[mm-commit-with-a-forcing-function]]; mechanism note: options-preservation (autonomy finding folded in) |
| mm-decision-reopening-bias | Scan: uncertain, ruled confirmed-but-managed; register #1 | Detail: [[commitment-lock-protocol]]; cure: commitment-guard skill, reopen test |
| mm-build-dont-adopt-bias | Scan: uncertain, ruled real-but-narrower | Cure: adoption forcing-function, [[systems-register]] rule |
| mm-confirmation-amplification-bias | Register #4 (personal form of confirmation bias) | Detail: [[commitment-lock-protocol]] division of labour; cure: case-builder never validates |
| mm-recency-bias | Register #2 | Cure: 48h warm-contact stand-down |
| mm-certainty-spike-bias | Register #3 | Cure: conviction >90% = warning light, anchor re-read |
| mm-answer-first-bias | Register #5 | Cure: anchor docs only after adversarial review |
| mm-optimism-accounting-bias | Register #6 | Cure: Banked/Hoped two-column rule |
| mm-loss-aversion-bias | Register #7 | Cure: "state the floor; state the scenario that breaches it" |
| mm-sunk-cost-bias | Register #8 | Cure: dated review trigger; "best deployed" question |
| mm-commitment-by-proxy-bias | Register #9 | Cure: retyping rule (lock condition 1) |

**Renames (3):** mm-stories-arent-evidence → mm-narrative-fill-bias (5 inbound files to repoint); mm-payoff-vs-prestige → mm-payoff-vs-prestige-bias (3); mm-fear-wears-a-disguise → mm-fear-disguise-bias (4).

**Unchanged (2):** mm-visual-representation-bias; mm-confirmation-bias (generic tier).

**Explicitly not carded:** assumption-blindness (scan refuted the active bias; evidence shows the assumption-audit control working - memory stays as the control); strategic-narrative-construction (deliberate skill, not a bias); autonomy-options-prioritisation (folded into commitment-stalling as mechanism); cure/discipline cards (timebox-the-rabbit-hole, commit-with-a-forcing-function, never-react, eggs-in-one-basket, start-to-start, impaired-state-rules) unchanged - they are countermeasures, not biases.

**biases-index.md:** 17 rows (12 new + 3 renamed + 2 unchanged), each: trigger situation + card link.

**Memory backstop proposal:** keep visual-representation-bias and decision-reopening; add narrative-fill (highest frequency, drives real stakeholder strategy). No others.

**behaviour-check skill trigger situations (v1):** weighing life/career options; wobble after a locked decision; scoping a piece of analysis; at the point of sending/committing; interpreting someone's silence or behaviour; building financial models or plans; designing a new system or process.

## Content Verification (phase 3 - open as of 19 Sep 2026)

The system is built and its outputs exist, but Julian has not yet content-verified them. Estimated ~1h attended. Tick each on review; corrections go back through normal edits. When all are ticked, this deliverable closes and total attended minutes roll up to [[estimation-baseline]] with the build/verify split preserved.

- [ ] [[biases-index]] (17 rows: right biases, right trigger wording)
- [ ] mm-overanalysis-bias / mm-commitment-stalling-bias / mm-decision-reopening-bias / mm-build-dont-adopt-bias (scan-evidenced cards)
- [ ] mm-confirmation-amplification-bias / mm-recency-bias / mm-certainty-spike-bias / mm-answer-first-bias / mm-optimism-accounting-bias / mm-loss-aversion-bias / mm-sunk-cost-bias / mm-commitment-by-proxy-bias (register-derived cards)
- [ ] mm-narrative-fill-bias / mm-payoff-vs-prestige-bias / mm-fear-disguise-bias (renamed cards, incl. renamed-from notes)
- [ ] behaviour-check skill wiki mirror (twelve triggers read sensibly)
- [ ] feedback-narrative-fill memory wiki mirror
- [ ] Card-floor rule wording in documentation-conventions.md Part 1

## Time and Token Log

| Date | Type | Effort | Notes |
|------|------|--------|-------|
| 2026-09-19 | Julian attended | 30 min | Fast-lane design discussion: pipeline, output design, done-criteria (this session, self-reported) |
| 2026-09-19 | Machine (workflow) | 52,814 tokens | First scan run: failed mechanically (args arrived as string, zero chunks scanned); only merge agent ran |
| 2026-09-19 | Machine (workflow) | 2,237,963 tokens | Full scan run: 20 Haiku scanners + merge + 10 Sonnet adversarial verifiers; 122 raw candidates, 10 merged, verdicts 4 confirmed / 2 uncertain / 4 refuted |
| 2026-09-19 | Machine (agent) | 130,810 tokens | Artefact-level adversarial review of all created cards, indexes, skill, memory; 12 findings, all fixed |
| 2026-09-19 | Julian attended | 30 min | Phase 2, system build and run: mapping-table review, verdict discussions, output spot-check (self-reported). Content verification of the produced artefacts deliberately NOT included - it is a separate phase, logged below when done |
