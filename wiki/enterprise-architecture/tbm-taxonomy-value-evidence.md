---
type: reference
tags: [enterprise-architecture, cost-management, tbm, evidence]
created: 2026-08-09
source: Perplexity research pasted by Julian 9 Aug 2026, validated by Fable same day
---

# TBM Taxonomy: When It Produces Savings and When It Becomes Shelf-Ware

## What this is, and why it exists

**What it is:** the evidence base on whether agreeing a TBM cost taxonomy actually produces savings, or just produces an artifact. Case results on one side, documented failure modes on the other, and the pattern separating them.

**Why it was created (9 Aug 2026):** Julian was designing the cost-transparency capability in the TTI Ty proposal and named two fears - a taxonomy that never gets agreed, and a taxonomy nobody uses. This research validated that both are the documented failure modes, and that his lightweight four-step design already encodes the mitigations.

**How it is used:** consulted when designing or defending any cost-transparency engagement. The case-study numbers are vendor-published and are **evidence for design decisions, never quotable savings promises** to a client.

## Key Takeaways

- **The taxonomy is an enabling step, not a deliverable.** It saves nothing by itself; savings come from the decisions its transparency makes possible (kill duplicate spend, renegotiate, decommission).
- **The mechanism is standardisation, not analysis** - a shared classification (like GAAP for IT cost) that makes three previously-contested activities possible: finding shadow/unclassified spend, benchmarking against peers, and capability-to-cost decommission decisions.
- **The two documented failure modes:** (1) taxonomy never agreed - stalls in negotiation without a pre-agreed operating model between Finance and IT; (2) taxonomy never used - "an artifact of governance aspiration" with no allocation model, decision-owner or review cadence attached.
- **The success pattern (all four together):** an allocation model mapping GL data through to applications and consumers; an agreed operating model defining decision ownership *before* rollout; a specific savings target with a review cadence; named expert data owners who can defend the numbers when challenged.
- **Scope it as step one of a named savings exercise, never as a standalone artifact.** And keep it light: a handful of agreed categories and a directionally-right view beat a six-month modelling exercise that exhausts sponsorship before the first number appears.

## Case evidence (vendor-published - design evidence, not quotable promises)

| Organisation | Result | Mechanism |
|---|---|---|
| Bank of Ireland | 137 applications decommissioned, ~€3M/yr run cost, within 2 years | Capability-to-cost view identified decommission candidates |
| MassMutual | ~$75M eliminated in under 100 days (divestiture) | Taxonomy-driven data exposed direct and stranded IT costs |
| National Grid | ~$47M year-one savings against a $100M 3-year target | Standard cost categories enabled peer benchmarking; ~130 named optimisations tracked against the target |
| Washington State | "Undefined" IT spend cut from 15% to 5% | First-time mapping of GL costs into standard categories; data used to defend budgets to the legislature |
| US SBA | $20-30M shadow IT identified early | Same first-time GL mapping effect |

**Sourcing caveat:** all five are Apptio / TBM Council customer stories - real organisations, marketing channel. Directionally credible, not independently audited.

## The counter-evidence (stronger sourcing than the successes)

- **GAO audit of mandated federal TBM adoption:** after years, 15 of 26 agencies had no implementation plan, 18 had no reliable allocation methodology; agencies reported transparency benefits but **"did not identify any cost savings."** Transparency without an allocation model and a linked decision process produces reports nobody acts on. This is the strongest-sourced finding in the whole evidence base.
- **Practitioner analyses (2026):** TBM friction is usually not political resistance but the absence of a pre-agreed operating model - transparency "surfaces cost, exposes accountability, highlights trade-offs," and without agreed decision ownership that creates tension instead of clarity. TBM teams also fail when they become de facto data owners for domains they don't understand.
- **Unverified, do not repeat:** the claim that governance frameworks consume "15-30% of the annual budget they govern" came from an unknown site and is implausibly high as a general rule.

## Application at TTI (as of 9 Aug 2026)

The cost-transparency capability in [[tti-ty-engagement-proposal]] encodes the mitigations: a handful of agreed categories (not a modelling exercise), existing data (GL, cloud bills, data lake) with AI doing the categorisation, a directionally-right view both sides trust, then the decision conversation - with month 1's measured baseline as the decision-attachment. The call-script guardrails live in [[tti-ty-call-script]] § Notes.

## Related
- [[tbm-vs-finops]] - the TBM/FinOps distinction and relationship
- [[perplexity-defensible-ea-benefits]] - the parallel evidence base on CFO-defensible EA metrics (leading/lagging split)
- [[tti-ty-engagement-proposal]] - the proposal this research shaped
