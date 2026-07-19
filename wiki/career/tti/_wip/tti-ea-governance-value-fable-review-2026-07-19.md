---
type: review
tags: [career, tti, review, adversarial]
status: wip
created: 2026-07-19
reviewer: Fable (adversarial, in role as Tony Chung)
source-doc: tti-ea-governance-value
verdict: Does NOT survive a hostile room as written; one must-fix identified
---

> **Adversarial review of [[tti-ea-governance-value]].** Fable in role as a threatened
> Tony Chung (SVP Finance APAC + tech oversight) trying to kill the pitch in front of
> the CFO. Text-only critique; the source doc was not edited. Findings ranked most
> dangerous first. Fix tracker at the bottom.

## Verdict (headline)

As it stands, the argument **does not survive a hostile room.** It survives a friendly one — the diagnosis is sharp, the CAB/Architecture-Board precision guard is a real seniority signal, and "committees are the symptom" is the best line in the doc. But every load-bearing claim routes back to one unanswered question a threatened SVP finds in under a minute: **where does the authority come from, and what happens the first time a region ignores the board?**

**The ONE fix before the Kari call:** build the mandate answer — chartered by whom (CFO/Ty), regional directors sitting ON the board so it pools rather than confiscates their authority, escalation terminating at one named executive, success measured in committees retired — and attach even a rough coordination-tax number to it. **Secondary but urgent:** delete or weld down the AI grunt-work line; it currently points at the director-level anchor.

---

## Ranked weaknesses

### 1. The mandate void — "Your Architecture Board is just one more steering committee, with your salary attached" — FATAL
**Attack (Tony):** "His solution to too many committees is a new standing committee he chairs, with veto rights over decisions my directors make. Who grants those rights? Who enforces a waiver denial when Milwaukee ignores it? First time a region escalates over his head — day one — we're back to steering committees plus one extra layer and one extra director salary. No sponsor, no reporting line, no enforcement mechanism named. A board with no enforcement is a committee. He's not dissolving committees, he's applying to chair them."
**Why it's fatal:** The whole pitch rests on "a standing body with decision rights," but the doc never says where the rights come from, who the role reports to, or what stops the first escalation gutting the board. TOGAF itself requires executive-granted authority. Peer authority (director-level) is NOT decision authority over peers.
**Fix:** Board chartered by the CFO/Ty (who owns the committee-chaos cost); EA chairs but does not outvote; regional directors sit ON the board (their authority pooled, not taken); escalation terminates at one named executive. Pre-empt the "another committee" jibe: the difference is a standing charter + decision rights + waiver process vs ad-hoc reconciliation. Use the word "sunset" — success metric is committees retired, counted.

### 2. No number, for a CFO audience that already asked for one — SERIOUS (borderline fatal given audience)
**Attack (Tony):** "You're selling the removal of a coordination tax you haven't measured. How many committee-hours a month, at what loaded cost, what fraction removed, by when? I can tell you exactly what a director hire costs, fully loaded, today. You're asking two finance men to trade a measurable certain cost for an unmeasured hypothetical saving."
**Why:** Section 5 pt 1 ("the coordination tax IS the business case") is assertion, not case. The strategy log records Ty needing "concrete figures for the savings." The doc walked away from that.
**Fix:** Rough illustrative model — N committees × attendees × seniority × frequency × decision-latency cost — framed as "here's the shape; discovery week one measures it properly." A CFO forgives an estimate, not its absence. Make "count of standing committees retired" the role's KPI (also patches #1).

### 3. The FinOps analogy inverts under finance-literate pressure — SERIOUS
**Attack (Tony):** "Three problems. One: FinOps aggregation works because compute is a fungible commodity with a rate card; SAP and Oracle licences don't pool, so your aggregation captures nothing, and licence consolidation is what procurement already does. Two: in FinOps the central team carries the commitment on its own book — unused RIs are their miss. What number are YOU accountable for? Your centre takes no risk, it just tells my regions what to do — the opposite of the FinOps deal. Three: you say the centre never tells engineers how to build, but a group reference architecture tells regions which ERP to run. That's the centre dictating usage. Which is it?"
**Why:** The doc's "honest boundary" concedes quantifiability but misses the sharper breaks: the accountability asymmetry and the internal contradiction (don't-touch-implementation vs ERP-convergence target). Kari/Ty know committed-use mechanics cold.
**Fix:** Restate on risk transfer, not discount mechanics: a single region can't commit to a shared platform because a failed bet lands on its P&L alone; the centre spreads the bet across the portfolio, like the FinOps team carrying RI utilisation risk. Name the number the EA role owns (committees retired, rework avoided, waiver cycle time). Drop or heavily caveat "the centre never tells engineers how to build" — for ERP convergence it visibly does.

