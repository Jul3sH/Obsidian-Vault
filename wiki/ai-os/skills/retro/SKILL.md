---
name: retro
description: >
  Weekly retrospective ceremony. Runs at 4 PM HKT every Sunday. Hard-capped at
  20 minutes. Reads the closing sprint from Jira and this week's standup log,
  presents a sprint summary, asks for 1 win / 1 problem / 1 change, logs the
  retro, and optionally actions the change. Run manually with /retro anytime.
---

# Retro Skill — Weekly Retrospective

Runs at 4 PM HKT every Sunday to close out the sprint. Hard time-box: 20
minutes. The purpose is identification and logging — not resolution. Resolution
happens in sprint planning.

**Format:** 1 win. 1 problem. 1 change. That's it.

---

## Connection Details

- **Site:** agileict.atlassian.net
- **Cloud ID:** `bbbb75d2-e2e4-44fe-a329-e506d1128c29`
- **Board:** BWS (Development Sprints)

---

## Step 1 — Fetch Sprint Data

**JQL — completed stories:**
```
project = BWS AND sprint in openSprints() ORDER BY status ASC
```

Use `searchJiraIssuesUsingJql`. Extract for each story:
- Key, Summary, Status, Story points (`customfield_10016`)

**Also read this week's standup entries** from `wiki/ai-os/logs/standup-log.md`
— last 5 rows max. This gives context on what happened day-to-day without
requiring the user to recap everything.

---

## Step 2 — Present Sprint Summary

```
Weekly Retrospective — [Sprint Name]
═══════════════════════════════════════════════
⏱  Time box: 20 minutes. One sentence per answer.

SPRINT SUMMARY:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  ✓  BWS-2  Integrate Platform & Send Campaigns    2 SP   Done
  →  BWS-3  Run Campaign & Measure                3 SP   In Progress
  ○  BWS-4  Build Enrichment Skills               5 SP   To Do
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  Committed: 10 SP  |  Completed: 2 SP  |  Velocity this sprint: 2
  Carried forward: BWS-3 (3 SP), BWS-4 (5 SP)
```

If standup log has entries this week, show a one-line summary:
```
This week's standups: Mon no progress | Tue BWS-2 done | Wed–Fri BWS-3 in progress
```

**Scope creep signal check (data-driven, before asking questions):**
- Check standup log for any entries where scope creep was noted
- If any In Progress or incomplete story has consumed significantly more hours than estimated (e.g. an 8h story still incomplete after 12h of a sprint): flag it
- Display a brief signal line if either is true:
```
⚠️  Scope signal: BWS-3 was estimated at 3 SP and is still incomplete after a full sprint.
    This may indicate scope expanded beyond the original Definition of Done.
```
- If no signal: omit this line entirely — don't manufacture issues

---

## Step 3 — Ask 3 Questions

Ask all three in one message. One sentence per answer — enforce this gently if
the user starts writing an essay:

```
Three questions — one sentence each:

1. What's your one WIN this sprint?
2. What's the one PROBLEM that got in the way?
3. What's the one CHANGE you'll make next sprint?
```

**If the user writes more than 2–3 sentences on any answer:**
"Let's keep it tight — can you distill that to one sentence? The detail can go
in the log if needed, but the headline is what matters."

**The change must be specific and actionable.** Push back on vague changes:
- Too vague: "Be more focused"
- Better: "Block 7–12 AM on calendar as focus time; decline all calls before noon"

**Scope creep follow-up (only if the signal was flagged in Step 2):**
After the three questions, add one targeted probe — do not ask this if no scope signal was detected:

```
One more: the sprint data suggests [BWS-X] may have expanded beyond its original
scope. Did the story deliver exactly what the Definition of Done described,
or did it grow during the sprint?
```

Use the answer to inform whether the "1 change" should address DoD discipline at sprint planning.
If scope creep is confirmed, push for a specific change: not "write better DoDs" but
"at next sprint planning, I'll write the DoD for each story before estimating hours."

**Payoff probe (only if the sprint contained Career or Performance stories):**
After the three questions, ask one question:

```
Last one: what did you spend time on this week that you couldn't invoice for,
or point at a deliverable it made faster?
```

This is the backward-looking half of the payoff gate, and it is the one that
actually catches what slipped through — the definition-time gate is easy to
rubber-stamp when Julian already wants to do the work. Ask it plainly and do not
soften the answer.

If the honest answer is "a fair bit", do not moralise. Turn it into the "1
change" with a specific mechanism, e.g. "next sprint, no Career or Performance
story enters the sprint without a named buyer or two named deliverables it
leverages." Recurrence across two or more consecutive retros is the signal that
the gate itself is being routed around — say so directly, and check whether the
5 SP speculative cap is holding.

