---
type: reference
tags: [career, tti, ea, benefits-critique, external-research]
status: static
created: 2026-08-09
source: Perplexity research report, uploaded by Julian
---

# Perplexity: Defensible EA Benefits and CFO-Ready OKRs

**What this is:** a third-party research report (produced via Perplexity) that critiques the five value-levers in [[tti-ty-engagement-proposal]] against TOGAF's ADM methodology and Enterprise Architecture practitioner-forum consensus (Reddit, LinkedIn, Larkinized, Gartner community), then proposes an alternative benefits structure built on leading/lagging indicator separation and quarterly OKRs.

**Why it was created:** Julian commissioned it on 9 Aug 2026 to pressure-test the proposal's lever table before the Ty call, from an angle the internal review rounds hadn't covered: whether each claimed benefit is something the architect personally controls and can be held accountable for, versus something that depends on other people acting.

**How it is used:** Reference input only - it is not itself sent to TTI. Its core argument and the disposition Julian and I reached on it are logged in [[tti-ea-governance-value]] / [[tti-ty-engagement-proposal]] as of 9 Aug.

---

## Core argument

A CFO paying US$300k for an EA hire wants outcomes traceable to decisions the architect actually controls. Practitioner forums consistently report that EA's link to results "is not always obvious" (only 26% of orgs say EA delivers strategic benefit), and Gartner's own community says it is "very difficult to attribute" changes in shareholder value, NPS or TCO to EA specifically - the recommendation is to measure things directly caused by architecture work instead (e.g. exemptions from standards, review coverage).

**The critique of the current five levers:** four of the five describe *conditions that enable value* (a capability map, an assurance process, a reference architecture) rather than *outcomes the architect owns*. A CFO will ask "what if the map gets built and nobody kills a project?" The fifth (procurement leverage) is the most honest, because it already hands the benefit to Procurement rather than claiming it.

| Existing lever | Why a CFO pushes back | What the report recommends instead |
|---|---|---|
| Strategic alignment (capability map) | No baseline, target, or named owner of the kill/defer call | Own the decision log, not the map |
| Portfolio duplication (multiple ERPs) | True but unquantified for TTI specifically | A capability-application matrix that names $ - one capital-goods manufacturer found $50-190M/yr this way |
| Decision latency = "direct NPV loss" | Asserted, no discount rate or benefit stream | Track median time-to-decision - measurable, architect-owned |
| Risk control (independent assurance) | Conflates a process the architect runs with an outcome (fewer overruns) that depends on programme teams complying | Own the review coverage rate, not the overrun outcome |
| Procurement leverage | Already honest - hands the benefit to Procurement | Keep as-is; frame explicitly as EA-owned input feeding a Procurement-owned KPI |

**TOGAF's own answer:** Phase A requires a formal value proposition, KPIs and business case *per initiative* before a vision is approved; Phase E requires cost/benefit/risk estimates per named project. TOGAF does not sanction a single reference architecture with unattached benefit narrative - it wants a business case per candidate initiative.

**Three recurring forum failure patterns:** (1) EA's value takes years to show, so choose metrics with data available inside 90 days; (2) vanity/input metrics ("map delivered", "ARB meetings held") erode trust without a downstream decision attached; (3) CFOs fund EA differently by maturity stage - a low-maturity org (TTI, standing up EA from scratch) needs Year-1 OKRs phrased in cost/cash terms, proven via a scoped pilot, not maturity-model language.

**Recommended reframe:** split each lever into an architect-owned *leading* deliverable (built by the architect, inspectable at quarter-end) and a business-owned *lagging* outcome (tracked, never promised) - e.g. "capability-application-cost matrix delivered" (owned) vs. "$ savings identified for FY27 budget cycle" (lagging, business decides to act).

**Proposed structure for a $300k/12-month engagement:** four Objectives with quarterly Key Results - (1) stand up ARB governance with a time-to-decision baseline, (2) deliver a capability/application duplication register with named $ figures, (3) one fully TOGAF-rigor costed business case with a scoped single-plant pilot ask, (4) a reference architecture that reduces vendor variants for Procurement - plus three 90-day quick wins (pilot register for one business unit, baseline time-to-decision early, name the three largest duplicate-spend items in month one).

**Evidence base cited for the ERP/portfolio-duplication number:** ISG capital-goods case ($50-190M/yr, from the matrix, not the map's existence); Thai Union five-year ERP consolidation; Hitachi 80+ ERP instances into one (five-year migration); two unnamed PE-backed manufacturer cases ($10M inventory reduction / $2M working-capital release from consolidated visibility).

## Full text

The complete report, including the reference list (17 sources), is preserved in the uploaded PDF: `Defensible EA Benefits and CFO-Ready OKRs — Manufacturing Group Business Case.pdf`. This wiki article is a faithful compression of its argument and tables for quick reference; consult the PDF directly for exact footnote numbers if a claim needs re-verification.

## Related
- [[tti-ty-engagement-proposal]] - the document this report critiques
- [[tti-ea-governance-value]] - the argument bank; disposition on this critique logged there
- [[tti-ty-proposal-sources]] - existing source discipline this report's own standard (attribute every claim to an owner) reinforces
