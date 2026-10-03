---
type: task
created: 2026-10-03
status: in progress
tags: [working-with-genai, steering, claude-code, review]
---

# Claude Code Feature Articles

This is the fast-lane record for writing one reference article per Claude Code
steering mechanism that lacked one, and for giving those feature articles their own
spaced-repetition review alongside the mental-model refresher. It came out of a
3 Oct 2026 Q&A on routing, steering, path-scoped rules, output styles and subagents,
where Julian decided that steering is the mental model and each mechanism is a
feature, so features get reference articles in `wiki/technology/claude-anthropic/`
rather than `mm-` cards. It is read at sign-off (the criteria below) and for
calibration (the Time and Token Log).

**Admission:** fast lane, by Julian's decision (3 Oct 2026): "Just fast track it, my
decision." He did not state the why, criteria or assumption in his own words; the
lines below are the agent's, recorded as such.

**Outputs:**
- New feature articles: [[claude-code-path-rules]], [[claude-code-output-styles]],
  [[claude-code-subagents]], [[claude-code-skills]] (filenames agreed 3 Oct 2026)
- [[mm-steering]] Detail slot linked to all six feature articles
- Feature review added to `~/.claude/hooks/mm-daily-refresher.sh`: files flagged
  `review: feature` are reviewed at 1, 7 and 30 days from `review-start:`, own queue,
  max three per day with every 1-day review always shown; one feature rotates in on
  quiet days. Rules set by Julian 3 Oct 2026; flag, start-date and rotation are the
  agent's proposed defaults, adopted under the fast-track decision.

**Done when (agent's criteria):**
1. Each of the four articles exists, every factual claim traced to a current
   Claude Code doc URL.
2. The hook surfaces due feature articles in a test run without changing
   mental-model behaviour, and its wiki mirror matches.
3. Indexes, mirror, sync checklist and ops log updated.

**Load-bearing assumption:** Claude Code's current docs describe these features
accurately enough that the articles stay correct until the next harness change.

**Verifiers:** facts checked against the docs by a `claude-code-guide` subagent
before writing, then an adversarial pass by a second subagent on the written
articles; hook verified by a dry run in a scratch environment; Julian signs off.

## Time and Token Log

| Date | Segment | Who | Tokens / Minutes | Notes |
|------|---------|-----|------------------|-------|

## Session Synopsis

*(Filled at handback: Julian's rating and read first, then the model's comment.)*
