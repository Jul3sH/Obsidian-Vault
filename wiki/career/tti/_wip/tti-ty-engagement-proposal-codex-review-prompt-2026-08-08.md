---
type: review-prompt
tags: [career, tti, review, adversarial, codex]
status: active
created: 2026-08-08
reviewer: Codex
target: tti-ty-engagement-proposal
output: tti-ty-engagement-proposal-codex-review-2026-08-08
supersedes-review: tti-ty-engagement-proposal-codex-review-2026-08-07
---

# Codex Adversarial Review Prompt - TTI Ty Engagement Proposal (round 2)

> **Purpose:** the document has changed substantially since the 7 Aug review found one
> FATAL and seven SERIOUS findings. All were addressed. This round checks (a) whether
> the fixes actually resolved the original findings or just moved them, and (b) whether
> the substantial new material introduced fresh problems. Different model from the
> drafter, per [[tti-ty-proposal]]'s stopping condition. Copy everything inside the
> fence below into Codex.

```
You are conducting a SECOND adversarial review of a document you have not seen before.
Read these files first, in this order.

VAULT ROOT: /Users/julianhart/Obsidian Vault

1. wiki/ai-os/system-design/generic/multi-agent-protocol.md
   Your role, output file naming, handoff discipline, frontmatter authority levels.
   Read it in full before starting.

2. THE PRIOR REVIEW (read this before the document itself):
   wiki/career/tti/_wip/tti-ty-engagement-proposal-codex-review-2026-08-07.md
   This found one FATAL (month 1 read as discovery, so the buyer committed to 12
   months before the value case existed) and seven SERIOUS findings. The author
   states all were addressed. YOUR JOB includes verifying that claim, not assuming it.

3. THE DOCUMENT UNDER REVIEW (current version, changed substantially since the prior review):
   wiki/career/tti/_wip/tti-ty-engagement-proposal.md

4. SUPPORTING CONTEXT (read all):
   wiki/career/tti/_reference/tti-2025-ar-key-initiatives.md
       - Ty Staviski's own stated targets and live initiatives (AR25).
   wiki/career/tti/_wip/tti-h1-2026-results-talking-points.md
       - NEW since the prior review. H1 2026 results (30 Jun 2026 HKEX announcement).
         The proposal now cites the SG&A/margin finding and the raised free cash flow
         target from this source. Verify the figures are used correctly and that
         nothing here is misattributed to Ty or Kari as something they said.
   wiki/career/tti/_wip/tti-ea-requirements.md
       - NEW since the prior review. A sourced, verbatim log of every requirement Ty
         or Kari have actually stated, tagged DIRECT / RELAYED / PUBLIC / INTERNAL.
         Check the proposal against this: does anything in the proposal claim or imply
         knowledge tagged INTERNAL (i.e. from an employee town hall, not something
         Julian was told directly or that is publicly published)? That would be a
         FATAL - it would reveal Julian holds material he should not have and cannot
         explain the source of. Read the "Quotability" section in this file carefully.
   wiki/career/independent-consulting-pricing.md
       - The rate, its basis, and why anchoring higher was rejected.
   wiki/career/tti/_wip/tti-cfo-brief.md
       - An earlier brief to the same buyer, plus an appendix recording a PRIOR
         red-team (not the 7 Aug one) that killed it for bracketed numbers, circular
         hire-first-justify-later logic, and no reason to act now. Confirm none of
         these three failure modes have returned in any form.
   wiki/career/tti/_wip/tti-ty-call-simulation-2026-07-19.md
       - Dry run of a conversation with the same buyer.
   wiki/career/tti/_wip/tti-engagement-strategy.md
       - Political dynamics, including the Tony Chung risk.
   wiki/career/tti/_wip/tti-story-bank.md
       - Prior-proof and credibility material (§1a: BG Group Design Authority - the
         answer to "where have you done this before?"; §3: predictable role-specific
         questions). This is SPOKEN-VERSION reserve material, not printed in the
         proposal itself. Read it so you understand what Julian can fall back on
         verbally if you ask a question the printed document doesn't answer - but
         evaluate the printed document on its own; do not credit it for material that
         only exists elsewhere.
   wiki/deliverables/tti-ty-proposal.md
       - The deliverable definition: completion criteria, load-bearing assumptions,
         and the stopping condition this review exists to satisfy.

ROLE
Adopt the persona of Ty Staviski, Deputy CFO of Techtronic Industries (US$15.3bn
revenue), reading this cold on a Monday after travel. You are numerate, busy,
commercially sceptical, and you did not ask for an enterprise architect - you asked
what this person would do and what they cost. You have no particular belief that
enterprise architecture is valuable. Treat "architecture" as an unproven category
until the document earns it. You have read the company's own H1 2026 results.

SITUATION
Julian Hart is an external candidate, introduced through a family relationship with
TTI's Vice-Chairman. He has no delivery track record inside TTI. He is asking for a
12-month committed engagement at US$320,644 with no break clause. He needs a decision
in roughly 24 hours. He gets one phone call to land this.

WHAT TO ATTACK - be specific, not general

1. VERIFY THE FATAL FIX. The prior review's core objection was: month 1 read as
   discovery, so Ty would be committing before he could see the value case. The
   document now claims month 1 is "execution, not a study" - one live cross-region
   decision taken through the mechanism (named owner, standard, ratifier, date), plus
   a decision map and a costed baseline. Does this actually resolve the objection, or
   does it just relabel discovery as execution while still being unfalsifiable until
   week one happens? Be genuinely hard on this - it is the one place a re-review most
   often finds the same wound with a bandage over it.
2. THE NEW FINANCIAL MATERIAL (SG&A finding, FCF lever). Check the logic independently.
   The document claims: gross margin +258bps, SG&A +173bps, EBIT +86bps in H1 2026,
   and that free cash flow = operating cash flow minus capex, so avoided technology
   capex flows into the raised FCF target. Is this arithmetic and mechanism sound, or
   does it strain to make two points out of one finding? Does citing TTI's own H1
   results read as informed, or as a candidate reaching for anything topical?
3. THE PROCUREMENT LEVERAGE ROW. It now claims standardisation enables consolidated
   vendor negotiation, while explicitly saying Julian does not do the negotiating
   himself. Does this distinction hold, or does a sharp CFO read it as claiming credit
   for procurement's job regardless of the hedge?
4. THE NEW DIRECTOR-LEVEL DEFENCE (judgement gap vs authority gap, positioned just
   before the price). Test both halves. Is "AI closes the drafting gap but not the
   judgement gap" a real distinction or a rhetorical move? Is "a principal lacks the
   standing to make it stick across directors" evidenced anywhere, or asserted? Does
   placing this paragraph immediately before the fee look like a deliberate answer to
   an anticipated objection, or does it look defensive - like Julian pre-empting a
   question that makes the read worse, not better?
5. The no-break 12-month commitment. Now that month 1 is reframed as execution, is the
   commitment structure actually de-risked, or does the FATAL from round 1 still exist
   in a different shape - e.g. Ty is now committing to trust that ONE decision, chosen
   in week one against unstated criteria, will be representative of whether the whole
   mechanism works?
6. What can Julian NOT evidence? Identify every claim in the CURRENT document that
   would collapse under "give me an example of where you have done this before" -
   noting that the printed document itself does not contain the BG Group prior-proof
   answer; that lives only in story-bank as a spoken fallback. Is the printed document
   self-sufficient, or does it depend on Julian saying things out loud that are not on
   the page?
7. Political exposure. Tony Chung (SVP Finance APAC) has multiple technology
   directors reporting to him and is a documented probable detractor. Does anything
   here hand him ammunition? Specifically check the "Portfolio duplication" and
   "Procurement leverage" rows, which name no specific systems now (this was fixed
   after round 1) - confirm that fix held and nothing re-introduces a specific,
   attributable target.
8. INTERNAL-SOURCED MATERIAL. Cross-check every substantive claim about TTI's current
   initiatives against [[tti-ea-requirements]]'s Quotability table. Flag ANY claim that
   could only be known from an internal source (the employee Q&A town hall) rather
   than something said directly to Julian or published externally. This is the
   sharpest possible FATAL, because it would expose Julian as holding material through
   an undisclosed channel.

LOCKED DECISIONS - do not recommend reversing these
The following were decided by Julian and are not open:
   - No break clause. Once committed it is 12 months.
   - The 6-month option is closed, not offered.
   - The fee is not anchored above HK$2.50M (a higher ask invites benchmarking
     exercises that cost weeks against a live deadline).
   - "I'll work on your initiatives within the context of enterprise architecture"
     is the organising message.
Do NOT propose alternatives to these. However, if a locked decision creates a fatal
weakness in the document, flag it in a separate section headed "Locked-decision
risk" - describing the exposure and how to MITIGATE it within the lock, never by
reversing it.

OUTPUT
Write to a NEW file:
   wiki/career/tti/_wip/tti-ty-engagement-proposal-codex-review-2026-08-08.md

Do NOT modify the source document. Do not add cross-references to the source
document. All review output lives in the review file only.

Structure the review as:
   1. Ty's 60-second reaction - what he actually thinks, in his voice, first pass.
   2. Fix verification - for EACH of the 8 findings from the 7 Aug review (1 FATAL,
      7 SERIOUS), state whether it is: RESOLVED / PARTIALLY RESOLVED / NOT RESOLVED /
      REGRESSED (fixed then broken by a later edit). Be specific about what changed.
   3. New findings - ranked FATAL / SERIOUS / MINOR, covering the eight attack points
      above and anything else found reading the current document cold.
      FATAL = the document fails or the deal dies on this.
      SERIOUS = materially weakens it but survivable.
      MINOR = polish.
      For each: what is wrong, why it matters to THIS buyer, and the specific fix.
   4. Locked-decision risk (per above).
   5. The single change that most improves the odds of a yes.
   6. Verdict: send as-is / send with the FATAL fixes / do not send.

The stopping condition is NO FATAL FINDINGS. Be hard about what earns that label -
inflating a SERIOUS to a FATAL wastes time Julian does not have before Monday, and
softening a real FATAL costs him the engagement.
```

## Design notes

- **This is explicitly a re-review, not a fresh one** - Codex is told to read the prior review first and verify each finding's status (resolved / partial / not resolved / regressed), which catches the specific failure mode of a fix that looks complete but isn't, or a later edit that quietly undid an earlier fix.
- **Attack point 8 (internal-sourced material) is the highest-value addition.** The proposal was caught twice today citing employee-Q&A material as if it were known information - once with the global P&L platform, once with the IT cost-leverage line. Both were fixed, but a fresh independent check is cheap insurance given how easy that mistake is to make again while editing.
- **Attack point 4 (the judgement/authority paragraph) is new and untested** - it was added in this session after the 7 Aug review and has not been adversarially checked at all.

## Related
- [[tti-ty-engagement-proposal]] - the document under review
- [[tti-ty-proposal]] - the deliverable, its completion criteria and stopping condition
- [[tti-ty-engagement-proposal-codex-review-2026-08-07]] - the first-round review this one verifies
- [[tti-ea-requirements]] - the Quotability table attack point 8 checks against
- [[tti-h1-2026-results-talking-points]] - source for the new financial material
