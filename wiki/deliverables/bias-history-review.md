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
- A `bias-check` dispatcher skill whose trigger description covers every index row's situation type; adding an index row includes checking/widening the skill trigger in the same operation.
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
5. bias-check skill built, trigger covering every index row's situation type, documented and mirrored per the skills rule.
6. Julian nominates which biases (if any) get the memory backstop.

## Time and Token Log

| Date | Type | Effort | Notes |
|------|------|--------|-------|
| 2026-09-19 | Julian attended | 30 min | Fast-lane design discussion: pipeline, output design, done-criteria (this session, self-reported) |
| 2026-09-19 | Machine (workflow) | 52,814 tokens | First scan run: failed mechanically (args arrived as string, zero chunks scanned); only merge agent ran |
| 2026-09-19 | Machine (workflow) | 2,237,963 tokens | Full scan run: 20 Haiku scanners + merge + 10 Sonnet adversarial verifiers; 122 raw candidates, 10 merged, verdicts 4 confirmed / 2 uncertain / 4 refuted |
