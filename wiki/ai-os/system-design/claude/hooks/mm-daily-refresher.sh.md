> Mirror copy. Source: `~/.claude/hooks/mm-daily-refresher.sh` (hidden path).
> Update this mirror whenever the source changes.

# mm-daily-refresher.sh

SessionStart hook script: first session of each effective day (05:00 UK
boundary), either the spaced-repetition review of mental models created exactly
1 day / 1 week / 1 month ago, or one rotating model from the whole vault.

```bash
#!/bin/bash
# Daily mental-model refresher (SessionStart hook).
# Day boundary is 05:00 UK local time (Julian is UK-based, up early): all date
# arithmetic subtracts 5h so a 00:30 session belongs to the previous day.
# Priority 1 (spaced repetition): mm-*.md files created exactly 1 day, 7 days,
# or 30 days ago (frontmatter `created:`) are due review - all of them.
# Priority 2 (rotation): otherwise pick one mm file by day-of-year for the
# periodic whole-vault cycle. Fires once per effective day via a state file.
EFF="-v-5H"
TODAY=$(date $EFF +%Y-%m-%d)
STATE="$HOME/.claude/mm-daily-reminder-last"
[ "$(cat "$STATE" 2>/dev/null)" = "$TODAY" ] && exit 0
echo "$TODAY" > "$STATE"
WIKI="/Users/julianhart/Obsidian Vault/wiki"
D1=$(date $EFF -v-1d +%Y-%m-%d); D7=$(date $EFF -v-7d +%Y-%m-%d); D30=$(date $EFF -v-30d +%Y-%m-%d)
DUE=$(grep -rlE "^created: ($D1|$D7|$D30)" --include="mm-*.md" "$WIKI" 2>/dev/null | sort | tr '\n' ' ')
if [ -n "$DUE" ]; then
  MSG="Spaced-repetition refresher (first session of the day): these mental models were created exactly 1 day, 1 week, or 1 month ago and are due review for retention: $DUE Read each and open your first reply with a short refresher per model (one-liner, reach-for-when, one key principle), then handle the request as normal."
else
  F=$(find "$WIKI" -name "mm-*.md" -not -path "*_archived*" | sort | awk -v n=$(date +%j) '{a[cnt++]=$0} END{print a[n%cnt]}')
  MSG="Daily mental-model refresher (first session of the day): read $F and open your first reply with a two-to-three line refresher covering its one-liner, when to reach for it, and one key principle. Then handle the request as normal. Keep the refresher short."
fi
printf '{"hookSpecificOutput":{"hookEventName":"SessionStart","additionalContext":"%s"}}\n' "$MSG"

```
