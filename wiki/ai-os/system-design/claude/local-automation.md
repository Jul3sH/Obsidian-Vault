---
type: reference
created: 2026-08-15
updated: 2026-08-15
---

# Local Automation (launchd) - DISCONTINUED 2026-08-15

**⚠ As of 15 Aug 2026: this automation was built, tested, and then turned off the same day.** The plist has been deleted and the launchd job unloaded. [[../../skills/whatsapp-someday/SKILL|whatsapp-someday]] is manual-only now (`/whatsapp-someday`). This document is kept as a record of what was built and why it was dropped, not as documentation of something currently running.

**Why it was dropped:** the last unresolved piece was getting Julian a real notification when a run succeeded, since nobody watches an unattended run. The sanctioned in-session tool (`PushNotification`) turned out to depend on a terminal context that a headless launchd-invoked process doesn't have, so it silently did nothing. Chasing a working replacement (native macOS notifications via a file-based handoff from the headless session to the wrapper script, verified through `launchctl kickstart` rather than Claude's own sandboxed Bash tool) turned into enough back-and-forth debugging that Julian called it: *"This is getting too complicated... Let's forget the automation part."* Given the actual weekly volume is one file, manually running `/whatsapp-someday` costs Julian little and keeps him watching the run in real time - which was always a cleaner solution to "how do I know it worked" than any notification mechanism could be.

## Original rationale (historical)

This document was originally the record of a persistent, unattended, local scheduled job that ran Claude Code on Julian's Mac without a human watching each action. It existed because Claude Code's two built-in scheduling mechanisms cannot do this job, and because creating this kind of automation is a safety-sensitive action that Claude Code's own auto-mode classifier gates behind explicit, specific user consent - so that consent was recorded here, not just implied. The rest of this document is left as written at the time, for the record.

## Why this exists instead of a built-in scheduler

Two sanctioned scheduling mechanisms exist in Claude Code and neither fits:

| Mechanism | Why it doesn't work here |
|---|---|
| `CronCreate` | Session-only - lives in memory, dies when the Claude session ends, auto-expires after 7 days regardless. Not durable. (This exact limitation was already hit once before, in June 2026 - see the "jira-pull" auto-run attempt logged in `log-2026-Q2.md`, 2026-06-15.) |
| `RemoteTrigger` / `/schedule` (cloud "routines") | Runs in Anthropic's cloud - no access to the local filesystem at all, so it cannot reach the Dropbox-synced drop folder or the local vault. Same limitation flagged in `log-2026-Q2.md`, 2026-06-27 ("remote `/schedule` routines can't reach the local non-git wiki/skill files either. Parked as a someday item... local launchd job needed"). |

The [[../../skills/whatsapp-someday/SKILL|whatsapp-someday]] skill needs both: durability across weeks and local filesystem access (the Dropbox-synced drop folder plus the vault itself). Only a local OS-level scheduler satisfies both, so this uses macOS `launchd`.

## The consent record

Creating a local launchd job that invokes Claude Code headlessly is flagged by Claude Code's auto-mode classifier under two named rules: **"Unauthorized Persistence"** (creating a cron/launchd job that executes code beyond the current session) and **"Create Unsafe Agents"** (an agent loop running with no per-action human monitor). Both require the user's own explicit, specific, in-conversation consent naming the actual mechanism - a settings.json permission tweak is not sufficient for this category.

That consent was given on 2026-08-15, in response to a direct question naming the mechanism exactly: *"a persistent local launchd job (com.julianhart.whatsapp-someday) that invokes Claude Code headlessly and unattended on Saturdays, with no human watching each action it takes (edits, moves files, fetches ~100+ URLs), using a scoped tool allowlist rather than a full permission bypass."* Julian's answer: *"Yes - I want the local launchd job, unattended, as described."*

## What was deliberately NOT used

`--dangerously-skip-permissions` / `--permission-mode bypassPermissions` were considered and rejected. Two draft versions of the wrapper script - one using the bypass flag, one using only a scoped allowlist - were both initially blocked by the auto-mode classifier; only after the explicit consent above was the allowlist-only version (no bypass flag at all) accepted. The running job therefore uses `--allowedTools` to pre-authorise only the specific tools the skill needs (`Read Edit Write WebFetch Bash(ls *) Bash(mkdir -p *) Bash(mv *) Bash(date *) Bash(cat *)`), plus `--permission-mode acceptEdits`, plus `--add-dir` scoped to just the vault and the Dropbox drop folder. If the run ever hits something outside that allowlist, there is nobody present to approve it - a `timeout` (45 min) kills the run rather than letting it hang or silently escalating.

## The job