### 4. The AI line hands Tony his cheapest kill — SERIOUS
**Attack (Tony):** "AI does the grunt work, and the human part is judgment and commanding the room. That's what my existing directors are paid for. So the proposal is: AI does the artefacts, we need one more person to chair meetings. I can get that with a principal architect and a Copilot licence, in my org, half the cost, tomorrow. He wrote my counter-argument for me."
**Why:** Section 5 pt 2 answers an objection nobody will raise (no one argues AI replaces the role) and gifts the hostile stakeholder the exact reduction he wants: principal-level, inside Tony's line, AI-leveraged. Undermines the director-level anchor.
**Fix:** Cut the AI point from the killer-objection answer, or fuse it into the authority argument so it can't be detached: "it must be director-level precisely because the artefacts are cheap now — the scarce thing is standing to make a decision stick across directors, which a principal has no way to hold." Never let "AI does the grunt work" appear near the role justification without the authority clause welded on.

### 5. Credibility gap real at the reference-architecture layer — SERIOUS
**Attack (Tony):** "He'll write our group ERP reference architecture and run compliance reviews on SAP S/4 and Oracle Cloud, and he's not an SAP or Oracle architect. Who evaluates conformance? The regional architects he's governing — they'll snow him in a quarter, and every dispute he can't arbitrate goes to a committee. And ask him: SAP or Oracle? If it's 'that's for the board to determine,' we've hired a man to draw the box others fill in — the diagram-drawer objection he claims to have answered."
**Why:** "I govern, they implement" holds at the principles/decision-rights layer (section 4 is genuinely strong there). It sinks at reference architectures + compliance reviews, which need domain depth to arbitrate an expert dispute.
**Fix:** Reference architectures authored BY the regional experts THROUGH the board (working groups of SAP/Oracle leads, chaired and forced to converge by the EA); compliance reviews = peer-review by cross-region architects against the agreed target, EA owning process and decision, not technical judgment. Prepare a non-empty answer to "SAP or Oracle?" — the criteria and decision process, named, even if not the verdict.

### 6. The silo diagnosis insults the room and ignores why the estate is fragmented — SERIOUS
**Attack (Tony):** "Three ERP tiers exist because we bought Milwaukee, Hoover, Vax and others, and someone at this table decided integration wasn't worth it at the time. Deliberate decentralisation got this company to fourteen billion. He's diagnosing our success as a disease and calling decisions made by people in this room 'papering over.' And an architect in Hong Kong governing Milwaukee's stack, our most mature shop? They'll laugh him off the first call."
**Why:** Two holes — (i) fragmentation has an M&A history / deliberate rationale the doc never acknowledges, so "no governance" reads as ignorant and accusatory; (ii) Ty's framing was "working with the US," and the doc is silent on the geography of authority. HK-governs-Milwaukee is the most politically explosive part of the design, unaddressed.
**Fix:** Reframe with respect: "the fragmentation is the rational residue of acquisition-led growth — each decision sensible in isolation; what's missing is only the layer that makes the NEXT decisions compose." Milwaukee answer: board's first members include Milwaukee's architecture leads; the target likely starts FROM Milwaukee's patterns (most mature); HK is the coordination point for Asia's tiers converging toward it, not a throne over the US.

