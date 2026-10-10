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
Since 2026-09-27 each model is announced with its wiki section (Working with GenAI
/ yourself / others, The human mind), derived from its parent folder, in both the
terminal line and the instruction to Claude.
Since 2026-10-03 the script also runs a separate **feature review** on the same
rules: reference articles flagged `review: feature` in frontmatter are reviewed at
1, 7 and 30 days from their `review-start:` date, in their own queue
(`~/.claude/feature-daily-reminder-queue`) with their own cap of three per day,
shown in addition to the models; every 1-day review is always shown. On a quiet
day one flagged feature rotates in. Set up by [[claude-code-feature-articles]].
Since 2026-10-10 every refresher must be written in plain English for someone who
has not read the article (technical terms explained in a few words), after a
feature one-liner came out too cryptic to follow.

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
# Section label (Julian, 2026-09-27): every model is announced with the wiki
# section it comes from (Working with GenAI / yourself / others, The human
# mind), derived from its parent folder, so the refresher carries its context.
#
# Feature review (Julian, 2026-10-03): steering is a mental model, but each
# mechanism (hooks, rules, output styles, subagents, skills...) is a feature,
# documented as a reference article, not an mm card. Features get their own
# spaced repetition on the same rules, in a separate queue with its own cap of
# MAX_PER_DAY (shown in addition to the models). A file opts in with frontmatter
# `review: feature`; its 1/7/30-day clock runs from `review-start:` (not
# `created:`), so an older article joins the cycle on the day it is flagged.
# When no feature is due, one flagged feature rotates in by day-of-year.
# Queue line format as for models; queue file feature-daily-reminder-queue.
# WIKI and the state/queue paths derive from REFRESHER_WIKI / HOME so the
# script can be dry-run against a scratch copy without consuming the real day.
MAX_PER_DAY=3
EFF="-v-5H"
TODAY=$(date $EFF +%Y-%m-%d)
STATE="$HOME/.claude/mm-daily-reminder-last"
QUEUE="$HOME/.claude/mm-daily-reminder-queue"
FQUEUE="$HOME/.claude/feature-daily-reminder-queue"
[ "$(cat "$STATE" 2>/dev/null)" = "$TODAY" ] && exit 0
echo "$TODAY" > "$STATE"
touch "$QUEUE" "$FQUEUE"
WIKI="${REFRESHER_WIKI:-/Users/julianhart/Obsidian Vault/wiki}"
# awk function: wiki section label from a file path's parent folder.
SECFN='function sec(p,  d){d=p; sub(/\/[^\/]*$/,"",d); sub(/.*\//,"",d); if(d=="working-with-genai")return "Working with GenAI"; if(d=="working-with-yourself")return "Working with yourself"; if(d=="working-with-others")return "Working with others"; if(d=="the-human-mind")return "The human mind"; if(d=="claude-anthropic")return "Claude & Anthropic"; return d}'

# take_due QUEUEFILE: print today's items (every 1-day item, then 7-day and
# 30-day up to MAX_PER_DAY in total) and rewrite the queue with the rest.
take_due() {
  local Q="$1" SORTED ONE REST N1 SLOTS
  # Order: rung 1, then 7, then 30; oldest due date first within a rung.
  SORTED=$(sort -t'|' -k1,1n -k2,2 -k3,3 "$Q")
  ONE=$(printf '%s\n' "$SORTED" | grep '^1|')
  REST=$(printf '%s\n' "$SORTED" | grep -v '^1|')
  N1=$(printf '%s\n' "$ONE" | grep -c .)
  SLOTS=$((MAX_PER_DAY - N1)); [ "$SLOTS" -lt 0 ] && SLOTS=0
  printf '%s\n%s\n' "$ONE" "$(printf '%s\n' "$REST" | grep . | awk -v n="$SLOTS" 'NR<=n')" | grep .
  printf '%s\n' "$REST" | grep . | awk -v n="$SLOTS" 'NR>n' > "$Q"
}

# --- Mental models ---
# Append newly due files (skip a path already queued at the same rung).
for RUNG in 1 7 30; do
  D=$(date $EFF -v-${RUNG}d +%Y-%m-%d)
  grep -rlE "^created: $D" --include="mm-*.md" "$WIKI" 2>/dev/null | sort | while IFS= read -r f; do
    grep -qxF "$RUNG|$TODAY|$f" "$QUEUE" || grep -q "^$RUNG|[0-9-]*|$f\$" "$QUEUE" || echo "$RUNG|$TODAY|$f" >> "$QUEUE"
  done
