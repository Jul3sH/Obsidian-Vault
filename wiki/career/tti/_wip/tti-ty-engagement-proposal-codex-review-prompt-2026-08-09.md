---
type: review-prompt
tags: [career, tti, review, adversarial, codex]
status: active
created: 2026-08-09
reviewer: Codex
target: tti-ty-engagement-proposal
output: tti-ty-engagement-proposal-codex-review-2026-08-09
supersedes-review: tti-ty-engagement-proposal-codex-review-2026-08-08
---

# Codex Adversarial Review Prompt - TTI Ty Engagement Proposal (round 3)

> **Purpose:** the document was substantially rewritten on 9 Aug in Julian's own
> editing pass, AFTER both prior reviews closed. The banner's "no open FATAL findings"
> belongs to the pre-rewrite version. This round reviews the revised document fresh,
> and verifies nothing the first two rounds fixed has regressed. **Process for this
> round: Codex reviews first; Fable then adjudicates each Codex finding before any fix
> is applied** (same adjudication pattern as the 9 Aug Perplexity assessment). Copy
> everything inside the fence below into Codex.

```
You are conducting a THIRD adversarial review of a document that has changed
substantially since you last saw it. Read these files first, in this order.

VAULT ROOT: /Users/julianhart/Obsidian Vault

1. wiki/ai-os/system-design/generic/multi-agent-protocol.md
   Your role, output file naming, handoff discipline. Read in full before starting.

2. THE TWO PRIOR REVIEWS (read before the document itself):
   wiki/career/tti/_wip/tti-ty-engagement-proposal-codex-review-2026-08-07.md
   wiki/career/tti/_wip/tti-ty-engagement-proposal-codex-review-2026-08-08.md
   Round 1 found one FATAL (month 1 read as discovery, so the buyer committed before
   the value case existed) and seven SERIOUS. Round 2's FATAL was later verified as a
   false positive (the procurement quote is public); its six SERIOUS and three MINOR
   were applied. All fixes landed on a version that has since been heavily rewritten -
   YOUR JOB includes checking the fixes survived the rewrite, not assuming they did.

3. THE DOCUMENT UNDER REVIEW (v4, rewritten 9 Aug on Julian's own editing pass):
   wiki/career/tti/_wip/tti-ty-engagement-proposal.md

4. THE SOURCES FILE (NEW since round 2 - use it as your verification layer):
   wiki/career/tti/_wip/tti-ty-proposal-sources.md
   Every factual claim with its primary source, verbatim wording and quotability tag.
   Cross-check the document against it BOTH ways: (a) any claim in the document with
   no row here is an unsourced claim - flag it; (b) any row marked "removed from the
   proposal" that has crept back in is a regression - flag it. Note S9 and S10: Kari
   is a private conversation and is deliberately cited NOWHERE in the document.

5. SUPPORTING CONTEXT (read all):
   wiki/career/tti/_wip/tti-ea-requirements.md
       - The Quotability table. Check every substantive claim about TTI against it.
         Anything only knowable from an INTERNAL source (employee town hall) is the
         sharpest possible FATAL. The "wherever the group is standardising how it
         reads cost and margin" sentence is a deliberate conditional fishing line -
         verify it asserts no internal knowledge as written.
   wiki/career/tti/_wip/tti-h1-2026-results-talking-points.md
       - H1 2026 figures the proposal cites (SG&A 173bps etc.). Verify usage.
   wiki/career/independent-consulting-pricing.md
       - The rate basis. NOTE: the fee is now US$299,563 (HK$2,336,594), revised DOWN
         on 9 Aug from the US$320,644 you saw in round 2. Locked, in both directions.
   wiki/career/tti/_wip/tti-engagement-strategy.md
       - Political dynamics, including the Tony Chung risk.
   wiki/career/tti/_wip/tti-ty-call-script.md
       - What Julian SAYS on the call: holding lines and spoken-only material
         (the honest-gap sentence, the stuck-decision play, the no-off-ramp answer,
         the six-month per-month cost reason). Read it so you know what exists as
         spoken reserve - but evaluate the printed document on its own two feet.
   wiki/deliverables/tti-ty-proposal.md
       - The deliverable definition and stopping condition. NOTE: its completion
         criteria still describe the OLD design (US$320,644 fee, month 1 as a
         discovery audit) - the wiki knows this is stale; do not treat the mismatch
         itself as a finding, but DO use its Definition of Done ("no claim Julian
         would have to walk back under questioning") as your standard.

WHAT CHANGED ON 9 AUG (so you review the deltas hardest - all of this is post-review
material with no adversarial pass on it):
   a. The lever table: rows renamed to capabilities (Capability mapping, Portfolio
      rationalisation, Decision rights, Design assurance, Vendor standardisation),
      each now carrying an architect-owned metric ("what you measure me against")
      and an explicit attribution split (which numbers are Julian's, which are TTI's).
   b. A new "Scope: three capabilities, one engagement" section: 1. the architecture
      capability (TOGAF Preliminary Phase, six bullets), 2. cost transparency (TBM
      strategic/top-down vs FinOps real-time/operational; principles-not-framework;
      a four-step lightweight approach; metric = share of spend categorised),
      3. Gen AI skills distribution (outside-in "pockets" observation; skills
      evaluated, endorsed, published; per-skill before/after measurement).
   c. Month 1 redesigned to THREE deliverables, one per capability - an architecture
      capability baseline (incl. which forums hold which decisions and current
      clearance times), cost transparency started, Gen AI skills framework drafted.
      The live cross-region decision was REMOVED as a written deliverable (it is now
      deliberately unwritten overdelivery, kept alive verbally). The months 2-12
      plan was REMOVED from month 1 (no plan before target state and gap analysis).
   d. Months 2-12 reframed as not-greenfield: baseline, target state with
      stakeholders, gap analysis, candidate roadmap, delivered through a standard
      delivery framework.
   e. Removals: the NPV-of-delay claim, the WACC re-run offer, all Kari citations,
      the honest-gap sentence (spoken-only now), the six-month fixed-cost clause,
      the standalone overrun paragraph, the "twelve years" flag (settled at 12,
      now back in writing safely).
   f. "Where I've done this before" rebuilt as a precedent per capability: BG Group
      design authority; +20% right-first-time across US$60M+ of assured solutions;
      cost models throughout career; twelve years of service design.
   g. The judgement/authority defence split into two separate paragraphs.

ROLE
Adopt the persona of Ty Staviski, Deputy CFO of Techtronic Industries (US$15.3bn
revenue), reading this cold on a Monday after travel. Numerate, busy, commercially
sceptical; you did not ask for an enterprise architect - you asked what this person
would do and what it costs. Treat "architecture" as an unproven category until the
document earns it. One calibration you should know and weigh honestly: this
engagement is sponsored by Stephan Pudwill and Julian is personally known to the
family - you are sceptical, but you are not hostile procurement.

SITUATION
Julian Hart, external, introduced through the Vice-Chairman's family. No delivery
track record inside TTI. Asking for a 12-month committed engagement at US$299,563
with no break clause. Needs a decision in roughly 24 hours. One phone call.

WHAT TO ATTACK - be specific, not general

1. THE CENTRAL QUESTION OF THIS ROUND: month 1 is now a baseline plus two "first
   cuts", with no live decision demonstrated. The heading still claims "execution,
   not a study." Round 1's FATAL was precisely that month 1 read as discovery. Has
   the rewrite regressed to it? Weigh honestly BOTH the design intent (every item is
   an artefact Julian controls - promise the floor, overdeliver the ceiling; the
   stuck-decision play still exists verbally) AND the sceptical read ("I'm paying
   US$300k committed and in 30 days I get three documents"). If you judge it
   regressed, say what the minimum written change is that fixes it WITHOUT
   reinstating an outcome Julian cannot control.
2. THE METRICATED LEVER TABLE. Are the four metrics (portfolio coverage,
   time-to-decision, assurance coverage, variant count) genuinely architect-owned
   leading indicators, or does any smuggle in a dependency on others? Does "what you
   measure me against" language anywhere overcommit? Does the Capability mapping
   row's "regional preferences get pushed through on the seniority of their sponsor"
   hand Tony Chung or the regional directors ammunition?
3. THE SCOPE SECTION. Does "three capabilities, one engagement" hold together under
   the organising message, or does it read as three parallel programmes - i.e. the
   "new function competing for sponsorship" the opening disclaims? Are the TOGAF
   Preliminary Phase bullets a seniority signal or jargon load for a CFO? Is
   anything in the six bullets a commitment Julian could be held to that he should
   not be?
4. COST TRANSPARENCY. Is "TBM strategic/top-down, FinOps real-time/operational"
   defensible if Ty knows the field? Does "directionally right, not perfect"
   strengthen (pragmatism) or weaken (imprecision) with a numerate CFO? Does the
   four-step approach with "Gen AI doing the heavy lifting" survive scrutiny?
5. GEN AI SKILLS DISTRIBUTION. "From the outside I can see many pockets of AI
   initiative across TTI" - is the outside-in basis safe under "how do you know
   that?" (sources file S13 says yes - verify you agree). Does evaluate-endorse-
   publish read as substantive or as a poster? Does avoiding the word "governance"
   (deliberate - security's turf) leave the paragraph without a control story?
6. THE HURDLE MECHANICS. The measurement now completes "as the first numbers land"
   (possibly month 2). Is the hurdle section's language consistent with that
   everywhere? Is the breakeven arithmetic still right at US$299,563 (annuity factor
   2.2607, benefits years 2-4 at 10%)? Check independently.
7. WHAT CAN'T BE EVIDENCED. Every claim that collapses under "show me": the +20%
   right-first-time, the cost-models claim, the twelve years, the BG Group numbers.
   The printed document no longer states the honest gap (no group-level charter
   held) - does its absence weaken credibility on the page, or was printing it
   always a self-wound?
8. POLITICAL EXPOSURE. Tony Chung, regional directors, the security team (Gen AI
   turf), Brian Pivar (enterprise data/AI). Does anything here read as a land grab
   or hand a detractor a line? Check "What this is not" still covers the widened
   three-capability scope.
9. INTERNAL-SOURCED MATERIAL. Full quotability sweep as in round 2. The two prior
   catches were both fixed; editing pressure makes re-introduction easy.

LOCKED DECISIONS - do not recommend reversing these
   - No break clause. Once committed it is 12 months.
   - The 6-month option is closed, not offered.
   - The fee is US$299,563, locked in BOTH directions (revised down 9 Aug to sit
     near Tony Chung's band; at this figure headroom is HK$4,421, effectively zero).
   - Never claim "market rate"; the basis is the prior Global Head salary.
   - The organising message: "I'll work on your initiatives within the context of
     enterprise architecture."
   - Kari is never cited or quoted in the outbound document.
   - Month-1 deliverables are deliberately artefacts within Julian's sole control;
     the live stuck decision is deliberately unwritten overdelivery.
If a locked decision creates a fatal weakness, flag it under a separate "Locked-
decision risk" section - describe the exposure and how to MITIGATE within the lock,
never by reversing it.

OUTPUT
Write to a NEW file:
   wiki/career/tti/_wip/tti-ty-engagement-proposal-codex-review-2026-08-09.md

Do NOT modify the source document, the sources file, or the call script. No
cross-references from source to review. All output in the review file only.

Structure:
   1. Ty's 60-second reaction - in his voice, first pass, cold.
   2. Regression check - for round 1's FATAL and the applied round-2 findings:
      SURVIVED THE REWRITE / REGRESSED / NO LONGER APPLICABLE (with one line why).
   3. New findings on the 9 Aug material - ranked FATAL / SERIOUS / MINOR, covering
      the nine attack points and anything else found reading cold. For each: what is
      wrong, why it matters to THIS buyer, and the specific fix.
      FATAL = the document fails or the deal dies on this.
      SERIOUS = materially weakens it but survivable.
      MINOR = polish.
   4. Locked-decision risk.
   5. The single change that most improves the odds of a yes.
   6. Verdict: send as-is / send with the FATAL fixes / do not send.

The stopping condition is NO FATAL FINDINGS. Be hard about what earns that label -
inflating a SERIOUS wastes hours Julian does not have before Monday; softening a
real FATAL costs him the engagement. Your findings will be independently
adjudicated by a second model before any fix is applied, so precision beats volume.
```

