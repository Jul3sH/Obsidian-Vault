> Mirror copy, exact. Source: `~/.claude/skills/whatsapp-someday/scripts/run_weekly.sh`
> Stored as Markdown per skill-conventions (scripts are never stored as raw executable files in the wiki).

```bash
#!/bin/zsh
# whatsapp-someday weekly runner - invoked by launchd (com.julianhart.whatsapp-someday)
# Mirrored at wiki/ai-os/system-design/claude/local-automation.md - keep both in sync.
#
# Created with Julian's explicit, specific consent (2026-08-15, in-conversation): a
# persistent local launchd job invoking Claude Code headlessly and unattended on
# Saturdays, no human watching each action, scoped tool allowlist rather than a
# full permission bypass.
#
# Fires on several checkpoints across Saturday (plus RunAtLoad on every login) so it
# doesn't depend on the laptop being on at one exact time. Step 0's file-move makes
# reruns idempotent, so firing more than once on a Saturday is harmless.
#
# No permission bypass is used. Only the specific tools this skill actually needs
# are pre-allowed via --allowedTools; anything outside that scope would prompt, and
# since nobody is present to answer, `timeout` kills the run rather than letting it
# hang - a failed/skipped week is logged and safe, never a silent bypass.

set -uo pipefail

VAULT="/Users/julianhart/Obsidian Vault"
DROPFOLDER="$HOME/Library/CloudStorage/Dropbox/5-Performance/Whatsapp someday"
LOGDIR="$HOME/.claude/skills/whatsapp-someday/logs"
CLAUDE_BIN="/Users/julianhart/.local/bin/claude"
TIMEOUT_SECS=2700   # 45 min ceiling - this run fetches ~100+ URLs one at a time
RUNLOG="$VAULT/wiki/ai-os/logs/whatsapp-someday-runs.md"

mkdir -p "$LOGDIR"
STAMP=$(date "+%Y-%m-%d_%H%M%S")
TODAY=$(date "+%Y-%m-%d")
LOGFILE="$LOGDIR/run_$STAMP.log"

# Appends one compliance row to the vault-tracked run log, written by this script
# directly (plain file I/O, no Claude tool permissions involved) so a row lands
# here even if the inner headless Claude session never finishes.
record_outcome() {
  local outcome="$1" detail="$2"
  printf '| %s | %s | %s |\n' "$TODAY" "$outcome" "$detail" >> "$RUNLOG" 2>/dev/null
}

# macOS has no built-in `timeout` (that's a GNU coreutils command, not part of BSD/macOS
# by default - found the hard way, the first real test run errored out instantly with
# "command not found" before Claude was ever invoked). This is a portable replacement:
# run the command in the background, race it against a sleep-then-kill watcher, and
# report 124 (matching GNU timeout's own convention) if the watcher won the race.
run_with_timeout() {
  local secs="$1"; shift
  "$@" &
  local pid=$!
  ( sleep "$secs" && kill -TERM "$pid" 2>/dev/null ) &
  local watcher=$!
  local status=0
  if wait "$pid" 2>/dev/null; then
    status=0
  else
    status=$?
  fi
  kill "$watcher" 2>/dev/null
  wait "$watcher" 2>/dev/null
  if [ "$status" -eq 143 ]; then   # 128+SIGTERM - our watcher killed it
    status=124
  fi
  return "$status"
}

{
  echo "=== whatsapp-someday run: $(date) ==="

  # Belt-and-braces day check; launchd's own Weekday filter should already guarantee this.
  if [ "$(date +%u)" != "6" ]; then
    echo "Not Saturday ($(date +%A)), skipping."
    exit 0
  fi

  # Cheap short-circuit: don't spin up a Claude Code session if there's nothing to process.
  # (find, not a bare glob - zsh's default nomatch behavior errors on a glob with zero hits)
  if [ -z "$(find "$DROPFOLDER" -maxdepth 1 -name '*.txt' -print -quit 2>/dev/null)" ]; then
    echo "No new export in '$DROPFOLDER', nothing to do."
    record_outcome "no-op" "no new export found"
    exit 0
  fi

  echo "New export(s) found, invoking Claude Code headlessly (allowlisted tools only, no permission bypass)."
  cd "$VAULT" || exit 1

  run_with_timeout "$TIMEOUT_SECS" "$CLAUDE_BIN" -p "/whatsapp-someday" \
    --permission-mode acceptEdits \
    --allowedTools "Read Edit Write WebFetch Grep Glob PushNotification Bash(ls *) Bash(mkdir -p *) Bash(mv *) Bash(date *) Bash(cat *)" \
    --add-dir "$VAULT" \
    --add-dir "$DROPFOLDER" \
    --output-format text

  STATUS=$?
  if [ "$STATUS" -eq 124 ]; then
    echo "TIMED OUT after ${TIMEOUT_SECS}s - likely stuck on a tool call outside the allowlist. Nothing was force-approved; re-run manually with /whatsapp-someday to see what it hit."
    record_outcome "FAILURE (timeout)" "timed out after ${TIMEOUT_SECS}s, see logs/run_$STAMP.log"
  elif [ "$STATUS" -ne 0 ]; then
    record_outcome "FAILURE (exit $STATUS)" "see logs/run_$STAMP.log"
  else
    record_outcome "success" "see today's row in log-2026-Q3.md for what was actually processed"
  fi

  echo "=== run complete (exit $STATUS): $(date) ==="
} >> "$LOGFILE" 2>&1
```