done
if [ -s "$QUEUE" ]; then
  TAKE=$(take_due "$QUEUE")
  LEFT=$(grep -c . "$QUEUE")
  # Paths contain spaces (Obsidian Vault), so items are joined with "; ".
  DUE=$(printf '%s\n' "$TAKE" | awk -F'|' "$SECFN"'{printf "%s-day review (due %s, section: %s): %s; ", $1, $2, sec($3), $3}')
  NAMES=$(printf '%s\n' "$TAKE" | awk -F'|' "$SECFN"'{n=$3; sub(/.*\//,"",n); sub(/\.md$/,"",n); printf "%s(%sd, %s) ", n, $1, sec($3)}')
  SYS="Mental-model refresher (spaced repetition due): $NAMES($LEFT queued for later days)"
  MSG="Spaced-repetition refresher (first session of the day). These mental models are due review for retention, listed in priority order (1-day reviews first, then 7-day, then 30-day): $DUE Read each and open your first reply with a short refresher per model, naming the section it comes from first (section, one-liner, reach-for-when, one key principle), then handle the request as normal. Keep it short; $LEFT more are queued for later days."
else
  F=$(find "$WIKI" -name "mm-*.md" -not -path "*_archived*" | sort | awk -v n=$(date +%j) '{a[cnt++]=$0} END{print a[n%cnt]}')
  SEC=$(printf '%s\n' "x|x|$F" | awk -F'|' "$SECFN"'{print sec($3)}')
  SYS="Mental-model refresher today: $(basename "$F" .md) ($SEC)"
  MSG="Daily mental-model refresher (first session of the day): read $F (section: $SEC) and open your first reply with a two-to-three line refresher naming its section, then covering its one-liner, when to reach for it, and one key principle. Then handle the request as normal. Keep the refresher short."
fi

# --- Features ---
for RUNG in 1 7 30; do
  D=$(date $EFF -v-${RUNG}d +%Y-%m-%d)
  grep -rlE "^review-start: $D" --include="*.md" "$WIKI" 2>/dev/null | grep -v "_archived" | sort | while IFS= read -r f; do
    grep -q "^review: feature" "$f" || continue
    grep -qxF "$RUNG|$TODAY|$f" "$FQUEUE" || grep -q "^$RUNG|[0-9-]*|$f\$" "$FQUEUE" || echo "$RUNG|$TODAY|$f" >> "$FQUEUE"
  done
done
if [ -s "$FQUEUE" ]; then
  FTAKE=$(take_due "$FQUEUE")
  FLEFT=$(grep -c . "$FQUEUE")
  FDUE=$(printf '%s\n' "$FTAKE" | awk -F'|' "$SECFN"'{printf "%s-day review (due %s, section: %s): %s; ", $1, $2, sec($3), $3}')
  FNAMES=$(printf '%s\n' "$FTAKE" | awk -F'|' "$SECFN"'{n=$3; sub(/.*\//,"",n); sub(/\.md$/,"",n); printf "%s(%sd, %s) ", n, $1, sec($3)}')
  SYS="$SYS | Feature refresher (spaced repetition due): $FNAMES($FLEFT queued for later days)"
  MSG="$MSG Feature refresher: these feature articles are also due review, in priority order: $FDUE Read each and, after the mental-model refresher, add a short refresher per feature, naming its section first (section, what the feature is in one line, when to reach for it, one gotcha). Keep it short; $FLEFT more features are queued for later days."
else
  FF=$(grep -rl "^review: feature" --include="*.md" "$WIKI" 2>/dev/null | grep -v "_archived" | sort | awk -v n=$(date +%j) '{a[cnt++]=$0} END{if(cnt)print a[n%cnt]}')
  if [ -n "$FF" ]; then
    FSEC=$(printf '%s\n' "x|x|$FF" | awk -F'|' "$SECFN"'{print sec($3)}')
    SYS="$SYS | Feature refresher today: $(basename "$FF" .md) ($FSEC)"
    MSG="$MSG Daily feature refresher: also read $FF (section: $FSEC) and, after the mental-model refresher, add a two-line feature refresher naming its section, then what the feature is and one gotcha."
  fi
fi
# Plain-English rule (Julian, 2026-10-10): one-line refreshers compressed into
# jargon that only made sense after reading the article. Applies to every
# refresher, model and feature alike.
MSG="$MSG Write each refresher in plain English for someone who has not read the article: no unexplained technical terms, and if one is unavoidable, say what it means in a few words."
printf '{"systemMessage":"%s","hookSpecificOutput":{"hookEventName":"SessionStart","additionalContext":"%s"}}\n' "$SYS" "$MSG"
```
