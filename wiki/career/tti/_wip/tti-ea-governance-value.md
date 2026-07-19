---
type: prep
tags: [career, tti, prep, enterprise-architecture, conversation]
status: wip
created: 2026-07-19
updated: 2026-07-19
version: v2 (hardened against Fable review)
audience: Julian only (conversation prep)
send: NEVER
---

> **CONVERSATION PREP. NOT AN ARTEFACT TO SHARE.** The argument, in memorable
> chunks, for how enterprise-architecture governance aligns TTI's regional
> application stack (ERP, CRM, integration) and dissolves the endless steering
> committees Ty described. Carry the points in conversation; don't read them off.
> Draw the sharpest lines into [[tti-kari-call-prep]].
>
> **v2 — hardened against the Fable adversarial review**
> ([[tti-ea-governance-value-fable-review-2026-07-19]]). The mandate answer (§4), the
> coordination-tax number (§5), the risk-transfer FinOps restatement (§2), the
> reference-architecture method (§6) and the director-hire answers (§8) are new. **Two
> items still need YOUR decision, flagged 🟡 in §6 and §8: the reporting line and the
> SAP-or-Oracle criteria.**
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

*This is the fatal gap if left unanswered: without it, the Architecture Board is just "one more committee, chaired by the new guy." Have this ready cold.*

- **Chartered by the CFO / Ty** — the executive who owns the *cost* of the committee chaos grants the board its decision rights. The authority is delegated from the top, not claimed by the role.
- **The board pools authority, it doesn't confiscate it.** The regional technology directors sit **on** the board. Its decisions are *their* authority exercised together against an agreed standard, not authority taken away from them. (This is the answer to a threatened Tony: you're not overruling his directors, you're giving them one table to decide at.)
- **The EA chairs but does not outvote.** Chairs the process, owns the decision rights of the forum, forces convergence — does not personally veto peers.
- **Escalation terminates at one named executive**, not another committee. The first time a region tries to go over the board's head, there is a single defined stop, so escalation can't gut the board.
- **Success is measured in committees retired, counted, and sunset.** The board's own KPI is the number of standing steering committees it makes unnecessary. That converts "another layer" into "a layer that removes layers."

> **Say it like this:** "The difference between this and another committee is a charter. It's chartered by Ty with real decision rights; your directors sit on it, so it's their authority pooled, not taken; I chair it, I don't outvote anyone; and escalation ends at one named exec, not a fresh committee. Its success metric is how many standing committees it retires."

## 5. The coordination-tax number (Ty buys with figures)

Don't walk in with an unmeasured saving. Bring the **shape** of the number, and offer to measure it properly in week one.

**Illustrative model (calibrate the variables with real TTI figures):**
> If there are ~**[N]** standing cross-region steering committees, each ~**[8]** senior/director attendees, meeting ~**[fortnightly]** for ~**[2h]**, that's ≈ **[N × 8 × 26 × 2]** senior-hours a year in the room alone — before the far bigger cost: **decision latency**, projects and spend stalled while decisions bounce between silos waiting for reconciliation. At a blended loaded senior rate of ~**[£/hr]**, the room-time alone is ≈ **[£]**/yr; the latency cost is a multiple of it.

> **Say it like this:** "I haven't measured your number yet — that's week one of discovery. But the shape is this: [N] committees, [8] senior people, [fortnightly], is already hundreds of director-hours a year just in the room, and the real cost is the decisions those rooms are holding up. My KPI is retiring them. You'd be trading a measurable hire against a saving I'll measure and be held to."

## 6. The EA-vs-solution-architect boundary + how the deep work actually gets done

The EA value sits **above** the solution layer: you set the target, the principles, the integration standards and the conformance process, and govern them. This is a strength — the coordinating layer is what's missing. But the honest gap (Fable's hit) is that *reference architectures* and *compliance reviews* need domain depth to arbitrate an expert dispute. The answer is **method**, not pretending you have SAP/Oracle depth:

- **Reference architectures are authored BY the regional experts THROUGH the board** — working groups of the SAP and Oracle leads, chaired and forced to converge by you. You own the process and the decision; they own the technical content.
- **Compliance reviews are peer-review** by cross-region architects against the agreed target. You own whether it conforms to the *standard and the decision rights*; the technical judgement is the peers'.

> **The line (Julian's flagged favourite):** "I don't need to be your SAP expert. I need to make sure your ERP, CRM and integration decisions across regions conform to one target and one set of principles, so they stop diverging and stop needing a committee to reconcile each time. The regional solution architects hold the deep application knowledge; my job is to make that expertise compose across regions instead of fragmenting."

**🟡 DECISION NEEDED — "SAP or Oracle?"** You need a non-empty answer ready. Not the verdict (that's the board's, evidenced), but the **criteria and the process**: e.g. "the group weighs total cost of ownership, existing skills concentration, M&A roadmap and integration surface; the board runs that evaluation with the regional leads and the US; I own that it gets decided *once*, on criteria, rather than re-litigated per region." *Confirm the criteria you'd actually name.*

## 7. The killer objection, pre-empted (AI line welded to authority)

**"You'll just draw governance diagrams; we need someone who understands our application estate."**

1. **The coordination tax is the business case.** Coordinating people is extremely time-consuming, and right now that cost is hidden: senior people are kept waiting and blocked while decisions bounce between silos and committees. That lost time *is* the problem the role removes.
2. **Authority is the scarce thing, and that's why it must be director-level.** The artefacts are cheap now — AI can draft candidate standards, reference models and documentation. Precisely *because* the artefacts are cheap, the scarce, valuable thing is the **standing to make a decision stick across directors**, which a principal has no way to hold. (Never say "AI does the grunt work" without this authority clause welded on — detached, it hands a hostile stakeholder "a principal plus Copilot, in my org, half the cost.")
3. **Partnership, not replacement.** You partner with the regional solution architects who hold the deep application knowledge — you coordinate and govern, they implement.

> **Say it like this:** "The hard part isn't the diagram, it's getting six regions to adopt one and stick to it — that's a decision-authority job, not a drawing job. The artefacts are cheap now; the scarce thing is the standing to make the call hold across your directors. A principal can't hold that by definition. That's the whole reason it has to be at director level."

## 8. Predictable director-hire questions (have an answer for each)

- **🟡 DECISION NEEDED — "Where does the role report?"** The hardest one, and it connects to §4. "I don't mind where it sits" reads as no plan; any specific answer creates a specific enemy. Least-bad framing to pressure-test: **chartered by the CFO, dotted-line to group technology leadership, explicitly NOT inserted into the regional (Tony) line** — so it coordinates across the regions rather than sitting inside one. *Decide this before the Kari call; don't improvise it live.*
- **"Why an external hire, not promote a regional architect who knows the estate?"** Precisely because an internal regional promotion inherits a region's allegiance and can't be neutral across the others — the coordinating role needs someone with no regional axe. Plus the cross-industry EA-governance track record most internal candidates won't have.
- **"Where have you done this before?"** [🟡 supply your real story] Candidate: Global Head of Enterprise Solution Architecture at Telstra International, governing US$200M+ of designs to one standard; US$300M+ managed-services transformation governed across many streams without disruption. *Frame the one that best shows "a governance forum that retired reconciliation overhead," with a concrete before/after.*
- **"What do you actually do in the first 90 days?"** Charter the board and its decision rights; stand up the principles that resolve live decisions immediately; measure the coordination-tax baseline; pick the first cross-region decision to settle through the board (not a committee) as the proof. Value visible in weeks, not years.

## Related
- [[tti-ea-governance-value-fable-review-2026-07-19]] — the adversarial review this v2 hardens against
- [[tti-kari-call-prep]] — the distilled talking bank for the Kari call
- [[tti-engagement-strategy]] — strategy, director-level premise, Pivar guardrail
- [[tti-technology-stack]] — the three-tier ERP fragmentation (Exhibit A)
- [[tti-sysadmin-skills-bridge]] — the "I work with the sysadmins" gap analysis
- [[tbm-vs-finops]] — the FinOps operating-model source
