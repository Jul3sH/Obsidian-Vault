---
type: simulation
tags: [career, tti, prep, kari, rehearsal]
status: wip
created: 2026-07-19
model: Fable (role-play as Kari)
audience: Julian only (rehearsal)
send: NEVER
---

> **CALL REHEARSAL — Fable role-playing Kari against Julian's real prep-doc lines.**
> A simulated dialogue to hear how the argument performs live, plus a failure-point
> analysis and a Kari receiver-profile. Read the transcript for the *feel*; the
> distilled tactical moves live in [[tti-kari-call-prep]]. Not a script to recite.

## The single most important thing

Julian must leave the call having **changed the sentence Kari says to Frank, without Kari ever noticing he was corrected.** In: "we're adding IT support, Julian could be the guy." Out: "this is the director-level governance role Ty wants, it pays for itself in retired committees, I can put it to Frank." The mechanism is **attribution**: the altitude always comes from *Ty's* description and from *cost logic Kari completes himself*, never from Julian's ambition. If Kari feels he *discovered* the bigger role, he carries it to Frank as his own find — that, before Frank leaves, is the whole game.

---

## 1. Simulated transcript

*Kari calls Julian, HK morning. Warm, unhurried; a finance man who likes the practical point.*

**KARI:** Julian! Good to finally speak. Stephan speaks very highly of you, and I had a good chat with Ty last week. Impressive CV. So look, I think there's something here. We've been saying we need to add some IT support in the region, and your profile could be a good fit.

**JULIAN:** Kari, thanks for making the time. And thank you for reading the CV and talking to Ty. Before I say anything, I'd love to hear what you took from the conversation with Ty. What did he describe to you?

**KARI:** Ty's view and mine are pretty aligned. The systems side here is stretched. We still run Oracle EBS in Hong Kong, legacy, and the finance reporting takes too long. And that Principal System Administrator posting, we never filled it properly. So when Stephan raised your name I thought, good, someone senior, hands-on, based here, who can support the IT side.

**JULIAN:** That matches what I saw, and the Hong Kong estate is a good example of the bigger thing Ty described. When we spoke, he didn't lead with the systems, he led with the coordination problem: fragmented technology leadership across the region, too many steering committees just to get cross-region decisions made. The committees aren't the problem, they're the symptom. The estate is fragmented for good historical reasons, acquisitions, each integrated as far as made sense at the time. What's missing is the layer that stops the next cross-region decision needing a committee.

**KARI:** Hm. That's more of a... management consulting answer. Let me be direct. What we feel day to day is more basic. Systems break, projects stall, the sysadmin team is thin. Isn't the practical need just that unfilled Principal System Administrator role? You've done networks, cloud, security. Why isn't that the job?

**JULIAN:** Fair question, and I'd rather you asked now than after. Two honest answers. First, that role is real and TTI should fill it, it's just a different job: hands-on platform operations, and frankly there are people who'd do it better than me at half the cost, because that's what they do all day. Second, the hands-on work isn't where the problem Ty described lives. What I'd do is work with your existing system administrators to turn what they do into repeatable, governed patterns, which frees me to do the thing that's actually missing: the architecture framework and governance that stops every decision going to a steering committee.

**KARI:** OK, but "governance" is one of those words. When Frank hears governance he hears headcount that writes PowerPoints. What do you actually produce?

**JULIAN:** Decisions that stick, mainly. Take your ERP picture, since you live in it. SAP globally, Oracle Cloud in North America finance, Oracle EBS legacy here. Three tiers, no group reference architecture governing how they align. Every time two have to talk, someone convenes a committee, senior people dial in, and the decision bounces for months. The hard part isn't drawing the target, the drawings are cheap now, AI drafts most of that. The hard part is getting the regions to adopt one and stick to it. That's a decision-authority job, not a drawing job.

**KARI:** The reconciliation point I recognise. We spend a ridiculous amount of finance time reconciling data between those three at every close. So you reduce that how? What's the number?

**JULIAN:** I haven't measured your number yet, and I won't pretend to. That's week one. But the shape: a dozen standing cross-region committees, eight senior people each, fortnightly, two hours, that's thousands of senior hours a year just in the room. And the room time is the small cost. The big one is decision latency, projects and spend stalled while a decision bounces. My commitment: baseline it in the first weeks, by calendar audit, and be measured on retiring those committees.

