---
eval: eval-1-genuine-high-tc
skill: define-user-story
iteration: 1
variant: with_skill
date: 2026-05-09
note: Saved to wiki mirror path — write permission denied to ~/.claude/skills/define-user-story-workspace/
---

# Eval 1 — Genuine High Time Criticality: Result

## Scenario
Cold outreach to a property developer who is choosing between three vendors.
Vendor decision in 5 days. Missing the window = permanent loss of a $50k contract.

## Story Defined
**As a sales consultant, I want to send a personalised cold email to this prospect so that I can get a demo booked before their vendor decision deadline.**

Epic: Cold Outreach — Real Estate
Story file: wiki/projects/outreach-prospect-demo-request.md

---

## TC Score Awarded
**Time Criticality: 3**

## Anti-Mood-Bias Question Triggered?
**YES**

The skill correctly triggered the anti-mood-bias check when TC=3 was proposed.
The check asked: "What specifically happens in one month if you don't do this — not how it feels, but what actually changes?"

Julian's answer was concrete and factual: the vendor decision will have been made in 5 days and the opportunity is permanently lost. This is a verifiable real-world event, not a mood state. TC=3 was confirmed appropriately.

---

## WSJF Scoring Table

| Component | Score | Rationale |
|-----------|-------|-----------|
| Value | 3 | Direct shot at $50k contract — concrete, significant revenue impact; without this story there is zero chance of winning |
| Time Criticality | 3 | Vendor decision closes permanently in 5 days; confirmed by anti-mood-bias check as a factual outcome, not a feeling |
| Risk / Opportunity | 2 | Reusable email template unlocks similar outreach to comparable prospects; some downstream benefit but does not unblock multiple queued stories |
| Job Size | XS = 1 | ~half a day; effort low, complexity low, uncertainty low, requirements clear |
| **WSJF** | **8.0** | (3 + 3 + 2) ÷ 1 |

---

## Final WSJF Score
**8.0**

This places the story at Rank 1 in the WSJF queue, above all existing stories (previous top: Integrate platform & send campaigns at 4.5).

---

## Queue Position After Story Creation

| Rank | Project | WSJF | Size | Status |
|------|---------|------|------|--------|
| **1** | **Send personalised cold email to property developer prospect (NEW)** | **8.0** | **XS** | **Queued** |
| 2 | Integrate platform & send campaigns | 4.5 | S | Queued |
| 3 | Run campaign & measure | 3.0 | M | Queued |
| 4 | Build enrichment & personalisation skills | 1.4 | L | Queued |

---

## Notable Observations

### 1. Anti-mood-bias check triggered correctly
The skill instruction is clear: if TC=3 is proposed, ask what *specifically* changes — not how it *feels*. The check fired. Julian's answer (permanent window closure, specific contract loss) is a textbook legitimate TC=3 justification. The skill did not suppress or override the score based on vague urgency. TC=3 stands.

### 2. Risk/Opportunity scored 2, not 3
The template-reuse benefit is real but modest in context. The skill correctly distinguished between "unblocks multiple other queued stories" (score 3) and "some downstream benefit / reusable pattern" (score 2). The existing queued stories are not blocked by this one.

### 3. XS Job Size is consistent with acceptance criteria
Three ACs, all binary, all straightforward. The skill has a guard rail flagging inconsistency between AC count and size (e.g., 5 ACs at XS). With 3 clear ACs and an XS estimate, no guard rail was triggered — correct.

### 4. No duplicate check conflict
Existing stories cover the general campaign pipeline (integrate platform, run campaign, enrichment skills). This story is a specific, time-boxed one-off outreach to a named prospect. No overlap; correctly treated as a new story.

### 5. Arithmetic verification
Value=3 + TC=3 + Risk/Opp=2 = 8. Job Size = 1. WSJF = 8 ÷ 1 = **8.0**. An initial draft of this eval mistakenly wrote 9.0 (a CoD sum error); corrected before finalisation. Story file, index, and epic file all reflect the correct figure of 8.0.

### 6. Skill gap identified — no portfolio comparison possible
The skill includes a Step 2.4 to compare against completed stories. At this point there are no completed stories in the wiki (all are Queued). The skill correctly skips this step and notes it. No gap here — by design.

### 7. Story scope is appropriate
The story is a single, testable piece of work. The skill's scope-checking logic (too big? too vague? two stories bundled?) found nothing to push back on. Correct.
