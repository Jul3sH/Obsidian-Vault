---
type: prep
tags: [career, tti, prep, enterprise-architecture, conversation]
status: wip
created: 2026-07-19
updated: 2026-07-19
version: v3 (hardened against Fable round 2)
audience: Julian only (conversation prep)
send: NEVER
---

# TTI — EA Governance Value (conversation prep)

## What this is, and why it exists

**What it is:** a bank of conversation arguments that map a *capability* Julian can bring - enterprise-architecture governance, TOGAF mechanics, FinOps operating-model thinking - onto a *problem a TTI stakeholder has actually stated*. Each section is one argument, written in memorable chunks with a "say it like this" line, so it can be carried in conversation rather than read out.

**Why it was created (19 Jul 2026):** Ty described the gap unprompted on the 15 Jul call - fragmented technology leadership across Asia, too many steering committees to coordinate between the silos, needing frameworks and governance put in place. This document was built to have a hardened answer ready for the conversations that would follow, rather than composing one live in the room.

**How it is used:** Julian only. `send: NEVER` - it is not an artefact to share, and several sections would be actively damaging if they reached Tony Chung. Read §0 first for why the argument is urgent right now, then the section that matches the objection you expect. Carry the argument, don't read it out, and draw the sharpest lines into the artefact you are actually writing. The numbers-shaped distillation for a finance audience is [[tti-cfo-brief]]; the live proposal it feeds is [[tti-ty-engagement-proposal]].

## Section map — which argument answers which stated requirement

Requirement IDs refer to [[tti-ea-requirements]], the sourced verbatim log of what TTI stakeholders have actually said. **T** = Ty, **K** = Kari.

| § | The argument | Answers |
|---|---|---|
| **0a** | The SG&A Squeeze. H1 2026 SG&A growth consumed roughly two-thirds of a record gross-margin gain, so the next EBIT point has to come from structural cost - answered by the same portfolio-duplication and rework-avoidance levers argued in the proposal. This opens the whole document with why the argument is urgent right now, before §1 explains the underlying mechanism. | T9, T15 |
| **0b** | The FCF Lever. TTI raised its 2026 free cash flow target mid-year by 30%, and because free cash flow is operating cash minus capex, technology capex avoided through governance flows directly into that number - the same mechanism as §0a, pointed at a different, more recently-moved metric. | T16 |
| **0c** | The Capacity Window. New manufacturing capacity is being built in Vietnam and the Americas over the next 12-18 months, which is a forward-looking argument for embedding a standard at build time rather than retrofitting governance later. | T18 |
| **1** | TTI's technology fragmentation is the rational result of acquisition-led growth, not incompetence - the steering committees are a symptom, and the missing coordination layer is the actual cause. This section also carries a scope guard (design the capability enterprise-wide, but concentrate effort where the gap actually is) and a geography guard on how to talk about Milwaukee without it sounding like Hong Kong governing the US. | T1, T2, K1, K3 |
| **2a** | An authority argument, independent of 2b: a central function can commit to a shared platform because it spreads the risk across the whole portfolio, whereas a single region cannot justify carrying that risk alone, which is why regions default to building their own. Not about cost. | T9, T12 |
| **2b** | A cost argument, independent of 2a: this answers Kari's own admission that TTI lacks technology cost data, using TBM (not FinOps) cost transparency. It is written as a question Julian asks rather than a fact he states, so he never appears to already know about TTI's internal finance platform. | K7, T13 |
| **3** | This walks through the specific TOGAF components that kill silo behaviour - principles, the Architecture Board, reference architectures, ADM phases G and H, and architecture contracts - plus the sequencing answer for how governance starts delivering value immediately rather than after a long design phase. It also states plainly that Julian would take only the useful parts of a framework rather than impose the whole thing on TTI, which directly answers Kari's own comment on that. | T1, T3, K6 |
| **4** | This is the mandate section, and it is the load-bearing argument in the whole document: who actually charters the board's authority, how a deadlock gets broken instead of stalling forever, and how the resourcing to do the work is secured at the point of charter rather than negotiated meeting by meeting. | T3, K8 |
| **5** | This gives Ty the shape of the coordination-tax cost honestly, as an unmeasured estimate, with an explicit offer to measure the real number properly in week one rather than presenting an invented figure as fact. | T6, T8, T9 |
| **5b** | This explains why governed programmes overrun less often than ungoverned ones: the people accountable for a delivery date should not also be the people judging whether their own design is sound. It is written to be led with as a strength, not held back as a defence against Kari's comment on past overruns. | K4 |
| **6** | This draws the boundary between enterprise architecture and solution architecture, showing how the detailed technical work still gets done properly without Julian needing to claim SAP or Oracle expertise he doesn't have. | T2, K9 |
| **7** | This pre-empts the most damaging objection Julian could face - that he would just draw governance diagrams and nothing more - by arguing that AI closes the drafting gap but not the judgement gap (which decisions are sound) or the authority gap (making them stick across directors), and both remaining gaps are exactly why the role needs to sit at director level. | T2 |
| ~~**8**~~ | ~~Predictable director-hire questions~~ | **Removed 8 Aug.** Positioning/credibility answers, not arguments mapped to a requirement — moved to [[tti-story-bank]] §3. T4 and K9 reclassified below as needing no argument. |

## ✅ Requirements coverage — all closed as of 8 Aug

Full audit against [[tti-ea-requirements]]. Every stated requirement now has an argument, is out of scope by decision, or is a process/signal item needing none.

