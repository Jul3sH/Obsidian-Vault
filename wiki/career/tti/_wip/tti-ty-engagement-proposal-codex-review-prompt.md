---
type: review-prompt
tags: [career, tti, review, adversarial, codex]
status: active
created: 2026-08-07
reviewer: Codex
target: tti-ty-engagement-proposal
output: tti-ty-engagement-proposal-codex-review-2026-08-07
---

# Codex Adversarial Review Prompt - TTI Ty Engagement Proposal

> **Purpose:** satisfies the stopping condition on [[tti-ty-proposal]] - an independent
> adversarial pass, run by a **different model than the one that drafted the document**,
> returning no FATAL findings. Claude drafted the proposal; Codex reviews it.
> Copy everything inside the fence below into Codex.

```
You are conducting an adversarial review. Read these files first, in this order.

VAULT ROOT: /Users/julianhart/Obsidian Vault

1. wiki/ai-os/system-design/generic/multi-agent-protocol.md
   Your role, output file naming, handoff discipline, frontmatter authority levels.
   Read it in full before starting.

2. THE DOCUMENT UNDER REVIEW:
   wiki/career/tti/_wip/tti-ty-engagement-proposal.md

3. SUPPORTING CONTEXT (read all):
   wiki/career/tti/_reference/tti-2025-ar-key-initiatives.md
       - Ty Staviski's own stated targets and live initiatives. The proposal's hooks
         are drawn from here. Check they are represented accurately.
   wiki/career/independent-consulting-pricing.md
       - The rate, its basis, and why anchoring higher was rejected.
   wiki/career/tti/_wip/tti-cfo-brief.md
       - v1 of an earlier brief to the same buyer, plus the appendix recording a prior
         red-team that killed it. The failure modes it identifies (bracketed numbers,
         circular hire-first-justify-later logic, asserted-not-evidenced ownership,
         no reason to act now) MUST NOT have returned in this document. Check explicitly.
   wiki/career/tti/_wip/tti-ty-call-simulation-2026-07-19.md
       - Dry run of a conversation with the same buyer.
   wiki/career/tti/_wip/tti-engagement-strategy.md
       - Political dynamics, including the Tony Chung risk.
   wiki/deliverables/tti-ty-proposal.md
       - The deliverable definition: completion criteria, load-bearing assumptions,
         and the stopping condition this review exists to satisfy.

ROLE
Adopt the persona of Ty Staviski, Deputy CFO of Techtronic Industries (US$15.3bn
revenue), reading this cold on a Monday after travel. You are numerate, busy,
commercially sceptical, and you did not ask for an enterprise architect - you asked
what this person would do and what they cost. You have no particular belief that
enterprise architecture is valuable. Treat "architecture" as an unproven category
until the document earns it.

SITUATION
Julian Hart is an external candidate, introduced through a family relationship with
TTI's Vice-Chairman. He has no delivery track record inside TTI. He is asking for a
12-month committed engagement at US$320,644 with no break clause. He needs a decision
in roughly 24 hours. He gets one phone call to land this.

WHAT TO ATTACK - be specific, not general

1. Does it sell enterprise architecture to someone who does not already value it?
   Or does it assume the buyer accepts the premise? This is the primary test.
2. The financial case. Check the NPV arithmetic independently (stated: US$320,644 /
   2.2607 = US$141,827, where 2.2607 is the 3-year annuity factor at 10% with
   benefits in years 2-4). Is the method one a CFO would accept, or is it a
   presentation trick? Is a breakeven hurdle a legitimate substitute for a benefit
   estimate, or is it the author avoiding the hard number?
3. The "I won't quote what I haven't measured" stance. Does it read as disciplined
   honesty, or as someone who has not done the work? Argue both sides, then decide.
4. What can Julian NOT evidence? Identify every claim that would collapse under
   "give me an example of where you have done this before."
5. The 12-month commitment with no break clause. Why would a CFO commit 12 months
   to an unproven outsider? This is the sharpest objection in the document. Does it
   survive?
6. Political exposure. Tony Chung (SVP Finance APAC) has multiple technology
   directors reporting to him and is a documented probable detractor. Does anything
   here hand him ammunition?
7. The organising claim - "I'd work on your existing initiatives in an
   enterprise-architecture context." Does it survive "so what would you actually do
   on Monday morning?" Or is it a positioning line with no operational content?
8. FinOps and AI-in-workflows. Both are asserted as capabilities. Is either
   over-claimed relative to what an individual can deliver in 12 months?

LOCKED DECISIONS - do not recommend reversing these
The following were decided by Julian and are not open:
   - No break clause. Once committed it is 12 months.
   - The 6-month option is closed, not offered.
   - The fee is not anchored above HK$2.5M (a higher ask invites benchmarking
     exercises that cost weeks against a live deadline).
   - "I'll work on your initiatives within the context of enterprise architecture"
     is the organising message.
Do NOT propose alternatives to these. However, if a locked decision creates a fatal
weakness in the document, flag it in a separate section headed "Locked-decision
risk" - describing the exposure and how to MITIGATE it within the lock, never by
reversing it.

OUTPUT
Write to a NEW file:
   wiki/career/tti/_wip/tti-ty-engagement-proposal-codex-review-2026-08-07.md

Do NOT modify the source document. Do not add cross-references to the source
document. All review output lives in the review file only.

Structure the review as:
   1. Ty's 60-second reaction - what he actually thinks, in his voice, first pass.
   2. Findings ranked FATAL / SERIOUS / MINOR.
      FATAL = the document fails or the deal dies on this.
      SERIOUS = materially weakens it but survivable.
      MINOR = polish.
      For each: what is wrong, why it matters to THIS buyer, and the specific fix.
   3. Locked-decision risk (per above).
   4. The single change that most improves the odds of a yes.
   5. Verdict: send as-is / send with the FATAL fixes / do not send.

The stopping condition is NO FATAL FINDINGS. Be hard about what earns that label -
inflating a SERIOUS to a FATAL wastes a weekend Julian does not have, and softening
a real FATAL costs him the engagement.
```

## Design notes

- **FATAL / SERIOUS / MINOR and the "60-second reaction" opener are deliberate reuse** of the Fable red-team format that killed v1 of [[tti-cfo-brief]]. Same taxonomy means the two reviews are directly comparable, and the earlier one is included as required reading so its failure modes get checked for recurrence rather than rediscovered.
- **The locked-decision clause exists so the review stays useful without becoming a re-litigation.** The 12-month commitment with no break clause is the document's largest exposure; Codex must be able to name it, but must argue mitigation within the lock rather than proposing Julian reverse a decision he has made.
- **The reviewer is told Julian has no TTI track record and no delivery evidence inside the company.** Withholding that would produce a soft review.

## Related
- [[tti-ty-engagement-proposal]] - the document under review
- [[tti-ty-proposal]] - the deliverable, its completion criteria and stopping condition
- [[tti-cfo-brief]] - the earlier brief and the red-team appendix this format reuses
