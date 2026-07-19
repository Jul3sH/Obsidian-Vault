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

> **CONVERSATION PREP. NOT AN ARTEFACT TO SHARE.** The argument, in memorable
> chunks, for how enterprise-architecture governance aligns TTI's regional
> application stack (ERP, CRM, integration) and dissolves the endless steering
> committees Ty described. Carry the points in conversation; don't read them off.
> Draw the sharpest lines into [[tti-kari-call-prep]].
>
> **v3 — hardened against TWO Fable adversarial passes**
> ([[tti-ea-governance-value-fable-review-2026-07-19]]). Round 2 added: the joint-charter
> design + deadlock-breaker (SLA + ratification) + resourcing commitment in §4, the
> committee-replacement pre-empt in §5, and the risk-transfer weld in §2.
>
> **⚠ ONE FATAL ITEM STILL NEEDS YOUR ORG KNOWLEDGE (🟡 §4): name the charter.** Who
> specifically grants and enforces the board's decision rights, given Frank (CFO) is
> leaving, Ty is only Deputy, and there's a CIO (Tom Uva)? And who is the single exec
> above BOTH APAC tech and Milwaukee IT (the escalation terminus)? Until that has a
> name, the mandate is scaffolding around a blank. **Close-second:** the parked
> prior-proof story (§8) — survivable in front of Kari, fatal in front of Ty.
>
> Strategy: [[tti-engagement-strategy]]. Their estate: [[tti-technology-stack]].
> FinOps source: [[tbm-vs-finops]].

---

## 1. The silo diagnosis (respectful — it's M&A residue, not incompetence)

The fragmentation is the rational residue of acquisition-led growth. TTI bought Milwaukee, Hoover, Vax and others; each integration call was made sensibly in isolation at the time, and deliberate decentralisation is part of what got the company to ~US$14bn. So the estate is not a disease to be cured. **What's missing is only the layer that makes the *next* decisions compose** instead of each one being reconciled from scratch.

**Exhibit A, stated carefully** ([[tti-technology-stack]]): SAP globally, Oracle Cloud ERP in NA finance, Oracle EBS legacy in HK. Three ERP tiers, no group reference architecture governing how they align. The endless steering committees are what the org uses to reconcile across that gap, meeting by meeting.

> **Say it like this:** "The committees aren't the problem, they're the symptom. The estate is fragmented for good historical reasons — acquisitions, each integrated as far as made sense at the time. What's missing is only the layer that stops the *next* cross-region decision needing a committee. Put that in and most of them stop being necessary."

**Geography guard (Milwaukee):** never frame this as HK governing the US. Milwaukee is the most mature IT shop and the target should start *from* its patterns; its architecture leads are among the first board members. Position yourself as the coordination point pulling Asia's tiers toward the group standard, working *with* the US, exactly as Ty framed it, not a throne over it.

## 2. FinOps analogy (a separate talking point — restated on RISK TRANSFER)

*Flagged deliberately as a distinct discipline — an operating-model analogy, native language for a finance audience, not a claim that EA is FinOps.*

The transferable idea is **not** discount mechanics (a finance-literate skeptic will correctly say SAP and Oracle licences don't pool like fungible compute, and licence consolidation is already procurement's job). The idea that transfers is **risk transfer through the centre**:

- A single region won't commit to a shared platform, because a failed bet lands on *its* P&L alone. So it stays on its own stack. That is how silos form.
- The centre can commit, because it spreads the bet across the whole portfolio, exactly as a central FinOps team carries Reserved-Instance utilisation risk on its own book so individual teams don't have to.

**Answer the accountability question before it's asked** (the sharp counter is "the FinOps centre owns a number; what number do YOU own?"): the EA role owns committees retired, integration rework avoided, and waiver cycle-time. Name it.

**And weld the "whose book carries the bet?" seam to §4** (the sharper counter: a governance board has no P&L, so it can't absorb a failed platform bet the way a FinOps team absorbs unused RIs). Don't claim the board absorbs the risk itself. The risk lands on the **charter executive's decision** to commit the group to a shared platform — which is exactly why the charter and group-level ownership of that decision matter. Say the weld out loud; don't let the seam show.

**Honest caveat:** don't claim the centre "never touches implementation" — a group ERP reference architecture visibly shapes what regions run. The line is: the centre owns the *target and the decision rights*; the regions own *how they get there*.

> **Say it like this:** "It's the FinOps risk-transfer principle. A single region won't commit to a shared platform because a failed bet is theirs alone — so it silos. The centre can commit because it carries that bet across the portfolio. Same reason a central FinOps team holds the commitment risk so the engineers don't have to."

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

> **Say it like this:** "I haven't measured your number yet — that's week one of discovery. But the shape is this: [N] committees, [8] senior people, [fortnightly], is already hundreds of director-hours a year just in the room, and the real cost is the decisions those rooms hold up — [your one concrete example]. You can't just cancel them; you have to replace what they decide, which is the board. My KPI is retiring them, measured and held to."

## 6. The EA-vs-solution-architect boundary + how the deep work actually gets done

The EA value sits **above** the solution layer: you set the target, the principles, the integration standards and the conformance process, and govern them. This is a strength — the coordinating layer is what's missing. But the honest gap (Fable's hit) is that *reference architectures* and *compliance reviews* need domain depth to arbitrate an expert dispute. The answer is **method**, not pretending you have SAP/Oracle depth:

- **Reference architectures are authored BY the regional experts THROUGH the board** — working groups of the SAP and Oracle leads, chaired and forced to converge by you. You own the process and the decision; they own the technical content.
- **Compliance reviews are peer-review** by cross-region architects against the agreed target. You own whether it conforms to the *standard and the decision rights*; the technical judgement is the peers'.

> **The line (Julian's flagged favourite):** "I don't need to be your SAP expert. I need to make sure your ERP, CRM and integration decisions across regions conform to one target and one set of principles, so they stop diverging and stop needing a committee to reconcile each time. The regional solution architects hold the deep application knowledge; my job is to make that expertise compose across regions instead of fragmenting."

**"SAP or Oracle?" — answer the *process*, not the verdict.** If asked which ERP the group should standardise on, do NOT snap-judge it (you don't have the application depth, and pre-judging is reckless). Instead show you know how to *run the decision*: name the **criteria** — total cost of ownership, existing skills concentration, M&A roadmap, integration surface — and the **process**: the board runs that evaluation once, with the regional leads and the US; you own that it's settled on criteria rather than re-litigated per region. *(These criteria are a sensible default; swap in the ones you'd actually cite.)*

## 7. The killer objection, pre-empted (AI line welded to authority)

**"You'll just draw governance diagrams; we need someone who understands our application estate."**

1. **The coordination tax is the business case.** Coordinating people is extremely time-consuming, and right now that cost is hidden: senior people are kept waiting and blocked while decisions bounce between silos and committees. That lost time *is* the problem the role removes.
2. **Authority is the scarce thing, and that's why it must be director-level.** The artefacts are cheap now — AI can draft candidate standards, reference models and documentation. Precisely *because* the artefacts are cheap, the scarce, valuable thing is the **standing to make a decision stick across directors**, which a principal has no way to hold. (Never say "AI does the grunt work" without this authority clause welded on — detached, it hands a hostile stakeholder "a principal plus Copilot, in my org, half the cost.")
3. **Partnership, not replacement.** You partner with the regional solution architects who hold the deep application knowledge — you coordinate and govern, they implement.

> **Say it like this:** "The hard part isn't the diagram, it's getting six regions to adopt one and stick to it — that's a decision-authority job, not a drawing job. The artefacts are cheap now; the scarce thing is the standing to make the call hold across your directors. A principal can't hold that by definition. That's the whole reason it has to be at director level."

## 8. Predictable director-hire questions (have an answer for each)

- **"Where does the role report?" (DECIDED — Julian, 19 Jul):** The role must **not** sit inside Tony Chung's organization. Chartered by the CFO/Ty, positioned to coordinate *across* the regions, dotted-line to group technology leadership. This is a firm position, not a preference: an inside-Tony reporting line would gut the cross-region mandate before it started (you cannot coordinate peers from inside one peer's org). Hold it plainly if asked.
- **"Why an external hire, not promote a regional architect who knows the estate?"** Precisely because an internal regional promotion inherits a region's allegiance and can't be neutral across the others — the coordinating role needs someone with no regional axe. Plus the cross-industry EA-governance track record most internal candidates won't have.
- **"Where have you done this before?"** 🟡 **PARKED — GENUINE BLOCKER for the Ty room (the sim confirmed it bites hardest here).** The prior-proof of an actual *governance forum that retired reconciliation overhead* — the evidentiary backbone of the pitch. **The honest bridge survives a receptive Ty ONCE, but NOT Ty retelling it to Tom Uva** — so it must be tightened in writing and backed by at least one concrete story.
  - **The honest bridge (rehearse until it's one breath long):** *"Straight answer: I haven't run this exact machine end to end under one charter, and I won't pretend otherwise. What I've run are its load-bearing parts at larger scale than you need — at Telstra International I held US$200M+ of regional designs a year to one group standard with a waiver process the regions couldn't route around. What I've never held is the charter to retire the committees around it. That gap is exactly why my ask isn't 'trust my track record' — it's a two-week audit and a threshold that kills the role before it starts if the number isn't there."* The confession must arrive **welded to the de-risk in the same breath**, never as a standalone admission.
  - **Build (≈one working session):** reconstruct ONE concrete Telstra International before/after — a named reconciliation forum / approval loop / recurring escalation that the design authority + waiver process made unnecessary: what it was, what replaced it, what stopped happening. Same for the US$300M transformation's design authority. *Scale answers ("US$200M/US$300M") do NOT satisfy this question — Ty asked before/after on committees, and reaching for scale reads as evasion.*
- **"What do you actually do in the first 90 days?"** Charter the board and its decision rights; stand up the principles that resolve live decisions immediately; measure the coordination-tax baseline; pick the first cross-region decision to settle through the board (not a committee) as the proof. Value visible in weeks, not years.

## Related
- [[tti-ea-governance-value-fable-review-2026-07-19]] — the adversarial review this v2 hardens against
- [[tti-kari-call-prep]] — the distilled talking bank for the Kari call
- [[tti-engagement-strategy]] — strategy, director-level premise, Pivar guardrail
- [[tti-technology-stack]] — the three-tier ERP fragmentation (Exhibit A)
- [[tti-sysadmin-skills-bridge]] — the "I work with the sysadmins" gap analysis
- [[tbm-vs-finops]] — the FinOps operating-model source