| Requirement | Status |
|---|---|
| ~~**K3**~~ Kari said the scope should be the whole enterprise, not just US/HK | **Closed, now §1's scope guard.** The resolution is to design the capability enterprise-wide but deploy effort where the gap actually is, and the same point is made explicitly in an "On scope" paragraph in [[tti-ty-engagement-proposal]]. |
| ~~**K4**~~ Kari said past leadership had been burnt by programmes that overran | **Closed, now §5b.** This was inverted from an objection to survive into an argument to lead with: assurance separates the design judgement from the delivery pressure. A hard guardrail sits alongside it against ever naming a specific programme. |
| ~~**K5**~~ Kari wanted strategic long-term gains, not quick wins | **Closed.** Month 1 in the proposal delivers proof that the mechanism works rather than a quick win, and months 2-12 are described explicitly as a structure that holds after Julian has gone. There is a standing guardrail never to say the words "quick win" on this engagement, because Kari sponsored the 12-month term on exactly that distinction. |
| ~~**K6**~~ Kari said not to shove a whole framework down people's throats | **Closed.** §3 was always making this argument, it just had not been mapped to the requirement until 8 Aug. |
| ~~**T13**~~ The global P&L platform Ty co-drives with Casey and Frank | **Closed, now §2b.** Because this is INTERNAL information from the employee Q&A, it is built as a question Julian asks rather than a fact he states, so quoting it never reveals that he holds an internal transcript. |
| ~~**T9, T15**~~ The H1 2026 SG&A/margin finding | **Closed, in §0a.** Opens the whole document with why the argument is urgent this half, before §1 explains the underlying mechanism. |
| ~~**T16**~~ The raised free cash flow target | **Closed, in §0b.** Split out from the SG&A finding on 8 Aug because it is a genuinely separate mechanism (capex avoided, not EBIT protected), not a repeat of the same point. |
| ~~**T18**~~ The Vietnam/Americas capacity expansion | **Closed, in §0c.** The only forward-looking finding of the three; full workup for all of §0 in [[tti-h1-2026-results-talking-points]]. |

### Deliberately not addressed (a decision, not an oversight)

| Requirement | Why it is left out |
|---|---|
| **T10** Ty is credited with margin expansion from factory and supply-base leverage | This is manufacturing and procurement cost, not the technology estate, and sits outside what an EA engagement can credibly influence. Reaching for it would read as Julian claiming to fix everything. |
| **T11** Net interest expense fell to 0.2% of turnover | This is treasury and capital management. There is no EA lever that touches it. |
| **T19** The effective tax rate and TTI's tax-efficiency language | This is Kari's territory, given his background in transfer pricing, not Ty's. It is held in [[tti-h1-2026-results-talking-points]] for the Kari channel rather than argued in this document. |
| **T20** The MILWAUKEE ERP conversion's "planned timing impact" | **Must never be used as evidence of an overrun** - the word TTI itself uses is "planned," and the CEO's public position is that the conversion executed flawlessly. Its only safe use, as neutral evidence that large ERP conversions have lasting financial effects, is already folded into §5b without naming it. |
| **T17** The US$500m share buyback | **Moved out of §0 on 8 Aug**, at Julian's direction: the organising rule for that section is that every finding must name a specific EA/TBM/AI capability that addresses it, and capital allocation has no such lever. Survives only as a fee-sizing aside in §0c's closing note - never as an urgency or capability claim. |

### Requirements that need no argument at all