### 7. TOGAF sequencing gap — you can't run Phase G with no target — SERIOUS but repairable
**Attack (Tony):** "He leads with Phases G and H — implementation governance and change management. TOGAF governs conformance against a target architecture. We don't have one. Producing a group target for a three-ERP, fourteen-billion multinational is Phases A–F — years. So what happens to my committees in year one while he draws the target? They keep running. His headline — 'put the framework in and most committees stop' — has a two-to-three-year hole."
**Why:** Leading with G/H implies governance can start before the artefacts it governs against exist. (CAB/Architecture-Board guard is correct and holds. Minor: say "Architecture Change Management" for Phase H precision.) Separately, the "single source of truth for customer data" example principle strays into Brian Pivar's Enterprise Data & AI mandate — violates the never-compete-with-Pivar guardrail.
**Fix:** Sequencing answer: principles + board deliver value week one (they resolve live decisions immediately; you don't need the full target to stop the next divergence), reference architecture builds incrementally behind them — decisions first, documents second. Swap the customer-data principle for something outside Pivar's turf (e.g. "reuse before buy before build," or "conform to group integration standards unless waived").

### 8. Missing entirely — questions with no answer anywhere — SERIOUS in aggregate
**Attacks (Tony, rapid fire):** "Where does the role report — to Ty in finance? That's architecture by spreadsheet. Why an external hire, not extend Milwaukee's function or promote a regional architect who knows our estate? Where has he done this before — name one company where his board demonstrably retired committees? What does he actually do in the first ninety days?"
**Why:** Reporting line, why-external, prior proof, first-90-days are the four most predictable director-hire questions; the doc holds zero answers. Kari will ask at least two.
**Fix:** One prep paragraph each. Reporting line is hardest (connects to #1) — decide it before Kari asks; "I don't mind where it sits" reads as no plan, any specific answer creates a specific enemy. Least-bad framing: chartered by the CFO, dotted to group IT leadership, explicitly NOT in the regional line — but that needs deciding, not improvising.

---

## Fix tracker (priority order)

| # | Fix | Severity | Status |
|---|-----|----------|--------|
| 1 | Mandate answer: chartered by CFO/Ty; directors sit ON the board; escalation to one named exec; KPI = committees retired | FATAL | ✅ addressed v2 §4 |
| 2 | Rough coordination-tax number + committees-retired KPI | Serious | ✅ addressed v2 §5 (needs real variables) |
| 4 | Delete/weld the AI grunt-work line to the authority clause | Serious | ✅ addressed v2 §7 |
| 3 | Restate FinOps analogy on risk-transfer; name the number the role owns; caveat "never tells how to build" | Serious | ✅ addressed v2 §2 |
| 6 | Respectful silo reframe (M&A residue) + Milwaukee/geography answer | Serious | ✅ addressed v2 §1 |
| 5 | Reference-architecture method (authored by experts through the board); "SAP or Oracle?" decision-process answer | Serious | ✅ method addressed v2 §6; 🟡 SAP-or-Oracle criteria need Julian's call |
| 7 | Sequencing answer (principles+board deliver week one); swap the Pivar-adjacent principle; "Architecture Change Management" wording | Serious | ✅ addressed v2 §3 |
| 8 | Prep paragraphs: reporting line, why-external, prior proof, first-90-days | Serious | ✅ addressed v2 §8; 🟡 reporting line + prior-proof story need Julian's call |

**Two open items requiring Julian's decision (not draftable for him):**
1. **Reporting line** (§8) — needs deciding before the Kari call, not improvising.
2. **SAP-or-Oracle criteria** (§6) — confirm the actual evaluation criteria he'd name.
Plus: supply the real "governance forum that retired committees" prior-proof story (§8).

---

## ROUND 2 (reviewing the hardened v2 → produced v3)

Fable, still in role as hostile Tony. Verdict: **v2 survives the first minute of a hostile room, not the third.** 3 of 8 fully closed (AI-line weld, silo reframe, sequencing); the rest partial; the fatal mandate gap only half-filled. The fixes opened new attacks:

**New FATAL #1 — the charter has no charterer.** "Chartered by the CFO/Ty" collapses on "name them": Frank Chan (Group CFO) is leaving; Ty is only *Deputy*; the CIO (Tom Uva) is absent from the design; and no single named exec sits above both APAC tech and Milwaukee IT (the escalation terminus). A finance-only charter over tech directors = "architecture by spreadsheet."
→ *Fix applied v3 §4:* joint charter (Ty + group tech leadership), Frank explicitly not load-bearing, 🟡 the above-both-regions escalation name flagged as the top open item.

**New FATAL #2 — the no-outvote board is a suicide clause.** Tony's cleanest kill: instruct his directors to attend politely and never agree. No outvote + no technical arbitration + no deadlock-breaker = board decides nothing, "committees retired" KPI fires Julian.
→ *Fix applied v3 §4:* decision SLA (auto-escalate) + ratification rule (silence = consent).

**Serious — resource starvation** of a floating coordinator with no line reports. → *Fix v3 §4:* resourcing committed at charter.
**Serious — the tax model invites the cheaper fix** ("cancel the committees for free"). → *Fix v3 §5:* can't cancel without replacing the decision function; bring one real latency example.
**Serious — risk-transfer onto an entity with no book.** → *Fix v3 §2:* welded to the charter executive's decision.
**Minor — "committees retired" is gameable** (rename to "alignment sync"). → *Fix v3 §4:* defined + calendar-audit baseline.

**Round-2 single highest-value remaining fix:** 🟡 **name the charter** — who specifically grants and enforces the decision rights given Frank's exit, Ty's deputy status, and Uva's existence; and the one exec above both regions. Everything else in §4 is scaffolding around that name. Close-second: the parked prior-proof story — survivable before Kari, fatal before Ty.

**Factual flag (out of role):** the doc previously said "chartered by the CFO/Ty" as if interchangeable; the stakeholder file has Frank Chan as Group CFO (leaving) and Ty as Deputy, with Tom Uva (CIO) absent from the governance design. Corrected in v3.

## Related
- [[tti-ea-governance-value]] — the source doc under review (now v3)
- [[tti-kari-call-prep]] — the talking bank these fixes feed
- [[tti-engagement-strategy]] — director-level premise, mandate principle, Pivar guardrail, political read on Tony
