> Mirror copy. Source: `~/.claude/hooks/mm-daily-refresher.sh` (hidden path).
> Update this mirror whenever the source changes.

# mm-daily-refresher.sh

SessionStart hook script: first session of each effective day (05:00 UK
boundary), either the spaced-repetition review of mental models created exactly
1 day / 1 week / 1 month ago, or one rotating model from the whole vault.
Emits a visible `systemMessage` in the terminal (added 2026-09-19) so Julian
sees every firing, plus the `additionalContext` instruction Claude acts on.
Since 2026-09-25 due models go into a queue at `~/.claude/mm-daily-reminder-queue`
(line format `rung|due-date|path`). Rung priority: every 1-day review is shown on
its day regardless of the cap; 7-day then 30-day reviews fill the remaining slots
up to three per day; the rest roll forward. Rationale: compounding makes the 1-day
review the one that must never be missed, the 7-day can slip a day or two, the
30-day up to a week. The queue exists because a 38-model batch created on 26 Aug
came due together on 25 Sep, which is unlearnable.

```bash
#!/bin/bash
# Daily mental-model refresher (SessionStart hook).
# Purpose: Julian learns his mental models through repeated visible reminders.
# The refresher must therefore appear IN HIS TERMINAL every time it fires: the
# JSON output carries both a systemMessage (the visible terminal line, proof
# the hook ran) and additionalContext (the instruction Claude acts on). Without
# the systemMessage, a firing consumed by a resume/clear/compact session start
# is silently swallowed and the day's reminder is lost.
# Day boundary is 05:00 UK local time (Julian is UK-based, up early): all date
# arithmetic subtracts 5h so a 00:30 session belongs to the previous day.
#
# Priority 1 (spaced repetition): mm-*.md files created exactly 1, 7, or 30
# days ago (frontmatter `created:`) become due and are appended to a queue.
# Queue line format: rung|due-date|path  (rung = 1, 7 or 30).
# Rung priority (Julian, 2026-09-25): compounding makes the 1-day review the
# one that must never be missed, the 7-day can slip a day or two, the 30-day
# up to a week. So:
#   - every 1-day item is shown on its day, regardless of the cap;
#   - the remaining slots up to MAX_PER_DAY go to 7-day items, then 30-day;
#   - anything not shown rolls forward, oldest due date first within a rung.
# The queue exists because a 38-file batch created on one day came due
# together 30 days later (25 Sep 2026), which is unlearnable.
# Priority 2 (rotation): when the queue is empty, pick one mm file by
# day-of-year for the periodic whole-vault cycle.
# Fires once per effective day via a state file.
MAX_PER_DAY=3
EFF="-v-5H"
TODAY=$(date $EFF +%Y-%m-%d)
STATE="$HOME/.claude/mm-daily-reminder-last"
QUEUE="$HOME/.claude/mm-daily-reminder-queue"
[ "$(cat "$STATE" 2>/dev/null)" = "$TODAY" ] && exit 0
echo "$TODAY" > "$STATE"
touch "$QUEUE"
WIKI="/Users/julianhart/Obsidian Vault/wiki"
# Append newly due files (skip a path already queued at the same rung).
for RUNG in 1 7 30; do
  D=$(date $EFF -v-${RUNG}d +%Y-%m-%d)
  grep -rlE "^created: $D" --include="mm-*.md" "$WIKI" 2>/dev/null | sort | while IFS= read -r f; do
    grep -qxF "$RUNG|$TODAY|$f" "$QUEUE" || grep -q "^$RUNG|[0-9-]*|$f\$" "$QUEUE" || echo "$RUNG|$TODAY|$f" >> "$QUEUE"
  done
done
if [ -s "$QUEUE" ]; then
  # Order: rung 1, then 7, then 30; oldest due date first within a rung.
  SORTED=$(sort -t'|' -k1,1n -k2,2 -k3,3 "$QUEUE")
  ONE=$(printf '%s\n' "$SORTED" | grep '^1|')
  REST=$(printf '%s\n' "$SORTED" | grep -v '^1|')
  N1=$(printf '%s\n' "$ONE" | grep -c .)
  SLOTS=$((MAX_PER_DAY - N1)); [ "$SLOTS" -lt 0 ] && SLOTS=0
  TAKE=$(printf '%s\n%s\n' "$ONE" "$(printf '%s\n' "$REST" | grep . | awk -v n="$SLOTS" 'NR<=n')" | grep .)
  printf '%s\n' "$REST" | grep . | awk -v n="$SLOTS" 'NR>n' > "$QUEUE"
  LEFT=$(grep -c . "$QUEUE")
  # Paths contain spaces (Obsidian Vault), so items are joined with "; ".
  DUE=$(printf '%s\n' "$TAKE" | awk -F'|' '{printf "%s-day review (due %s): %s; ", $1, $2, $3}')
  NAMES=$(printf '%s\n' "$TAKE" | awk -F'|' '{n=$3; sub(/.*\//,"",n); sub(/\.md$/,"",n); printf "%s(%sd) ", n, $1}')
  SYS="Mental-model refresher (spaced repetition due): $NAMES($LEFT queued for later days)"
  MSG="Spaced-repetition refresher (first session of the day). These mental models are due review for retention, listed in priority order (1-day reviews first, then 7-day, then 30-day): $DUE Read each and open your first reply with a short refresher per model (one-liner, reach-for-when, one key principle), then handle the request as normal. Keep it short; $LEFT more are queued for later days."
else
  F=$(find "$WIKI" -name "mm-*.md" -not -path "*_archived*" | sort | awk -v n=$(date +%j) '{a[cnt++]=$0} END{print a[n%cnt]}')
  SYS="Mental-model refresher today: $(basename "$F" .md)"
  MSG="Daily mental-model refresher (first session of the day): read $F and open your first reply with a two-to-three line refresher covering its one-liner, when to reach for it, and one key principle. Then handle the request as normal. Keep the refresher short."
fi
printf '{"systemMessage":"%s","hookSpecificOutput":{"hookEventName":"SessionStart","additionalContext":"%s"}}\n' "$SYS" "$MSG"
```
