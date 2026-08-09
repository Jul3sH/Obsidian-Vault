---
type: reference
tags: [career, tti, ea, benefits-critique, external-research]
status: static
created: 2026-08-09
source: Perplexity research report "Defensible EA Benefits and CFO-Ready OKRs - Manufacturing Group Business Case", uploaded by Julian 9 Aug 2026
---

# Perplexity: Defensible EA Benefits and CFO-Ready OKRs

## What this is, and why it exists

**What it is:** the full text of a third-party research report (produced via Perplexity) that critiques the five cost-reduction levers in [[tti-ty-engagement-proposal]] against TOGAF's ADM methodology and Enterprise Architecture practitioner-forum consensus, then proposes an alternative benefits structure built on leading/lagging indicator separation and quarterly OKRs.

**Why it was created (9 Aug 2026):** Julian commissioned it to pressure-test the proposal before the Ty Staviski call on 10 Aug, from an angle the two Codex adversarial rounds had not covered: whether each claimed benefit is something the architect personally controls and can be held accountable for, versus something that depends on other people acting.

**How it is used:** reference input only, `send: NEVER` in effect - it is not shown to TTI, and **none of its dollar figures are safe to quote to Ty** (see the disposition below). Julian's decision on the critique is recorded in [[tti-role]]'s status log for 9 Aug.

> **⚠ As of 9 Aug 2026 - disposition after review.** A Fable review of this report against the proposal found the critique **lands cleanly on only one lever (Strategic alignment)** and misfires on Decision latency and Portfolio duplication, because the proposal already answers those through its breakeven-hurdle framing and Month 1 deliverables. **The four-Objective OKR structure below was rejected for the 10 Aug call** - it commits to named-dollar registers, a scoped pilot and a variant-reduction target before Ty has agreed anything, which reopens the Round 1 FATAL; its correct home is the months 2-12 sequenced plan, as an *output* of Month 1. **All case-study dollar figures in this report are non-TTI analogues with no revenue normalisation and must not be spoken to a CFO.** No proposal edits were made as a result of this report.

> **📄 Source note.** The original PDF is not stored in the vault. This file is the record. The body below is the report's full text, transcribed; only the reference footnote markers (superscript numbers, which did not survive PDF extraction cleanly) have been dropped, with the numbered reference list preserved in full at the end.

---

## Purpose and Framing

A CFO paying $300,000 for one year of an Enterprise Architecture (EA) hire wants outcomes that are traceable to decisions the architect actually controls, not to benefits that depend on other people executing well. Practitioner forums are blunt about where EA overclaims: architects "produce principles, models, and roadmaps, but the link to immediate business results (revenue, cost savings, speed to market) is not always obvious," and a 2023 industry survey found only 26% of organizations agreed their EA practice delivered strategic benefits like agility. Gartner's own peer community echoes this: practitioners admit "it is very difficult to attribute changes" in shareholder value, NPS, or TCO to EA specifically, and recommend instead measuring things directly caused by architecture work, such as exemptions from principles or standards violations. This report uses that lens throughout: TOGAF's formal methodology for grounding the case, forum-sourced criticism for stress-testing it, and case-study evidence for calibrating what a single architect can realistically move in twelve months.

## Critique of the Current Report's Five Benefits