**Label:** `com.julianhart.whatsapp-someday`
**Plist location (live, not mirrored in full below - see the exact copy underneath):** `~/Library/LaunchAgents/com.julianhart.whatsapp-someday.plist`
**Wrapper script:** `~/.claude/skills/whatsapp-someday/scripts/run_weekly.sh` (mirrored at [[../../skills/whatsapp-someday/scripts/run_weekly|run_weekly.md]])
**Logs:** `~/.claude/skills/whatsapp-someday/logs/` (per-run logs plus launchd's own stdout/stderr capture)

**Trigger design:** Julian's stated requirement was "fire when I log on, at any point on Saturdays" rather than one fixed clock time, since the laptop isn't always on. This is approximated with `RunAtLoad` (fires on every fresh login) plus six `StartCalendarInterval` checkpoints spread across Saturday (09:00, 12:00, 15:00, 18:00, 21:00, 23:30) as a safety net for a session that stays logged in but asleep/awake without a fresh login event - macOS launchd runs a missed calendar-interval job shortly after the next wake if the Mac was asleep at the scheduled time. This is not a literal login-hook; it's a reasonable approximation using launchd's actual catch-up behaviour, and is disclosed as such rather than overclaimed.

The job is naturally idempotent: [[../../skills/whatsapp-someday/SKILL|the skill's Step 0]] only ever acts on `.txt` files still sitting in the drop folder, and Step 5 moves each processed file into a `_processed/` subfolder immediately. Firing more than once on a Saturday (multiple wake events, a fresh login plus a calendar checkpoint) is therefore harmless - the second and subsequent fires just find nothing to do.

### Exact plist content (mirror)

> Mirror copy, exact. Source: `~/Library/LaunchAgents/com.julianhart.whatsapp-someday.plist`

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>com.julianhart.whatsapp-someday</string>

    <key>ProgramArguments</key>
    <array>
        <string>/bin/zsh</string>
        <string>-c</string>
        <string>/Users/julianhart/.claude/skills/whatsapp-someday/scripts/run_weekly.sh</string>
    </array>

    <!-- Checkpoints spread across Saturday only (Weekday 6 = Saturday), so it doesn't
         depend on the laptop being on at one exact time. Combined with RunAtLoad below
         for a fresh login. Step 0 in the script/skill makes reruns a harmless no-op. -->
    <key>StartCalendarInterval</key>
    <array>
        <dict><key>Weekday</key><integer>6</integer><key>Hour</key><integer>9</integer><key>Minute</key><integer>0</integer></dict>
        <dict><key>Weekday</key><integer>6</integer><key>Hour</key><integer>12</integer><key>Minute</key><integer>0</integer></dict>
        <dict><key>Weekday</key><integer>6</integer><key>Hour</key><integer>15</integer><key>Minute</key><integer>0</integer></dict>
        <dict><key>Weekday</key><integer>6</integer><key>Hour</key><integer>18</integer><key>Minute</key><integer>0</integer></dict>
        <dict><key>Weekday</key><integer>6</integer><key>Hour</key><integer>21</integer><key>Minute</key><integer>0</integer></dict>
        <dict><key>Weekday</key><integer>6</integer><key>Hour</key><integer>23</integer><key>Minute</key><integer>30</integer></dict>
    </array>

    <!-- Fires on every fresh login too; the script itself exits immediately if it's
         not Saturday, so this is safe on the other six days. -->
    <key>RunAtLoad</key>
    <true/>

    <key>StandardOutPath</key>
    <string>/Users/julianhart/.claude/skills/whatsapp-someday/logs/launchd.out.log</string>
    <key>StandardErrorPath</key>
    <string>/Users/julianhart/.claude/skills/whatsapp-someday/logs/launchd.err.log</string>

    <key>ProcessType</key>
    <string>Background</string>
</dict>
</plist>
```

## Tested end to end (2026-08-15)

The job was initially activated without ever having actually fired on a real file - only the "nothing to do" no-op path had been exercised. Julian flagged this directly, correctly. Running it for real with a test file surfaced three bugs a reasoning-only build had missed: macOS has no built-in `timeout` command (GNU coreutils, not BSD - the first live run errored out before Claude was even invoked), the timeout replacement's own first draft crashed on a zsh-reserved variable name (`status`), and the tool allowlist was missing `Grep`/`Glob`, which the skill's wiki-search step needs. The second bug's crash happened *after* the real Claude process had already been launched in the background, which then ran to completion orphaned and unsupervised while the parent script logged nothing at all - proving the exact silent-failure risk the compliance section below exists to catch, live. All three are fixed in the current script, plus a `trap`-based safety net that kills any orphaned child and guarantees a compliance row gets written no matter how the script dies. Verified clean on a second full test run (exit 0, correct wiki writes, file moved, compliance row written, no orphaned process).

## Compliance / observability (added 2026-08-15)

Nobody watches this job run. The compliance question - did it actually fire, did it succeed, or did it fail silently - can't be answered by looking at `raw/brain-dump.md` alone, because "nothing new this week" and "it broke" both look identical from there (no new content either way). [[../../logs/whatsapp-someday-runs|whatsapp-someday-runs.md]] closes that gap: the **wrapper script itself** appends one row per Saturday it actually checks (no-op / success / FAILURE + reason), written by plain shell file I/O rather than by the headless Claude session - so a row lands even if that inner session times out or crashes before finishing. Check that file, not this one, to see whether the automation is healthy. A missing Saturday in that table means the job never fired at all that day (worth checking `launchctl list | grep whatsapp-someday` - see below).

## How to check on it / turn it off

- **Compliance / did it run and succeed:** read [[../../logs/whatsapp-someday-runs|whatsapp-someday-runs.md]]
- **See if the job is still loaded:** `launchctl list | grep whatsapp-someday`
- **See a specific run's full transcript:** `ls -lt ~/.claude/skills/whatsapp-someday/logs/` then read the newest `run_*.log`
- **Turn it off (unload, keeps the files):** `launchctl bootout gui/$(id -u) ~/Library/LaunchAgents/com.julianhart.whatsapp-someday.plist`
- **Remove entirely:** unload as above, then delete the plist and the skill folder

## Wiki mirror confirmation

This file mirrors the live plist at `~/Library/LaunchAgents/com.julianhart.whatsapp-someday.plist` and documents the wrapper script mirrored separately at [[../../skills/whatsapp-someday/scripts/run_weekly|run_weekly.md]]. Both are tracked in [[hidden-file-sync|Hidden File Sync]].
