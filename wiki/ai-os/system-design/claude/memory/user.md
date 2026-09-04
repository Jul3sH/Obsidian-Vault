---
name: user-profile
description: "Who Julian is, how he works, key context for every session"
metadata: 
  node_type: memory
  type: user
  created: 2026-05-08
  updated: 2026-07-12
  originSessionId: 12afdf14-c34c-4380-83e6-424aa676a1bb
  modified: 2026-08-08T11:25:45.475Z
---

# Julian

## Identity
- Email: julianhart@gmail.com
- Location: UK (as of Sep 2026, confirmed 3 Sep) - relocated from Hong Kong; day starts early, ~5 AM UK
- Solo operator - works alone, no team

## Family
- Daughter: Sophia (12, moves to UK with Julian; school year boundary Aug 2027)
- Mother: daily 5:30 AM call; lives in Malvern, Worcestershire

## Psychological Fingerprint

These four traits are always in play. They shape how Claude should communicate and what guardrails to apply.

| Trait | What it means in practice |
|-------|--------------------------|
| **Visual thinker** | Tables and registers outperform prose; needs trade-offs spatially in one place to connect dots; summaries that list separately instead of showing side-by-side lose him |
| **ADHD** | Analysis is the strength, commitment is the weak link; stalls without a forcing function; hyper-focus activates once genuinely started; research loops and scope creep are the main failure modes |
| **Loss-averse** | Financial security is the master emotion (downstream of divorce + cancer); naming and accepting the worst case unlocks him from the freeze; "you're a survivor, it works out" is a valid counter-move |
| **ENTP wiring** | Option-closing feels like loss; watch for manufactured third options that are really deferral in disguise; performs best under genuine external deadlines |

### Execution-first, always (added 2026-08-08)

Julian needs **something real to deliver against within days**. Extended analysis or discovery phases are not merely unpleasant for him - they are actively counterproductive. In his own words: *"I'm terrible at navel-gazing, and a month for me of analysis could be terrible. I just go all over the place and get lost."*

**How to apply:** design engagements, deliverables and sprints so execution starts immediately and learning is a **by-product of delivering**, never a phase that precedes it. When a piece of work seems to require a discovery or baselining period, find the smallest real thing that can be delivered in parallel and lead with that. A plan whose first phase is "assess / align / diagnose" is a plan he will lose direction inside.

This is the operating-style counterpart to the ADHD row above: hyper-focus activates once genuinely started, so the design goal is to shorten the distance to started.

## Context Loader

When a conversation topic matches a trigger below, load the corresponding wiki file before responding.

| Trigger | Load |
|---------|------|
| Making, reviewing, or structuring a decision | `wiki/performance/decision-journal/decision-maker-profile.md` |
| Commitment, locking a choice, wobbling on a settled question | `wiki/performance/working-with-yourself/commitment-avoidance.md` |
| Planning work, prioritising, managing focus or capacity | `wiki/performance/working-with-yourself/adhd-aware-work-patterns.md` |

## Operating Model
- 8-hour daily focus capacity (7-12 PM + 1-4 PM, or 8-12 PM + 1-4 PM if running)
- 40-hour weekly sprint capacity (1 SP = 1 hour)
- Sprint cadence: 1 week (Mon-Sun)
- Ceremonies: standup 4 PM weekdays, retro Sundays (SessionStart hook prompts it), sprint-plan manual
- Runs occasionally (impacts morning schedule)

## Preferences
- Concise, direct responses - no trailing summaries
- Cost-first decision-making over qualitative anchoring
- Structural guardrails over willpower (DoD gates, capacity caps, ceremony cadence)

## Workstreams
career, finance, performance, personal, relationships, wellbeing
(6 workstreams - see `wiki/_master-index.md` for full structure. Technology is a reference library, not a workstream.)

## Tooling
- Primary: Claude Code + Obsidian wiki
- Project management: Jira (project BWS - Development Sprints)
- Calendar: Google Calendar (primary)
- Credentials: `~/.leadgen/credentials.json` (chmod 600)

## Environment Quirks (Hong Kong - historical; UK-based as of Sep 2026, likely stale)
- Anthropic API requires VPN (blocked in HK on direct connection)
- RapidAPI must bypass VPN (blocks VPN exit IPs)
- ExpressVPN configured with reverse bypass