**KARI:** Then why hire anyone? If the committees are waste, cancel half of them. That's free.

**JULIAN:** Because a committee can't be cancelled without replacing its decision function. That's why they exist and multiply. Each is doing a real job badly: making a cross-region call nobody has the standing to make alone. You have to give those decisions a home before you can close the rooms. That's what the role is, the home.

**KARI:** All right. Ty said enterprise architect, senior. You're saying director. Why? We could bring you in at principal level, prove yourself a year, then talk. Cleaner for Frank. Cheaper.

**JULIAN:** I understand why that's cleaner, and if this were a normal hire I'd agree. Here's why it doesn't work for this role. TTI APAC has multiple technology directors already, reporting into Tony. The role coordinates across exactly those people. A principal is an individual contributor, no cross-director mandate, so from day one every director can politely ignore him, and the whole value, decisions that stick, is dead on arrival. Then you've spent the money and got nothing. That's not about my career, it's whether the role can work. Director is the floor.

**KARI:** Mm. Tony. How does this sit with Tony's organisation? He runs technology in the region.

**JULIAN:** Carefully and respectfully, honestly. His directors would sit on the architecture board, so it's their authority pooled, exercised together against an agreed standard, not taken from them. I'd chair the process, I wouldn't outvote anyone. And the target should start from Milwaukee's patterns, they're the most mature, this isn't Hong Kong governing the US. But structurally the coordinating seat has to sit across the regions, not inside one, otherwise it can't be neutral. The charter would come from the business sponsor and group technology leadership, with a decision SLA and a ratification rule so the board can't be talked into stalemate, and...

**KARI:** *(at capacity)* Julian, you're losing me a little. SLAs, ratification. I'm a tax guy.

**JULIAN:** *(recovering)* Sorry, that was the machinery. The finance version, because there's an analogy you'll know better than I do. It's the FinOps principle, risk transfer through the centre. A single region will never commit to a shared platform, because if the bet fails it lands on their P&L alone. So every region stays on its own stack, and that's how you got three ERPs. The centre can make the commitment because it carries the bet across the whole portfolio. Same reason a central FinOps team holds cloud commitment risk so individual teams don't. What I'd run is the mechanism that lets TTI make those group calls once, on criteria, instead of six times in six committee cycles.

**KARI:** That I follow. It's the same logic as central treasury versus each entity hedging its own FX. Nobody hedges properly when it's their own book.

**JULIAN:** That's a better version of my analogy than mine. Yes. Exactly that.

**KARI:** Practical matters. What does this cost? Frank will ask in the first thirty seconds. Director-level in Hong Kong is not small money.

**JULIAN:** It isn't, and I won't dance around it. But I'd rather the structure and number come out of the conversation with Frank and Ty, because the shape, permanent versus an initial engagement, drives it. What I'd say to Frank is what I've said to you: measure it against the coordination cost. If the role can't retire enough committee and reconciliation overhead to cover itself several times over in year one, it shouldn't exist, and I'd be the first to say so.

**KARI:** That's a decent answer, though he'll still want a number. And Frank's leaving, you know.

**JULIAN:** I'd heard. How does that change things, in your view? Would Frank want to shape this before he goes, or would it wait for his successor?

**KARI:** Depends how it's framed. Frank doesn't want to hand his successor a mess, but he won't create a big new structure on his way out unless Ty is clearly driving it and it looks like Ty's initiative. If it's positioned as filling the IT support gap, that's easy, it's small. What you're describing is bigger. Bigger is slower.

**JULIAN:** Useful read. Can I ask it this way: from where you sit, what would Frank need to see for the bigger version, the governance version, to be sign-able rather than parkable? Because the smaller version doesn't fix the thing Ty raised, it just adds a person to it.

**KARI:** *(pause)* He'd need Ty to own it on paper. A number, even rough. And it not to look like a fight with Tony, because Frank hates mess in his last quarter more than he hates cost. If those three are there, Frank listens to me on IT spend, I can put it in front of him properly.

**JULIAN:** Then can I ask for exactly that? Not a pitch, just the accurate framing. When you speak to Frank, the sentence I'd hope survives is: this is the person Ty wants to run the architecture governance that gets us out of the committee and reconciliation mess, and it only works at director level because it coordinates the existing directors. If that's a sentence you're comfortable saying, that's worth more than anything I could send.