These are process, timing, or simple signals rather than a stated need, so nothing was built for them: **T5** (an August meeting was suggested), **T7** (12 months seemed acceptable to Ty), **T14** (no offer or structure was given at the 15 Jul call), **K2** (no pushback on the EA framing), **K10** (a positive reaction to the AI/service-design pitch), and **K11 through K13** (decision timing, including the still-pending Kari reply). **J1, P1 and P2** are the overrun intel and the public record behind it; they inform §5b rather than being requirements in their own right. **T4** (the role should be HK-based) and **K9** (Kari's acknowledgement that an outsider takes time to onboard) were loosely mapped to the now-removed §8; neither needed a rebuttal argument to begin with, and both are answered, if at all, by the positioning material in [[tti-story-bank]] §3.

**One note on where AI sits.** Kari responded positively to the AI framing (K10), but the AI *value* argument lives in [[tti-ty-engagement-proposal]] and [[tti-story-bank]] §1c, not here. This document carries only §7's defensive AI line, welded to the authority clause. That is deliberate - here AI is a thing to be defended, not sold.

---

## Fable verdict summary — what was attacked, what was fixed, what is still open

> **Two adversarial passes by Fable (hostile Tony Chung role).** Read this block instead of the separate review file. Full detail: [[tti-ea-governance-value-fable-review-2026-07-19]].

### What Fable attacked (both rounds, most dangerous first)

| # | Attack | Severity | Round |
|---|--------|----------|-------|
| 1 | Mandate void: Architecture Board has no charter, no enforcement — "just another committee, with your salary" | FATAL | 1 |
| 2 | No charterer: "CFO/Ty" collapses — Frank leaving, Ty only Deputy, no exec above both regional lines named | FATAL | 2 |
| 3 | No-outvote board is a suicide clause: Tony's directors attend and never agree; no deadlock-breaker | FATAL | 2 |
| 4 | No coordination-tax number for a CFO audience that already asked for one | Serious | 1 |
| 5 | FinOps analogy inverts: no accountability number owned, centre-vs-implementation contradiction | Serious | 1 |
| 6 | AI grunt-work line hands Tony his cheapest kill: "principal + Copilot, half the cost, in my org" | Serious | 1 |
| 7 | Credibility gap at reference-architecture layer: can't arbitrate SAP/Oracle expert dispute | Serious | 1 |
| 8 | Silo diagnosis insults the room; silent on Milwaukee geography of authority | Serious | 1 |
| 9 | TOGAF sequencing gap: leading with G/H implies a target that doesn't yet exist | Serious | 1 |
| 10 | Four director-hire questions unanswered: reporting line, why-external, prior proof, 90-day plan | Serious | 1 |
| 11 | Resource starvation: floating coordinator with no line reports; Tony keeps teams "very busy" | Serious | 2 |
| 12 | Cheaper fix invited: "just cancel the committees for free" | Serious | 2 |
| 13 | "Committees retired" KPI is gameable: rename to "alignment sync" and baseline disappears | Minor | 2 |

### What was fixed (applied in v3)

| Fix | Where |
|-----|-------|
| Mandate: joint charter (Ty + group tech leadership), Frank explicitly not load-bearing | §4 |
| Deadlock-breaker: decision SLA (auto-escalate) + ratification rule (silence = consent) | §4 |
| Resourcing committed at charter, not negotiated per meeting | §4 |
| "Committees retired" defined as calendar-audited standing forum, not self-reported | §4 |
| CEO-chip fallback: Uva tier as day-to-day ratifier; CEO as rarely-used backstop, formalised later | §4 |
| FinOps reframed: risk-transfer only; role owns a named number; welded to charter executive's decision | §2a |
| AI grunt-work line fused to authority clause so it cannot be detached and used against director-level | §7 |
| Silo diagnosis reframed: "rational residue of M&A"; Milwaukee as most mature, board starts from its patterns | §1 |
| TOGAF sequencing: principles + board deliver value week one; reference architecture builds behind them | §3 |
| Reference-architecture method: authored by regional experts through the board, not Julian solo | §6 |
| Reporting line decided: NOT inside Tony's org — firm position, hold it plainly | Moved 8 Aug to [[tti-story-bank]] §3 |
| Prior-proof: honest bridge drafted, welded to the de-risk; instruction to build one Telstra before/after | Superseded 8 Aug — the real answer is BG Group, [[tti-story-bank]] §1a |
| Coordination-tax: illustrative model + "can't cancel without replacing the decision function" | §5 |

### Still open (must close before the Ty room)

> **⚠ Corrected 8 Aug — this table had gone stale.** Two of the original four items were already closed and the table hadn't been updated; that is the exact failure mode this whole document restructure exists to fix. Verified against current content, not assumed.

| Item | Priority | Where |
|------|----------|-------|
| 🟡 **Name the charter.** Nobody has yet been named as the executive who sits above both regional technology lines, which is the escalation terminus the whole mandate design in §4 depends on. | Highest | §4 has a full answer to this now: it is a choice, not a missing requirement, and the CEO-chip fallback already gives Julian a complete answer even without a name. |
| 🟡 **Find a stuck-decision example.** Julian needs one real cross-region decision, currently stalled or stalled recently, to use as evidence for §5's coordination-tax argument and as the candidate for month 1's first deliverable. | Secondary on its own, but load-bearing for month 1 of the proposal | This is the same gap as "no named stuck cross-region decision" in the Gaps section of [[tti-ea-requirements]]. Kari is the only realistic route to it; see [[tti-role]] Next Actions. |
| ~~The prior-proof story~~ | — | **Closed on 8 Aug.** The answer is the BG Group Design Authority Julian designed, stood up and chaired - see [[tti-story-bank]] §1a. |
| ~~The SAP-or-Oracle criteria~~ | — | **This was never actually open.** §6 already names the criteria (total cost of ownership, existing skills concentration, the M&A roadmap, and integration surface), with a note that Julian should swap in whichever ones he would genuinely cite. It is a polish item, not a blocker. |

---

> **⚠ Removed 8 Aug — this banner duplicated the purpose block at the top of the
> document and had gone stale (it still claimed a fatal blocker that §4 resolved
> weeks ago).** All of its links already live in the Related section at the bottom.

---

## 0. The live urgency (H1 2026 results — three findings, each tied to a specific capability)

*Everything below is PUBLIC (30 Jun 2026 HKEX results announcement) - fully quotable. Full workup: [[tti-h1-2026-results-talking-points]].*

**The organising rule for this whole section, restated 8 Aug at Julian's direction: every finding here must name the specific EA/TBM/AI capability that addresses it.** A financial fact from the results is only worth including if it connects to something Julian would actually *do*. The share buyback was cut from this section on that basis - a real signal, but there is no EA lever that touches capital allocation, so it does not belong under "what architecture can achieve." It survives only as a fee-sizing aside; see the note at the end of §0c.

### 0a. The SG&A Squeeze

| | H1 2026 | Movement |
|---|---|---|
| Gross margin | 42.9% (record) | +258 bps |
| SG&A / sales | 33.0% | +173 bps |
| EBIT margin | 9.9% (record) | +86 bps |

**Roughly two-thirds of a record gross-margin gain was consumed by SG&A growth before it reached EBIT.** TTI's own explanation is mostly deliberate investment - new product development, field resources, commercialisation, write-offs from rationalising underperforming categories - **not waste, and do not imply otherwise.** But the arithmetic still stands, and it lands on the exact lever Ty has already named publicly: taking out *structural* corporate admin and G&A cost, on the way to the 10% EBIT target by 2027 (now independently confirmed in this same announcement - TTI is already at 9.9%).

**The capability that addresses it:** the portfolio-duplication and rework-avoidance levers already argued in [[tti-ty-engagement-proposal]]'s "Where the money is" table. Duplicate capability and re-cut programmes are structural G&A; architecture governance is what removes them and keeps them removed.

**Why this goes first, ahead of the silo diagnosis.** Everything from §1 onward argues that architecture removes structural cost. This section is the reason that argument is urgent *this half*, not evergreen: the easy operational margin has been taken, and TTI's own numbers say the next point has to come from the structural side. Open here, then move to §1's mechanism.

> **Say it like this:** "One thing that struck me in the half-year numbers - 258 basis points of gross margin is a serious operational result, but only 86 of it reached EBIT, because SG&A moved 173. Most of that looks like deliberate investment, not waste. But it does mean the next margin point has to come from the structural side, and that's the part architecture actually touches."

### 0b. The FCF Lever

**The signal:** TTI raised its 2026 free cash flow target mid-year, from over US$1.0bn to over US$1.3bn - a 30% increase in a target it had already committed to publicly, revised upward before the year was even half over.

**Why this is a genuinely different argument from the SG&A finding, not a repeat of it.** Free cash flow is operating cash flow minus capital expenditure. It is a specific, calculated number - not a general synonym for "cash flow," which is the broader term covering operating, investing and financing activity together. Because capex is subtracted to arrive at FCF, **any technology capex avoided through governance flows directly into this number.** A duplicate ERP or CRM build that never happens, a design that does not need re-cutting after the fact - both are capital that was never spent, which is capital that stays inside free cash flow rather than leaving it.

**The capability that addresses it:** the same portfolio-duplication and rework-avoidance levers as §0a, pointed at a different TTI metric. This is not a new mechanism - it is evidence that the mechanism already argued for touches a number TTI has just told the market it cares about more than it did six months ago.

**Why it may be the stronger hook of the two.** The EBIT target has existed since AR25; TTI is simply on track to hit it. The FCF target is the one that just moved, upward, mid-year - it is evidence of a live, current priority rather than a standing one.

> **Say it like this:** "You also raised the free cash flow target mid-year, from over a billion to over one-point-three - that's not a small revision. Free cash flow is operating cash minus capex, so anything on the technology side that avoids a duplicate build or a design that has to be re-cut isn't just an EBIT saving, it's capital that never left free cash flow in the first place."

### 0c. The Capacity Window

**The signal:** capital expenditure in H1 2026 included *"automation and productivity initiatives around the globe,"* with planned capacity expansion in **Vietnam and the Americas over the next 12-18 months.**

**Why this is a different kind of urgency from §0a and §0b.** Those two are about cost already being lost. This one is about cost not yet committed - new manufacturing capacity is about to be built, and it will either be built to a group standard from day one, or it will be built to whatever the local team already has, adding a fourth or fifth pattern to the estate that will need reconciling later. The cheaper moment to set a standard is before the capacity exists, not after.

**The capability that addresses it:** the same reference-architecture and standards machinery in §3 and §4, applied at the point of new build rather than as a retrofit. This is the only one of the three findings that is genuinely forward-looking rather than remedial.

> **Say it like this:** "The capacity expansion you've got coming in Vietnam and the Americas is actually the easiest place to start, not the hardest - it's cheaper to build to one standard from day one than to unpick five different patterns in eighteen months' time."

**A note on the share buyback (deliberately not included above as a finding).** TTI commenced a US$500m automatic repurchase plan in June 2026 (US$42m done by end of July). There is no EA, TBM or AI lever that touches capital allocation, so it does not belong in this section. Its only legitimate use anywhere in this engagement is as a scale comparison for the fee - US$320,644 is a rounding error against a US$500m buyback - which is the same breakeven-hurdle framing already in the proposal, not a new claim, and not evidence that architecture creates value at that scale.

## 1. The silo diagnosis (respectful — it's M&A residue, not incompetence)

The fragmentation is the rational residue of acquisition-led growth. TTI bought Milwaukee, Hoover, Vax and others; each integration call was made sensibly in isolation at the time, and deliberate decentralisation is part of what got the company to ~US$14bn. So the estate is not a disease to be cured. **What's missing is only the layer that makes the *next* decisions compose** instead of each one being reconciled from scratch.

**Exhibit A, stated carefully** ([[tti-technology-stack]]): SAP globally, Oracle Cloud ERP in NA finance, Oracle EBS legacy in HK. Three ERP tiers, no group reference architecture governing how they align. The endless steering committees are what the org uses to reconcile across that gap, meeting by meeting.

> **Say it like this:** "The committees aren't the problem, they're the symptom. The estate is fragmented for good historical reasons — acquisitions, each integrated as far as made sense at the time. What's missing is only the layer that stops the *next* cross-region decision needing a committee. Put that in and most of them stop being necessary."

**Backing the "Procurement leverage" row (added 8 Aug — this was asserted in [[tti-ty-engagement-proposal]] without an argument anywhere until now).** Steve Richman has said publicly he wants to *"leverage our negotiating costs on IT"* ([[tti-2025-ar-key-initiatives]], PUBLIC). Fragmentation is what blocks that: three or more regional variants of the same platform means three or more separate vendor negotiations, none big enough alone to move a vendor's price. **⚠ Do not claim this as a discount mechanic** — SAP and Oracle licences are not fungible the way cloud compute is, and licence negotiation is procurement's job, not an architect's (see §2a's caveat). **The honest claim is narrower and upstream of that:** reducing variant count is what lets procurement negotiate one enterprise-wide deal instead of several regional ones. Julian is not the one who gets the discount — he is the reason procurement is able to ask for it. That is exactly why the lever table says standards make consolidated negotiation *possible*, not that they *deliver* the saving.