## Design notes

- **Attack point 1 is the round's centre of gravity.** The stuck-decision deliverable was round 1's FATAL fix, and Julian removed it today on a considered trade (artefacts he controls beat outcomes he doesn't; the political context is a sponsored entry). Codex is told the design intent AND told to test the sceptical read - and, if it finds regression, to propose a fix that respects the locked artefact-only principle rather than reinstating the old item.
- **The sources file is new leverage for this round** - round 2 had no verification layer; now every claim can be checked both directions (unsourced claims in, removed claims creeping back).
- **The Ty persona is calibrated, not hostile** - Julian's 9 Aug read (Stephan-sponsored entry, effectively an FTE) is given to Codex explicitly, so findings are priced against the real buyer rather than an imagined procurement adversary. That calibration note exists in [[tti-ty-call-script]] § Notes.
- **Process:** Codex writes the review file; Julian brings it back to Fable, who adjudicates each finding (CONFIRMED / REFUTED / PARTIAL, with reasoning) before anything is applied - the same two-model pattern that caught round 2's FATAL as a false positive.

## Related
- [[tti-ty-engagement-proposal]] - the document under review (v4)
- [[tti-ty-proposal-sources]] - the claim-verification layer
- [[tti-ty-call-script]] - spoken-reserve material and the 9 Aug calibration note
- [[tti-ty-engagement-proposal-codex-review-2026-08-07]] · [[tti-ty-engagement-proposal-codex-review-2026-08-08]] - the prior rounds this one verifies
- [[tti-ty-proposal]] - deliverable definition and stopping condition