**KARI:** I can say something like that. Though knowing Frank, send me half a page too. Numbers-shaped, not architecture-shaped. What it costs the group today, what changes. I can walk that in.

**JULIAN:** Done, you'll have it within a couple of days. And one more thing on timing: my family has a schooling decision in mid-August that fixes where we're based, so I'm working to know whether this is real before then. I'm not asking anyone to rush, but if the honest answer is it can't move until after Frank goes, that's genuinely useful to know early.

**KARI:** Understood, and better you tell me now. Let me talk to Frank this week, maybe Ty again. Send me the half page. And Julian, this was more interesting than I expected. I came in thinking IT support.

**JULIAN:** Well, the support is real, someone should fill that sysadmin seat. I'd just like to be the reason it's the last committee TTI ever creates to decide something like that.

**KARI:** *(laughs)* All right. We'll speak soon.

---

## 2. Failure points (in call order)

1. **The first 30 seconds — the "IT support" anchor.** Never let it stand, never correct it. **Redirect:** "what did you take from Ty?" so Ty's words lift the altitude, not Julian's. Kari can't be offended by Ty.
2. **"Why isn't this the Principal System Administrator role?"** Don't disparage it (insults Kari's IT people) or claim you'd do it too (re-anchors you as the hands-on hire). **Validate + cost logic:** "a dedicated platform person would do it better at half the cost; hiring me into it wastes the money and the thing Ty asked for."
3. **Director ask lands as ego/cost.** Lead with the failure cost: **"the cheap version isn't cheaper"** — a coordinator below the directors gets ignored; same money, structurally can't deliver. That's a cost argument Kari can carry to Frank.
4. **Jargon overdose.** Charters/SLAs/ratification are Ty-grade; they made sim-Kari disengage. **One sentence of machinery max, then the treasury/FinOps analogy.** When Kari improves the analogy (treasury vs FX), surrender authorship instantly — now he owns it and repeats it.
5. **The cost question.** Don't name a number (becomes the anchor Frank negotiates down). **Refuse + offer the self-funding test.** Finance loves a hire that carries its own P&L test.
6. **School deadline.** Not pressure. Once, late, framed as candour with an easy out ("tell me if it's dead"). High-status: signals other branches, turns Kari into an informant not a pressured middleman.

**Tony hazard:** if asked, only the safe register — directors sit ON the board, authority pooled, Milwaukee patterns lead, and **never one negative syllable about Tony.** Kari talks to everyone in that office; assume it reaches Tony verbatim.

---

## 3. Kari receiver-profile + conversion plan

**What he cares about (ranked):** (1) not being embarrassed in front of Frank; (2) cost justification; (3) the local concrete HK pain (Oracle EBS, thin support, reconciliation grind — his "IT support" framing is his daily experience, not ignorance); (4) his own standing across the Frank→successor transition; (5) how the role is structured (perm vs engagement, whose budget).

**What's in it for him:** to be the finance-side author of fixing what finance suffers most (the reconciliation/coordination tax across three ERP tiers), banking a win with both Frank (departing) and Ty (ascendant). If Julian succeeds, Kari brokered it. Let him have that story.

**Conversion plan (supportive contact → active advocate):**
1. Let him co-author the argument; when he reframes it in his own metaphor, hand him ownership.
2. Attribute the altitude to Ty throughout — "the role Ty described" is safe for Kari to carry; "the role Julian wants" is not.
3. Extract his read on Frank explicitly ("what would Frank need to see for the bigger version to be sign-able?") — intelligence + commitment escalation.
4. Give him one carryable sentence and test it live; simplify until he can say it fluently.
5. Arm him with the half-page for Frank: numbers-shaped, one page, no TOGAF vocabulary. A NEW artefact, not any existing prep doc.
6. Make the Frank timing his mission ("would Frank want to shape this before he goes?").

**What Julian must NOT do:** correct his framing; negotiate title/money with him; say a critical word about Tony / the sysadmin team / committee attendees; dump the governance machinery; ask him to advocate beyond his conviction (an over-pushed advocate goes silent — the consumed-but-not-converted death); lead with the deadline or let urgency smell like need.

## Related
- [[tti-kari-call-prep]] — the distilled talking bank (tactics folded in)
- [[tti-ea-governance-value]] — the full argument (Ty-grade; ration the machinery for Kari)
- [[tti-engagement-strategy]] — political read; Frank/Ty/Tony dynamics
