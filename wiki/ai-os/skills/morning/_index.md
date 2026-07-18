---
type: skill-index
created: 2026-05-07
skill-path: ~/.claude/skills/morning/SKILL.md
---

# Morning Skill

On-demand daily plan generator (`/morning`). Fetches live sprint status from Jira first, cross-references wiki for WSJF scores, maps remaining sprint work to your daily focus capacity (adjusted for disruptions), checks Google Calendar for conflicts, and populates your calendar with the plan.

## What It Does

0. **Fetches live sprint from Jira** — Queries `project = BWS AND sprint in openSprints()`, filters out Done stories. In Progress stories go to the top of the plan; To Do stories follow in WSJF order. This ensures the plan reflects ground truth, not a potentially stale wiki.
1. **Cross-references WSJF scores** — Merges Jira story status with wiki WSJF scores to produce a single ordered working list.
2. **Asks about disruptions** — "Are there any disruptions to your ideal day profile?" Recalculates focus capacity based on running, gym, lunch meetings, etc.
3. **Checks for calendar conflicts** — Scans Google Calendar for events 7 AM–4 PM.
4. **Detects calendar disruptions** — If a meeting exists, asks: "Do we need to adjust your ideal day?"
5. **Maps stories to time blocks** — Allocates remaining sprint work to adjusted focus blocks:
   - Morning: 7–12 PM (5h) or 8–12 PM (4h if disruption)
   - Afternoon: 1–4 PM (3h)
6. **Populates Google Calendar** — Creates events for each allocated story with WSJF score, hours, Jira key, and status in the description.
7. **Presents a summary** — Shows sprint status, what was scheduled, what's queued for tomorrow, and disruption/conflict status.

## Ideal Day Template

**Fixed blocks (not managed by skill):**
- 5:00–5:30 AM: Wake up, personal
- 5:30–6:00 AM: Call with mum
- 6:00–7:00 AM: Admin + Sophia school prep (external calendar, ignored)
- 12:00–1:00 PM: Lunch + admin (external calendar, ignored)

**Focus work (managed by skill):**
- **Default (no disruptions):** 7 AM–12 PM (5h) + 1–4 PM (3h) = **8h**
- **With disruptions (running, gym, etc.):** 8 AM–12 PM (4h) + 1–4 PM (3h) = **7h**
- **Multiple disruptions:** Capacity adjusted based on sum of disruption times

**After 4 PM:** Flexible. Only schedule additional work if the daily target (7h or 8h) wasn't hit due to morning disruptions.

## Trigger & Scheduling

| Trigger | Type | Time |
|---------|------|------|
| Manual | `/morning` | On demand, anytime |
| Automatic | Cron | 6 AM HKT, every day |

Runs before `/standup` (6 AM standup ceremony) so you can review your calendar during standup prep.

## Key Files

- **Skill:** `~/.claude/skills/morning/SKILL.md`
- **Configuration:** `~/.claude/skills/morning/ideal-day-template.json`
- **Sprint status:** Jira (agileict.atlassian.net, Cloud ID: bbbb75d2-e2e4-44fe-a329-e506d1128c29, project BWS) — fetched live
- **WSJF scores:** `wiki/projects/_index.md` — cross-reference only; Jira is primary
- **Calendar target:** Google Calendar (primary calendar)
- **Reference:** `wiki/ai-os/service-design/project-workflow.md` (capacity model)

## Design Principles

1. **Jira is primary, wiki is secondary.** Sprint status comes from Jira (live). The wiki provides WSJF scores only. Stale wiki data never causes the plan to include already-completed work.

2. **Finish what's started.** In Progress stories always go to the top of the day's allocation. Context-switching debt from carrying over half-finished work is worse than starting something new.

3. **Capacity is a hard limit.** 8 hours (or less with disruptions) is the daily focus budget. Stories exceeding capacity are queued for tomorrow; no over-commitment.

4. **Disruptions are proactively captured.** The skill asks "Are there any disruptions?" at the start — running, gym, lunch meetings, or any deviations. Capacity adjusts automatically.

5. **WSJF ranks the remaining work.** After In Progress stories, To Do stories are ordered by WSJF score. Mood-driven re-ordering is deferred to sprint planning.

6. **Calendar conflicts are detected, not assumed away.** If a meeting appears overnight, the skill asks: "Adjust the plan?" rather than silently re-mapping.

7. **Google Calendar is the output.** No separate plan.md; your calendar IS your daily plan.

## Typical Run

**6:00 AM HKT:**
```
→ Are there any disruptions to your ideal day profile? None
→ Fetching WSJF queue...
→ Checking Google Calendar for 7 AM–4 PM...
→ No conflicts detected ✓

Morning Plan — Wednesday, 7 May 2026
────────────────────────────────────
Disruptions: None
Available Focus: 8 hours (7 AM–12 PM, 1–4 PM)

CALENDAR POPULATED:
 7:00–9:00 AM   [WSJF 4.5] Integrate Platform (2h/8h) ✓
 9:00–12:00 PM  [WSJF 4.5] Integrate Platform (3h/8h) ✓
 1:00–4:00 PM   [WSJF 4.5] Integrate Platform (3h/8h) ✓
                            Subtotal: 8h ALLOCATED

QUEUED FOR TOMORROW:
 2. [WSJF 3.0] Run Campaign & Measure (16h total)
 3. [WSJF 1.4] Build Enrichment Skills (40h total)

→ Calendar updated. Review before standup.
```

## Related Skills

- **`/sprint-plan`** — Weekly capacity planning for the sprint (40h/week)
- **`/standup`** — Daily 5-min ceremony at 6 AM HKT (after morning plan)
- **`/retro`** — Weekly retrospective (4 PM Friday)
- **`/project-planner`** — Define new Projects and break into WSJF-scored deliverables

## Key Takeaways

- Runs automatically at 6 AM before standup; reduces decision load at start of day
- Capacity = 8h/day (adjusted for any disruptions); WSJF-ranked projects allocated first
- Disruptions (running, gym, lunch meetings, etc.) are asked about upfront and recalculate capacity
- Calendar conflicts are detected and trigger a decision point, not a failure
- Output is Google Calendar; no separate plan file

## Links

- **Project Workflow:** [[../../../service-design/project-workflow|Project Workflow]] — capacity, timebox structure, ceremonies
- **Projects Index:** [[../../../projects/_index|Projects]] — WSJF-ranked queue
- **Ceremonies:** [[../sprint-plan/_index|Sprint Plan]], [[../standup/_index|Standup]], [[../retro/_index|Retro]]
