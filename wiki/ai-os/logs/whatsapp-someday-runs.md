---
type: log
created: 2026-08-15
---

# WhatsApp Someday - Run Log

> One line per Saturday the automated job actually checked the drop folder. Written by the wrapper script itself (`~/.claude/skills/whatsapp-someday/scripts/run_weekly.sh`), not by the headless Claude session it launches - so a row lands here even if the inner Claude session times out or fails partway through. This is the compliance trail: check this file, not the hidden per-run logs, to see whether the automation is actually firing and succeeding.

**How to read a gap:** if a Saturday is missing from this table entirely, the job never fired that day at all (laptop never on/logged-in that Saturday, or the launchd job got unloaded - check with `launchctl list | grep whatsapp-someday`). If a Saturday is present with a `FAILURE` outcome, the job fired but didn't complete - check the referenced log file.

## How to verify the job itself is still registered

This table only tells you what happened when the job fired. It can't tell you if the job was silently removed (OS update, accidental `launchctl bootout`, plist deleted). Check separately, whenever you think of it:

```bash
launchctl list | grep whatsapp-someday
```

If that returns nothing, the job isn't loaded - reload it with:

```bash
launchctl bootstrap gui/$(id -u) ~/Library/LaunchAgents/com.julianhart.whatsapp-someday.plist
```

---

## Run history

New rows are appended by the wrapper script below this line - keep this table the last thing in the file so appends land correctly.

| Date | Outcome | Detail |
|------|---------|--------|
| 2026-08-15 | N/A (manual) | First live run was manual, before the launchd job existed. See [[../logs/log-2026-Q3\|log-2026-Q3]] 2026-08-15 entries. |
| 2026-08-15 | no-op | no new export found (manual script test, launchd load + re-test after the glob fix) |
| 2026-08-15 | no-op | no new export found |
| 2026-08-15 | FAILURE (exit 127) | see logs/run_2026-08-15_095339.log |
| 2026-08-15 | success | see today's row in log-2026-Q3.md for what was actually processed |
| 2026-08-15 | success | see today's row in log-2026-Q3.md for what was actually processed |
