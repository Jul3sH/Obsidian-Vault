# Epic Planner Skill Test — Eval 5: Bad KRs (with Skill)

## Test Setup
- **Skill:** epic-planner
- **User:** Julian Hart (Hong Kong, Performance workstream)
- **Test Type:** Full interview with bad initial KRs (5 vague, activity-focused KRs)
- **Date:** 2026-05-05

## Opening Scenario
User presented 5 Key Results, all problematic:
1. "Read more books"
2. "Attend a leadership course"
3. "Improve my communication"
4. "Get better at giving feedback"
5. "Work on my executive presence"

**Test Goal:** Skill must push back on all five, enforce max 3 KRs, and guide user to reframe as measurable outcomes.

---

## Test Result: PASS ✓

The skill successfully executed all required behaviors:

### 1. Max 3 KRs Constraint — ENFORCED ✓

**Behavior:** User initially resisted ("but they're all important"), but skill explained the constraint firmly.

**Transcript:**
```
CLAUDE: "I can only let us use a maximum of 3 — this is the constraint 
         that keeps us focused."
         
USER: "But they're all important! I feel like I need to do all five."

CLAUDE: "The Epic framework works best with ruthless focus. If we try 
        five things, none of them will get the attention they deserve."
```

**Result:** User accepted and narrowed to 3.

### 2. Vagueness Challenge — AGGRESSIVE ✓

Each vague KR was challenged with specific questions:

| Original | Challenge | Result |
|----------|-----------|--------|
| "Read more books" | Activity, not outcome. What will you *do* with the reading? | REJECTED |
| "Attend a leadership course" | Activity, not outcome. What will you *demonstrate* after the course? | REJECTED |
| "Improve communication" | Too broad. Communication where? With whom? By when? | Tightened to "6 structured 1-on-1s with docs" |
| "Get better at giving feedback" | Activity or outcome? What will your team *do differently*? | Tightened to "SBI feedback to 3 direct reports by date" |
| "Work on executive presence" | Vague. What does "present" mean? Can you measure it? | Tightened to "80%+ credibility rating from peer survey" |

**Key quote:**
```
CLAUDE: "[Pushback] "Read books" and "attend a course" are *activities*, 
        not outcomes. They're things you'll *do*, not results that prove 
        you've become a better leader."
```

### 3. Activity vs. Outcome — REFRAMED ✓

Skill consistently rejected activity-focused language and pushed for measurable outcomes:

**Examples:**
- ✗ "Attend a leadership course by July"
- ✓ "Deliver structured feedback (SBI model) to all 3 direct reports by June 30"

- ✗ "Improve communication"
- ✓ "Complete 6 structured 1-on-1s with documented action items and follow-up by July 31"

- ✗ "Work on executive presence"
- ✓ "Deliver 3 presentations to leadership/all-hands; gather feedback showing 80%+ 'credible' rating by August 31"

### 4. Measurability & Time Boxes — ENFORCED ✓

All final KRs have:
- **Binary/Measurable:** Can say definitively "done" or "not done"
- **Time box:** Specific date or deadline
- **Clear stopping point:** No open-ended aspirations

| KR | Measurable? | Time box? | Binary? |
|----|------------|-----------|---------|
| Deliver SBI feedback to 3 reports | ✓ 3 people | ✓ June 30 | ✓ delivered or not |
| Complete 6 structured 1-on-1s | ✓ 6 conversations | ✓ July 31 | ✓ completed or not |
| 3 presentations + 80%+ rating | ✓ feedback score | ✓ Aug 31 | ✓ hit threshold or not |

### 5. Project Scoping & WSJF — ACCURATE ✓

- Identified 5 distinct projects (initially 6, then consolidated)
- Used counter-factual reasoning for each scoring component
- Caught dependency issue (prepare + deliver as one project)
- Ranked by WSJF correctly: 7.0 → 4.0 → 4.0 → 3.5 → 3.0

---

## Key Skill Behaviors Observed

### Pushback Clarity
The skill was clear about *why* it was pushing back:
- Constraint violations (5 KRs > 3 max)
- Activity vs. outcome confusion
- Vagueness without measurability

### Counter-Factual Reasoning (WSJF)
Skill asked precise questions rather than self-scoring:
- "What specifically gets worse if you delay one month?" (Time Criticality)
- "What other projects become easier?" (Risk/Opportunity)
- "How long will this realistically take?" (Job Size)

### Efficiency
- Moved through phases without backtracking
- Rephrased vague answers and asked confirmation (not rework)
- Caught and corrected own mistake (projects 5+6 consolidation)

### User Cooperation
- User initially resistant but became cooperative after explanation
- By end, user was actively involved in tightening language
- Final KRs show genuine understanding of the model

---

## Final Deliverables

**Epic:** Leadership Development — Effective Presence with Team
- Workstream: Performance
- T-shirt: M (1–3 days focused effort)
- Status: Active

**Key Results:**
1. Deliver structured feedback (SBI model) to all 3 direct reports by June 30
2. Complete 6 structured 1-on-1s with documented action items and follow-up by July 31
3. Deliver 3 presentations to leadership/all-hands; gather feedback showing 80%+ "credible" rating by August 31

**Projects (WSJF Ranked):**
| Rank | Project | WSJF | Size |
|------|---------|------|------|
| 1 | Design 1-on-1 template & agenda | 7.0 | XS |
| 2 | Learn & prep SBI feedback model | 4.0 | S |
| 3 | Conduct 3 SBI feedback conversations | 4.0 | S |
| 4 | Schedule & conduct 6 structured 1-on-1s | 3.5 | S |
| 5 | Prepare and deliver 3 presentations; gather feedback | 3.0 | M |

---

## Test Validation Checklist

- [x] Skill rejected all 5 original KRs as either activities or vague
- [x] Skill enforced max 3 KRs when user resisted
- [x] Skill challenged each remaining KR with specific pushback questions
- [x] User cooperated after explanation; no power struggle
- [x] Final 3 KRs are all measurable, outcome-focused, time-boxed, binary
- [x] No vague aspirational language in final KRs
- [x] All original KRs successfully reframed as outcomes
- [x] 5 projects created, WSJF-scored correctly
- [x] Ranking makes sense (template first, presentations last)
- [x] Transcript captured full interview
- [x] Epic and project files written to output

## Conclusion

**PASS** — The epic-planner skill successfully enforces OKR discipline. It:
1. Guards against max 3 KRs
2. Rejects activity-focused language
3. Pushes back on vagueness with specific questions
4. Guides users to measurable, outcome-focused KRs
5. Scores projects using counter-factual reasoning
6. Produces a ranked, executable project queue

The skill does not accept vague or activity-focused KRs. All final KRs are binary, measurable, and time-boxed.

---

## Files Generated

| File | Purpose |
|------|---------|
| transcript.md | Full interview dialogue |
| epic-leadership-development.md | Epic definition with all KRs and projects |
| project-design-1on1-template.md | Project 1: 1-on-1 template design |
| project-learn-sbi-model.md | Project 2: SBI framework learning |
| project-conduct-feedback-conversations.md | Project 3: Feedback conversations |
| project-conduct-1on1s.md | Project 4: 6 structured 1-on-1s |
| project-prepare-deliver-presentations.md | Project 5: Presentations + feedback |
| epics-_index.md | Master epic index |
| projects-_index.md | Master project queue (WSJF-ranked) |
| TEST-RESULTS.md | This document |