Background: `wiki/performance/working-with-yourself/payoff-vs-prestige-bias.md`.

---

## Step 3.5 — Systems-Register Check

**Every retro** (weekly - monthly proved too long, context of the week's work is lost):
open `wiki/performance/systems-register.md` and walk the rows in one message:

```
Monthly systems check. Register status:
- [SYS-n System] — [Status], last used [date]
...
Any row to move? (re-adopt with a forcing-function / retire / no change)
```

- Update `Last used` and `Status` for each row per Julian's answers.
- A **New** row older than two weeks with no real use moves to **Abandoned** —
  say so plainly rather than letting it sit.
- Any change is one line each; do not let this exceed ~2 minutes of the retro. Rows unchanged since last week need no discussion - list them on one line.
- Update the register file in the same operation, and bump its `updated:` date.

## Step 4 — Log and Close

**Append one row to `wiki/ai-os/logs/retro-log.md`:**

```
| [date] | [sprint name] | [committed SP] | [completed SP] | [velocity] | [win] | [problem] | [change] |
```

**Update completed stories in `wiki/projects/`:**
For each story marked Done this sprint, update its `.md` file:
- Set `status: completed`
- Add `completed: [date]`
- Add `actual-points: [original estimate]` (or adjusted if the story was
  re-estimated mid-sprint due to significant scope discovery)

This builds the portfolio that `/define-user-story` and `/define-enabler` use
for relative comparison during future estimation.

**If a completed story closes out its parent Project (Project reaches `done`):**
Update the Project's row in `wiki/ai-os/service-design/estimation-baseline.md`:
- Fill **Actual hrs** (sum the actual effort across the Project's delivered stories).
- Compute **Variance** against both the top-down t-shirt band and the scoped estimate.
- Add one line of **learning** (e.g. "build-from-blueprint ran 1.6x the M estimate; size these L in future").
This is what makes the baseline calibrate future sizing rather than just recording it. See [[estimation-baseline|Estimation Baseline]].

**Calculate and display velocity:**
```
VELOCITY:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  This sprint:    2 SP completed
  Last 3 sprints: [N] SP avg  (or "not enough data" if < 3 sprints)
  Trend:          ↑ improving / → stable / ↓ declining
```

Read `wiki/ai-os/logs/retro-log.md` to calculate the rolling 3-sprint average.
If fewer than 3 sprints exist, show what's available and note the data gap.

**Final output:**
```
Retro logged. ✓

  Win:      [one sentence]
  Problem:  [one sentence]
  Change:   [one sentence]

Sprint velocity: 2 SP (committed 10 SP)
Rolling avg (last 3): [N] SP
Carried to next sprint: BWS-3 (3 SP), BWS-4 (5 SP)
```

---

## Step 5 — Action the Change (Optional)

Ask: "Does the change need actioning before sprint planning?"

**If yes, ask what type:**
- **Jira story** → create a new story in BWS backlog via `createJiraIssue` with
  the change as the summary; assign appropriate priority and story points
- **Process update** → ask what to update (CLAUDE.md, a wiki article, a skill);
  make the edit
- **Nothing yet** → log it and done; the change is captured for next sprint's
  planning discussion

**If no:** done.

---

## Edge Cases

**No active sprint:**
- Tell the user there's no open sprint to retro. Ask if they want to run
  `/sprint-plan` to start a new one.

**Sprint has zero completed stories:**
- Show the summary honestly. Don't soften it.
- The 1-win question still applies — even a week with no Jira progress had
  something go right (a conversation, a learning, a decision made).

**Retro run mid-week (manual):**
- Runs identically but note it's a mid-sprint retro in the log entry.

**User wants to dig into the problem:**
- Gently redirect: "Let's capture it and take it to sprint planning. The retro
  is for identification, not resolution."

---

## Configuration & Scheduling

**Trigger mechanism (SessionStart hook, `.claude/settings.json` in the vault):**
On any session opened on a Sunday, if `wiki/ai-os/logs/retro-log.md` has no entry
dated today, the hook injects a reminder and Claude prompts Julian once to run
`/retro`. No phone, no cron, no memory required - the harness executes it. Sunday
is sprint day, so the retro fires whether or not a sprint actually ran.

**Trigger Phrases:**
- `/retro` — manual run anytime

---

## Key Files & Links

- **Retro Log:** `wiki/ai-os/logs/retro-log.md`
- **Standup Log:** `wiki/ai-os/logs/standup-log.md` (context for the week)
- **Jira Board:** https://agileict.atlassian.net/jira/software/projects/BWS/boards
- **Wiki Documentation:** `wiki/ai-os/skills/retro/_index.md`