The existing draft leans heavily on narrative logic (a capability map "makes visible" what wasn't visible; independent assurance "separates two jobs") without stating what a CFO can hold the architect accountable for. Reviewed against TOGAF and forum experience, each claim needs tightening.

| Existing claim | Why a CFO will push back | What forums say instead |
|---|---|---|
| **Strategic alignment via capability map** | No baseline, no target, no owner of the "kill or defer" decision, sounds like documentation, not governance | EA only creates CFO value "when it directly supports capital allocation... what to invest in, what to stop, what to simplify". The deliverable must be a decision log, not a map. |
| **Portfolio duplication (multiple ERPs)** | True and well-evidenced elsewhere, but the report doesn't quantify TTI's own duplication or attach a savings range | A capital goods manufacturer with 4,000+ apps found $50-190M/year in potential savings once ISG built a capability-application matrix. The number came from the matrix, not from the map's existence. Reddit practitioners confirm the mechanism: "capability maps will give you the relationships between capabilities and people/process/technology... you'll be able to identify redundant applications and gaps". |
| **Decision latency = "direct NPV loss"** | Correct in principle but unmeasured; NPV-of-delay claims without a discount rate and a deferred benefit stream are assertions, not numbers | Larkinized's practitioner-derived KPI set explicitly recommends "median time-to-decision" as a governance KPI precisely because latency is measurable and attributable to the architect running the review board. |
| **Risk control via independent assurance** | Conflates a governance process (architect can build and run it) with an outcome (fewer overruns, which depends on programme teams complying) | Same LinkedIn/CFO research: "if architecture does not influence what to invest in, what to stop, and what to simplify, it loses its purpose". The architect should own the review coverage rate, not the overrun outcome. |
| **Procurement leverage** | Explicitly hands the benefit to Procurement ("negotiating stays procurement's job"). This is the most honest of the five, but as written it isn't an EA-owned OKR at all | Reference architecture that reduces variant count is the causal, EA-owned input; the negotiated saving is a lagging Procurement KPI, not something to claim as an EA result. |

The common flaw: four of the five benefits describe *conditions that make value possible* rather than *actions the architect performs and outputs the architect owns*. A CFO signing a $300k check will ask "what if the capability map is built and nobody kills a project?" That has already happened to other EA functions, which is why over 20 years of practitioner discussion keeps landing on the same complaint: EA's link to results "is not always obvious".

## What TOGAF Actually Prescribes for the Business Case

TOGAF's ADM does not leave the business case to narrative. Phase A (Architecture Vision) explicitly requires the architect to "Define the Target Architecture Value Propositions and KPIs," "develop the business case for the architectures and changes required," and "produce the value proposition for each stakeholder grouping" before the vision is approved. This is paired with a Business Transformation Readiness Assessment, which scores the organization's readiness factors and feeds directly into the Implementation and Migration Plan (Phases E/F) so that risk is priced in before work starts. TOGAF templates for the Architecture Vision phase include a formal "Strategic Alignment" section (current-state assessment, future-state assessment, gap analysis) and a Statement of Architecture Work that must be signed off by sponsors. Phase E (Opportunities & Solutions) requires the architect to "estimate the cost, benefits, and risk for each project" and to "secure stakeholder agreement" before work packages are prioritized. In other words, TOGAF's own method insists that benefit claims be attached to named projects and owners, not a standalone capability map. The practical implication for TTI: the deliverable that satisfies both TOGAF discipline and CFO scrutiny is a value-proposition/business-case document per candidate initiative (per TOGAF Phase A/E), not a single group reference architecture with unattached benefit narrative.

## Forum Consensus on What Is Hard to Justify

Cross-referencing multiple independent threads and LinkedIn posts converges on three recurring failure patterns, which should shape what OKRs are proposed and which are avoided.

- **Time lag kills credibility.** "EA's value takes years to show, making ROI difficult to prove compared to hands-on technical work". This is the single most repeated complaint across r/EnterpriseArchitect threads. The fix practitioners converge on is choosing metrics with data available inside 90 days, not multi-year capability-maturity uplift.
- **Vanity/input metrics erode trust.** Practitioner-written guidance explicitly warns against "vanity metrics: total Visio diagrams, ARB meetings held, principles published without adoption evidence". Anything phrased as "capability map delivered" without a downstream decision attached will read as vanity to a CFO who has seen this before.
- **CFOs fund EA differently by maturity stage.** A CFO-facing LinkedIn thread from 2026 states plainly: "In low-maturity EA environments, CFOs see EA as cost... In high-maturity EA environments, CFOs see the value of EA; but only when architects speak in financial terms," and reports EA programmes have been "stalled or defunded simply because they failed to adapt their communication style". Since TTI is standing up EA from a low base, Year 1 OKRs must be phrased in cost/cash terms, not maturity-model terms.
- **What does work: pilots and phased proof before asking for the big commitment.** A practitioner diary of pitching EA investment to a C-suite found that a scoped pilot on one non-critical system, with a before/after comparison, was what converted a skeptical CFO and COO. "These early successes are critical in building momentum and trust."
- **The metrics that survive CFO scrutiny are inputs the architect visibly controls.** Larkinized's practitioner-sourced KPI framework recommends splitting leading indicators (review throughput, standards adoption, median time-to-decision, architect-controlled) from lagging indicators (realized savings, incident reduction, influenced by architect but delivered by others), and reviewing quarterly whether the leading indicators are actually moving the lagging ones.

## Evidence Base for Quantifying ERP/Portfolio Duplication

> **⚠ None of the figures in this section are TTI's, and none are revenue-normalised. Do not speak them to Ty.**

Because the existing report's strongest, most concrete claim is portfolio duplication across ERPs, it is worth anchoring the size of that opportunity in real manufacturing cases rather than leaving it as assertion. A capital-goods manufacturer with a portfolio that had grown unchecked to 4,000+ applications had ISG identify $50-190 million/year in potential savings, but crucially the number came from an assessment of the application repository against capability, not from the mere existence of a capability model. Thai Union's five-year ERP consolidation across a multi-brand manufacturing group reduced its footprint toward a target of ~100 applications from 250+, and reported measurable SG&A and inventory control gains, but this was a five-year programme, not a one-year deliverable. Hitachi's case of consolidating 80+ ERP instances into one for a decentralized manufacturer took a full five-year migration window with a year of assessment work up front. Multi-ERP PE-backed manufacturers report faster wins when the first move is data unification and a capability-application matrix rather than a system rip-and-replace: one six-ERP, ten-facility manufacturer achieved "immediate" supplier-term savings once procurement was viewed as one portfolio, and another delivered a $10M inventory reduction and $2M working-capital release from consolidated visibility. The consistent lesson: the fast, first-year, architect-controllable step is building the capability-to-application-to-spend map and using it to surface duplicate spend and negotiate leverage; the slow, multi-year step is the actual system consolidation, which should not be promised inside a one-year OKR.

## Recommended Benefit Reframing

Each of the five original benefits is restated below as an architect-owned leading indicator paired with a business-owned lagging indicator, closing the attribution gap forums repeatedly flag.

| Theme | Architect-owned leading deliverable (Year 1, in scope) | Business-owned lagging outcome (tracked, not promised) |
|---|---|---|
| **Strategic alignment** | Capability map with every active project (>$250k) tagged to a capability and a "fund/defer/kill" recommendation logged | $ value of spend redirected or stopped by the investment committee |
| **Portfolio duplication** | Capability-application-cost matrix covering all ERP/finance/CRM instances group-wide, with duplicate-spend heat map | $ savings identified for FY27 budget cycle (business decides to act) |
| **Decision latency** | Architecture Review Board stood up, charter signed, median time-to-decision baselined and tracked monthly | Reduction in cross-region escalation volume to group committee |
| **Risk control** | Independent design-assurance checkpoint added to the stage-gate process for all Tier-1 programmes, review coverage % tracked | Reduction in late re-cuts/overruns on assured programmes vs. historical baseline |
| **Procurement leverage** | Reference architecture published defining "standard" vendor/platform per capability, variant count baselined and reduced | $ negotiated savings claimed by Procurement, EA cited as enabler |

## Proposed OKRs for a $300,000 / 12-Month Engagement

> **⚠ Rejected for the 10 Aug call. See the disposition banner at the top. Reassigned to the months 2-12 sequenced plan as an output of Month 1, not an input to the pitch.**

The OKRs below are split deliberately: quarterly Key Results the architect can be judged on personally (matching the "within my control" requirement), and 12-month structural Objectives that establish the capability without over-promising benefit realization that depends on others. This mirrors TOGAF Phase A/E's requirement to attach cost/benefit/risk to named projects, and the forum-derived principle of separating leading from lagging metrics.

**Objective 1 - Establish a functioning EA governance capability (owned outcome, Q1-Q2)**
- **KR1:** Architecture Review Board chartered, sponsored by CFO/CIO, and running with a documented case log within 90 days.
- **KR2:** 100% of new Tier-1 (>$500k) programme business cases pass through the ARB before funding approval by end of Q2.
- **KR3:** Median time-to-decision at ARB tracked from week 1, with a published baseline by end of Q1 and a target reduction of 30% by Q4 versus the pre-ARB escalation baseline.

**Objective 2 - Deliver a group capability and application map that exposes duplication (owned outcome, Q1-Q3)**
- **KR1:** Capability model covering top 12 group-wide business capabilities, validated with business unit heads, complete by end of Q2 (TOGAF Phase B deliverable).
- **KR2:** Every application with annual run cost >$100k mapped to a capability and a duplication/overlap flag by end of Q3.
- **KR3:** A quantified duplicate-spend register (not an estimate, a named list of overlapping systems with owner, cost, and contract end date) delivered to the CFO by end of Q3, modeled on the ISG-style assessment approach.

**Objective 3 - Produce a costed, TOGAF-compliant business case for the highest-value consolidation opportunity (owned outcome, Q3-Q4)**
- **KR1:** One candidate initiative (e.g., ERP or CRM consolidation) taken through TOGAF Phase A-E rigor, with a formal Statement of Architecture Work, value proposition, and cost/benefit/risk estimate signed off by sponsors.
- **KR2:** Business case includes a scoped pilot (one plant/BU) rather than a full-programme ask, following the pattern that converted skeptical CFOs in comparable engagements.
- **KR3:** Business case delivered to the investment committee by end of Q4, with an explicit go/no-go decision requested (success = decision made, not benefit realized within the year).

**Objective 4 - Build procurement leverage input without claiming procurement's result (owned outcome, Q2-Q4)**
- **KR1:** Reference architecture published defining the standard platform/vendor per capability for at least 3 capability domains by end of Q3.
- **KR2:** Vendor/platform variant count baselined in Q1 and reduction target (e.g., -25%) set and tracked through Q4.
- **KR3:** Joint report with Procurement each quarter showing variant reduction achieved and negotiations enabled, savings figures attributed jointly, not solely to EA.

**Quick wins (first 90 days, credibility-building, low dependency)**
- Publish the capability map and duplicate-application register for one already-troublesome business unit or region (mirrors the "pilot on a non-critical system" pattern that built trust fastest in comparable engagements).
- Baseline and publish current average time-to-decision for cross-region investment escalations, even before the ARB is fully operational. This number alone often reframes the conversation.
- Identify and name (not yet action) the three largest single duplicate-spend items found in the first month, giving the CFO an immediate, concrete "found money" list ahead of the full Q3 register.

## What Not to Promise

Given the forum evidence, avoid framing any Year 1 OKR around outcomes the architect does not control: realized cost savings from consolidation, reduced overrun rates on programmes, or improved NPS/agility scores. These are the exact claims practitioners say erode EA's credibility over time because "the burden of proof has shifted" onto architects who cannot show attribution. Frame the year instead as: governance stood up, duplication quantified, one fully costed TOGAF-rigor business case delivered, and procurement given a usable reference architecture. Four deliverables entirely within a single architect's control, each with a named artifact the CFO can inspect at quarter-end.

## References

1. *Enterprise Architecture: Ongoing Justification of Its Value* - LinkedIn. "1. Common Criticisms from Business and IT Stakeholders. Enterprise Architecture (EA) often faces skep..."
2. *KPI/OKR that are used to measure Enterprise Architecture value to...* - "What are the metrics - KPI/OKR that are used to measure Enterprise Architecture value to your Enterp..."
3. *CFOs see EA value in high-maturity environments | Vintage* - LinkedIn. "An interesting day speaking with CFOs alongside Enterprise Architecture leaders. A clear pattern is..."
4. *Applications Rationalization Assessment Identifies Millions in Savings* - "A global capital goods manufacturer's application portfolio had grown unchecked to more than 4,000 a..."
5. *Application Consolidation EA approach*
6. *How do you help organizations with overlapping systems?*
7. *What KPIs should Enterprise Architects track? | Larkinized* - "Essential KPIs for Enterprise Architects: portfolio, governance, maturity, and value metrics recommen..."
8. *Enterprise architecture governance: The ultimate guide* - N-iX. "Let's take a look at enterprise architecture governance, its simplicity in concept and complexity in..."
9. *Is EA Trying to Solve an Unsolvable Problem? : r/EnterpriseArchitect* - "Hard to measure success - EA's value takes years to show, making ROI difficult to prove compared to..."
10. *The TOGAF Standard, Version 9.2* - Governance Foundation
11. *Preliminary Phase: Framework and Principles*
12. *TOGAF Batch Lecture 21 Phase E Opportunities & Solutions Introduction + Templates for All Phases* - "In Lecture 21 of the TOGAF Training Batch, we move forward in the ADM cycle and explore Phase E - Op..."
13. *Diary Of A Chief Architect: Challenges in Influencing C-Suite Over...* - "The CFO appreciated the phased investment approach, which spreads costs over time and allows for per..."
14. *Thai Union - Building a Sustainable Business with Digital Enablers* - "Thai Union is one of the world's largest seafood processors. Their footprint across manufacturing and..."
15. *Customer Stories* - "How PE-backed manufacturers connected fragmented data and drove real business outcomes, inventory re..."
16. *[PDF] From 80+ Systems to One - A Case Study of ERP Consolidation*
17. *TOGAF ADM Phase B - Develop the Business Architecture* - Conexiam. "TOGAF ADM is the core of the TOGAF Standard. It is the only scalable universal method to develop ent..."

## Related
- [[tti-ty-engagement-proposal]] - the document this report critiques
- [[tti-ea-governance-value]] - the argument bank behind the proposal
- [[tti-ty-proposal-sources]] - the source discipline this report's own standard (attribute every claim to an owner) reinforces
- [[tti-role]] - status log entry for 9 Aug records the disposition