> **Say it like this:** "One thing this also does, without it being the headline — Steve's talked publicly about wanting to leverage negotiating costs on IT. Right now that's hard, because every region's on its own variant, so procurement's negotiating three or four small deals instead of one big one. I'm not the one who gets you the discount — that's still procurement's job — but standardising is what makes it possible for them to ask for it."

**Scope guard (K3 — Kari's own framing, and it works in your favour).** Kari volunteered that the scope should be enterprise-wide: *"if we are doing this it should be done everywhere - across the whole enterprise"* - while naming Australia and Europe as already fine. Read it correctly: he is **not** asking for more work, he is asking for the capability to be designed at **group level rather than as a US-HK bilateral patch**. Take it, for three reasons. It is a bigger mandate at the same cost. It is a sponsor's own stated ambition, and matching it is free while declining it looks small. And it **dissolves the geography problem below** - at enterprise level this is not HK governing the US, it is a group layer above both, which is materially safer with Tony *and* with Shane. The formula that keeps it honest and guards against over-claiming for one person: **design enterprise-wide, deploy where the gap is.** Principles, standards and the board are group-level by construction because that is the only way they work; the first application is the Asia-US interface because that is where the fragmentation actually sits.

**Geography guard (Milwaukee):** never frame this as HK governing the US. Milwaukee is the most mature IT shop and the target should start *from* its patterns; its architecture leads are among the first board members. Position yourself as the coordination point pulling Asia's tiers toward the group standard, working *with* the US, exactly as Ty framed it, not a throne over it.

## 2a. Why the Centre Can Commit

> **⚠ Genuinely separate from 2b below, not two halves of one argument (corrected 8 Aug).** They used to share a parent section on the grounds that both use financial vocabulary - but that was the only thing they had in common. This one is an **authority argument**: why decisions should sit centrally. It has no relationship to cost, saving money, or TBM. Read it on its own.

The transferable idea is **not** discount mechanics (a finance-literate skeptic will correctly say SAP and Oracle licences don't pool like fungible compute, and licence consolidation is already procurement's job). The idea that transfers is **risk transfer through the centre**:

- A single region won't commit to a shared platform, because a failed bet lands on *its* P&L alone. So it stays on its own stack. That is how silos form.
- The centre can commit, because it spreads the bet across the whole portfolio, exactly as a central FinOps team carries Reserved-Instance utilisation risk on its own book so individual teams don't have to.

**Answer the accountability question before it's asked** (the sharp counter is "the FinOps centre owns a number; what number do YOU own?"): the EA role owns committees retired, integration rework avoided, and waiver cycle-time. Name it.

**And weld the "whose book carries the bet?" seam to §4** (the sharper counter: a governance board has no P&L, so it can't absorb a failed platform bet the way a FinOps team absorbs unused RIs). Don't claim the board absorbs the risk itself. The risk lands on the **charter executive's decision** to commit the group to a shared platform — which is exactly why the charter and group-level ownership of that decision matter. Say the weld out loud; don't let the seam show.

**Honest caveat:** don't claim the centre "never touches implementation" — a group ERP reference architecture visibly shapes what regions run. The line is: the centre owns the *target and the decision rights*; the regions own *how they get there*.

> **Say it like this:** "It's the FinOps risk-transfer principle. A single region won't commit to a shared platform because a failed bet is theirs alone — so it silos. The centre can commit because it carries that bet across the portfolio. Same reason a central FinOps team holds the commitment risk so the engineers don't have to."

## 2b. Cost Transparency (TBM)

*This answers a requirement Kari stated to Julian's face, so unlike most of this document it rests on something quotable. Independent of 2a above - that one is about authority, this one is about money.*

> **⚠ Seniority signal — do not conflate FinOps and TBM.** **FinOps is the cloud slice; TBM is the whole estate** (infrastructure, applications, licences, labour, outsourced services *and* cloud). They are not the same principles at different sizes. Getting this distinction right lands as senior in a CFO conversation; getting it wrong is a tell. This distinction matters here, not in 2a - 2a never claimed to be either discipline, it only borrowed FinOps's risk-transfer logic as an analogy. Source: [[tbm-vs-finops]].

**The stated requirement (K7, DIRECT — safe to reference):** responding to Julian's TBM point about shared data letting finance and IT discuss trade-offs in the same language, Kari said: **"We lack having that type of data available to us in the organisation."** He volunteered it as a real gap.

**What TBM actually is, and why the distinction is the argument.** TBM maps general-ledger technology spend up to business capabilities across infrastructure, applications, licences, labour and outsourced services — so the question shifts from *"what did technology cost?"* to *"is our total technology spend delivering business value?"* You cannot reduce a cost estate you cannot read, and today TTI's technology cost is a lump in the P&L rather than something anyone can manage line by line.

**Why this is defensible work and not a tooling purchase** ([[tbm-vs-finops]]): the cloud-FinOps layer is commoditising toward free and native — the hyperscalers ship it. What stays unautomated is the whole-estate allocation: mapping spend to capabilities is org-specific business-rule logic, the data is fragmented across the GL, CMDBs, HR, licence managers and contracts, and **the genuinely hard part is not the analytics but getting Finance and Engineering to agree the model and own the number.** That needs a neutral human with standing. It is exactly the coordinating role, and it is exactly what a tool cannot supply.

**The hook to a group cost standard — ⚠ ASK, NEVER ASSERT.** TTI is standing up a global platform for reading P&Ls and gross margin one consistent way (T13). **That is INTERNAL, from the employee Q&A — Julian must not reveal he knows it.** See [[tti-ea-requirements]] § Quotability. Raise the principle and let Ty supply the specific:

> *"Cross-functional platforms that give the business one consistent way of reading its numbers are exactly what architecture governance exists to protect — they fragment the moment each region interprets the standard slightly differently. Is there work like that underway?"*

If he says yes, the argument opens on his invitation: **a group P&L standard is how the *business* reads its money; TBM is how the *technology estate* reads its money — the same discipline in an adjacent domain, and the second feeds the first.** Without it, technology stays an unexplained lump inside the very platform he is building.

**And the EA close, which is the point:** one standard system across an organisation is an **architectural commitment, not a software purchase.** It stays standard only while something governs it; the moment each region interprets it locally you are back to reconciliation. Cross-business, cross-functional systems of exactly this kind are what enterprise architecture exists to encourage and then protect.

**Guardrail:** Casey owns that programme, with Frank and Ty. Never sound like you are taking it. The frame is strictly additive — you make sure the technology-cost view underneath exists, and that the standard holds across regions.

> **Say it like this (once he has raised it):** "That's the business view of the money. The bit that usually goes missing underneath is the technology view — mapping what the estate actually costs up to the capabilities it supports, so technology stops being one line in the P&L. That's TBM rather than FinOps; FinOps is just the cloud corner. The hard part isn't the tooling, it's getting Finance and Engineering to agree the model and own the number — and that needs someone neutral with the standing to settle it."

## 3. The TOGAF parts that map to his pain (memorable set) + the sequencing answer

Each component kills a specific silo behaviour:

- **Architecture Principles** — agreed rules that stop regional divergence ("conform to the group reference architecture unless a waiver is granted"; **"reuse before buy before build"**; "conform to group integration standards unless waived"). The mechanism that stops every decision becoming a fresh committee fight.
- **The Architecture Board + waiver/compliance process** — a *standing* body with chartered decision rights. The structural replacement for ad-hoc steering committees. (Authority: see §4 — this is the load-bearing part.)
- **Reference Architectures + the Architecture Repository** — a group-level target for ERP/CRM that regions conform to, built incrementally (see sequencing below).
- **ADM Phases G (Implementation Governance) and H (Architecture Change Management)** — the parts that *operationalise and sustain* governance, not just draw pictures.
- **Architecture Contracts + Compliance Reviews** — how you hold regional delivery to the target without a committee for every change.

> **Precision guard:** a **CAB** (Change Advisory Board) is ITIL operational change, *not* TOGAF. The anti-silo mechanism is the **Architecture Board** + principles + reference architecture; the CAB is the operational-change complement. Keep them distinct if probed.

**Sequencing answer (pre-empts "you can't govern against a target you don't have yet"):** principles and the board deliver value in **week one** — they resolve *live* cross-region decisions immediately; you don't need the finished target to stop the *next* divergence. The reference architecture then builds incrementally behind them. **Decisions first, documents second.** The committees start retiring as decisions get a home, not years later when the full target lands.

> **Note:** avoid "single source of truth for customer data" as an example principle — it strays into Brian Pivar's Enterprise Data & AI mandate ([[tti-ai-roles]]). Use the reuse/integration-standard examples above instead.

## 4. The mandate — where the authority comes from (THE load-bearing section)

*The fatal gap if unanswered: without a real charter the Architecture Board is "one more committee, chaired by the new guy," and a threatened Tony kills it by simply having his directors attend politely and never agree. Two things must both be true — a NAMED charter, and a DEADLOCK-BREAKER.*

**Who charters it — a joint charter, not a finance-only one.** The board's decision rights are granted from above, not claimed by the role. The honest design pairs **the business sponsor who owns the *cost* of the committee chaos** (Ty raised it) **with group technology leadership who owns authority over the technology line** (CIO tier — Tom Uva / David Butts level). Finance alone is fatal: a finance-only charter over technology directors reads as "architecture by spreadsheet," and the CIO cannot be missing from the design.
- **Frank's departure must NOT be load-bearing.** Frank Chan (Group CFO) is leaving; a charter resting on him dies at his farewell. It must rest on people who will still be there.
- 🟡 **DECISION NEEDED (your org knowledge):** name the single executive whose authority sits above BOTH the APAC technology directors (Tony's) AND Milwaukee / US IT — that is the escalation terminus. It is probably CEO-level or a jointly-constructed authority, not Ty alone. Until it has a name, the escalation stop does not yet exist. *This is now the single highest-value open item for the pitch.*
- **CEO-chip fallback (from the Ty sim — have this ready, or the qualification-gate line boomerangs).** Ty's realistic answer is "above both lines is the CEO, and I won't spend that chip on a role that doesn't exist yet, in the quarter our CFO is leaving." So don't require the CEO charter up front: **day-to-day ratifier is Tom Uva's tier** for anything inside the technology line, with the finance sponsor carrying the cost case; the **CEO-level terminus is a rarely-used backstop you design in but formalise later**, once the board has a track record and a number behind it. Charter what Ty + Uva can charter now; the backstop gets formalised once it's proven it converges. *(Caveat Ty will raise: a backstop added later is one Tony's people know isn't there yet — accept it, it's the price of a startable version.)*
- **⭐ Why this is genuinely hard, and the choice it leaves you (added 8 Aug, in answer to "why isn't there a documented answer here?").** This isn't undone through neglect - it requires org knowledge nobody but Julian has, and the two people who could supply a name (Uva, Butts) are candidates from the Ty simulation, not confirmed. Two ways to close it, and **this is a choice, not a missing requirement**:
  1. **The strong version:** Julian names an actual person before the Ty room - so if asked "who ratifies," the answer is a name, not a tier. Requires org knowledge Julian may or may not have yet.
  2. **The workable version, already fully built above:** don't name anyone yet. The CEO-chip fallback carries the room on its own - charter what Ty + Uva's tier can charter now, say the CEO backstop is designed in but not yet formalised. This is a complete, defensible answer; it is not a placeholder for the strong version.
  
  **The document does not need Julian to pick before Monday.** The CEO-chip fallback is sufficient by itself. Naming a real person is an upgrade if the knowledge exists, not a blocker if it doesn't.

**The board pools authority, it doesn't confiscate it.** The regional technology directors sit **on** the board; its decisions are *their* authority exercised together against an agreed standard, not taken from them. You chair the process; you do not outvote peers.

**The deadlock-breaker (without this, "no outvote" is a suicide clause).** Pooled authority means every member holds a veto — and Tony's directors work for Tony. If they attend and never converge, the board decides nothing and the "committees retired" KPI fires *you*. So the charter must contain:
- a **decision SLA** — the board resolves an item within a set window or it **auto-escalates** to the charter executive;
- a **ratification rule** — the chair recommends, the named executive ratifies, and **silence is consent, not a park**. "Forces convergence" has to be a written mechanism, not a verb in your mouth.

**Secure resourcing at charter, not per meeting.** A coordinator with no line reports controls none of the hours his deliverables need (reference architectures are authored by the regions' own architects). Tony can starve it by keeping his teams "very busy." So the charter commits a named share of regional architects' time to board working groups, agreed up front.

**Success = standing committees retired, counted honestly.** Define a retired committee as a *standing cross-region decision forum with recurring senior attendance*, baselined in week-one discovery by **calendar audit, not self-report** (or they just rename them "alignment syncs").

**Qualification-gate framing (turns the gap into a strength — say it before anyone else does):**
> "I'd only take this on if that charter exists. Without it, the board is just another committee, and I wouldn't chair that."

This signals you understand exactly why these roles fail, and pre-empts the "it's just another committee" kill.

> **Say it like this:** "The difference from another committee is a charter with teeth: chartered jointly by the business sponsor and group technology leadership — not a departing CFO — with a decision SLA and a single ratifier, so it can't be talked into stalemate. Your directors sit on it, so it's their authority pooled; I chair but don't outvote. Its metric is committees retired. If that charter isn't real, I wouldn't take the role, because then it's just another committee."

## 5. The coordination-tax number (Ty buys with figures)

Don't walk in with an unmeasured saving. Bring the **shape** of the number, and offer to measure it properly in week one.

**Illustrative model (calibrate the variables with real TTI figures):**
> If there are ~**[N]** standing cross-region steering committees, each ~**[8]** senior/director attendees, meeting ~**[fortnightly]** for ~**[2h]**, that's ≈ **[N × 8 × 26 × 2]** senior-hours a year in the room alone — before the far bigger cost: **decision latency**, projects and spend stalled while decisions bounce between silos waiting for reconciliation. At a blended loaded senior rate of ~**[£/hr]**, the room-time alone is ≈ **[£]**/yr; the latency cost is a multiple of it.

**Pre-empt the cheaper fix** (a hostile "then just cancel half the committees for free"): a committee can't be cancelled without replacing its *decision function* — that's why they exist and why they multiply. The board replaces the function; that's what makes retirement stick. Meeting-hours are the visible cost; the decision function is the load-bearing one.

**Bring one concrete latency example** 🟡 *(supply a real one):* a single named or anonymised cross-region decision that bounced for months while spend or a project stalled. One real story beats the algebra, and it evidences the latency cost the model can only assert.

**⭐ Why this one is genuinely unfinished, not just undone (added 8 Aug).** Unlike the charter question, there is no fallback that fully closes this - and it does double duty, which raises the cost of leaving it open:
- **It's the evidence for the coordination-tax argument here in §5** (the model above is otherwise pure algebra, bracketed variables, nothing real).
- **It's also the candidate for the actual first deliverable in month 1** of [[tti-ty-engagement-proposal]] - "one live cross-region decision taken through the mechanism." Same gap, doing two jobs.

**Why Julian can't supply it alone.** He is an outsider without visibility into which decisions are currently stuck inside TTI - and this is not a personal gap, it is the exact thing Kari named unprompted (K9, [[tti-ea-requirements]]): *"coming in as an outsider takes time - you need to get to know people and elicit information."* Kari is the route because he is the one person who has already described TTI's real organisational pain directly (K1, K7, K8) - not a cold ask, a continuation of a channel already open.

**The two ways to close it, and only one is fully built:**
1. **Best case:** Kari names an actual stuck decision before Monday. Closes §5's evidence gap *and* gives month 1 a concrete proof case, in one answer.
2. **Fallback, already written into the proposal's spoken version:** no example in hand, say so - *"I'd pick it with you in week one, against criteria: stuck across regions, someone senior waiting on it, real cost to the delay."* This closes month 1 (the mechanism is what's being sold, not the specific decision). **It does NOT close §5** - the coordination-tax model here still has no real evidence behind it either way, and stays illustrative until Kari answers or discovery runs in week one.

**The one thing to actively avoid: inventing a plausible-sounding example.** Same failure class as the ERP-tier attribution caught earlier the same day - a specific, wrong detail is worse than an honest "I don't have one yet."

> **Say it like this:** "I haven't measured your number yet — that's week one of discovery. But the shape is this: [N] committees, [8] senior people, [fortnightly], is already hundreds of director-hours a year just in the room, and the real cost is the decisions those rooms hold up — [your one concrete example]. You can't just cancel them; you have to replace what they decide, which is the board. My KPI is retiring them, measured and held to."

## 5b. Assurance — why governed programmes overrun less (answers K4)

*Numbered 5b deliberately: other files cite §4 and §6 by number, so renumbering would break them.*

**The stated requirement (K4, DIRECT from Kari — safe to reference).** Old leadership *"had been burnt by programmes that overran and cost a lot of money"* and therefore did not believe in spending on technology leadership or EA. Kari framed this as the *old* regime, improved under new leadership.

**Invert it — this is the strongest argument FOR the capability, not an objection to survive.** The pain is already felt and already believed inside TTI. That makes architecture governance the answer to a known problem rather than a cost needing justification. Do not defend against it; lead with it.

**The mechanism, in one idea.** Large technology programmes overshoot mostly not through incompetence, but because **the people accountable for hitting a date are also the people judging whether the design is sound.** When the design decision and the delivery pressure sit in the same hands, optimism is structural rather than personal. Independent architecture assurance separates those two jobs, so problems surface while they are still cheap to fix rather than at integration.

**Why it is an EA argument and not a PMO one.** A PMO tracks whether the plan is being followed; assurance tests whether the thing being built is the right shape and conforms to the standard. The second is what stops rework, and rework is the mechanism by which programmes overrun.

**The proof (now available — [[tti-story-bank]] §1a).** BG Group: 20+ design standards, design cycle times down up to 30%, **measured**. That is the same causal chain - a standard removes the re-litigated decision, so the work gets faster and lands right first time more often.

**A second, independent proof-point exists if BG Group alone doesn't land** (added 8 Aug, [[tti-story-bank]] §2): a separate engagement as Global Head of Enterprise Solutions Architecture delivered **US$60M+ of assured multi-tower solutions with a +20% right-first-time improvement via a solution-assurance restructure.** Different engagement, same mechanism - independent assurance catching design problems before they become rework. Hold in reserve rather than leading with both at once; one clean story beats two competing for the room's attention, but if Ty pushes on whether one data point is enough, this is the second one.

> **⚠ HARD GUARDRAIL — never name a programme, a number or a business unit.** The CEO's public position is that the North American ERP conversion *"executed flawlessly"*, and it is Shane Mall's business. Justin's ~US$50M overrun figure is unverified hearsay and must never be spoken. **Let Ty supply his own example.** Full intel and public record: [[tti-ea-requirements]] § The overrun question.

> **Say it like this:** "The reason big technology programmes overrun usually isn't incompetence. It's that the people accountable for the date are also the people judging whether the design is sound - so optimism is built into the structure, not the person. Assurance separates those two jobs. Nobody marks their own homework, and problems surface while they're still cheap. That's why a governed estate costs less to change than an ungoverned one."

## 6. The EA-vs-solution-architect boundary + how the deep work actually gets done

The EA value sits **above** the solution layer: you set the target, the principles, the integration standards and the conformance process, and govern them. This is a strength — the coordinating layer is what's missing. But the honest gap (Fable's hit) is that *reference architectures* and *compliance reviews* need domain depth to arbitrate an expert dispute. The answer is **method**, not pretending you have SAP/Oracle depth:

- **Reference architectures are authored BY the regional experts THROUGH the board** — working groups of the SAP and Oracle leads, chaired and forced to converge by you. You own the process and the decision; they own the technical content.
- **Compliance reviews are peer-review** by cross-region architects against the agreed target. You own whether it conforms to the *standard and the decision rights*; the technical judgement is the peers'.

> **The line (Julian's flagged favourite):** "I don't need to be your SAP expert. I need to make sure your ERP, CRM and integration decisions across regions conform to one target and one set of principles, so they stop diverging and stop needing a committee to reconcile each time. The regional solution architects hold the deep application knowledge; my job is to make that expertise compose across regions instead of fragmenting."

**"SAP or Oracle?" — answer the *process*, not the verdict.** If asked which ERP the group should standardise on, do NOT snap-judge it (you don't have the application depth, and pre-judging is reckless). Instead show you know how to *run the decision*: name the **criteria** — total cost of ownership, existing skills concentration, M&A roadmap, integration surface — and the **process**: the board runs that evaluation once, with the regional leads and the US; you own that it's settled on criteria rather than re-litigated per region. *(These criteria are a sensible default; swap in the ones you'd actually cite.)*

## 7. The killer objection, pre-empted (AI line welded to authority)

**"You'll just draw governance diagrams; we need someone who understands our application estate."**

1. **The coordination tax is the business case.** Coordinating people is extremely time-consuming, and right now that cost is hidden: senior people are kept waiting and blocked while decisions bounce between silos and committees. That lost time *is* the problem the role removes.
2. **Sharpened 8 Aug: AI closes the drafting gap, not the judgement gap or the authority gap - and this role needs both closed.** AI makes candidate options cheap now — draft standards, reference models, documentation. What it doesn't do is judge which option is actually sound, which risk is real versus noise, or when an exception is genuinely warranted; that discrimination comes from years of watching decisions go right and wrong, and it doesn't come bundled with the tool. And even where the judgement is right, a principal still lacks the **standing to make a decision stick across directors** who don't report to them. Lead with judgement, land on authority — a purely political "I need the title to be listened to" argument is weaker and less flattering than "I need the title because the judgement and the standing both have to be there." (Never say "AI does the grunt work" without both clauses welded on — detached, it hands a hostile stakeholder "a principal plus Copilot, in my org, half the cost.")
3. **Partnership, not replacement.** You partner with the regional solution architects who hold the deep application knowledge — you coordinate and govern, they implement.

> **Say it like this:** "AI makes candidate options cheap now — draft standards, reference models, documentation. What it doesn't do is judge which option is actually sound, or when an exception is genuinely warranted — that comes from years of watching decisions go right and wrong. And even where the judgement's right, a principal still doesn't have the standing to make it stick across directors who don't report to them. AI closes the drafting gap; it doesn't close the judgement gap or the authority gap. This role needs both closed, which is the whole reason it has to be at director level."

> **§8 removed 8 Aug.** It held predictable role-specific questions (reporting line,
> why external, prior-proof, first 90 days) - positioning/credibility answers, not
> arguments mapped to a stated requirement, so they didn't belong in this document by
> its own stated purpose. Moved to [[tti-story-bank]] §3, with the superseded Telstra
> bridge text dropped (the real prior-proof answer is BG Group, §1a).

## Related
- [[tti-ea-governance-value-fable-review-2026-07-19]] — the adversarial review this v2 hardens against
- [[tti-kari-call-prep]] — the distilled talking bank for the Kari call
- [[tti-engagement-strategy]] — strategy, director-level premise, Pivar guardrail
- [[tti-technology-stack]] — the three-tier ERP fragmentation (Exhibit A)
- [[tti-sysadmin-skills-bridge]] — the "I work with the sysadmins" gap analysis
- [[tbm-vs-finops]] — the FinOps operating-model source
