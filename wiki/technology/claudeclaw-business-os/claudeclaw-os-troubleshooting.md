---
type: reference
created: 2026-07-07
---

# ClaudeClaw OS - Troubleshooting

> Operational fixes for the running ClaudeClaw OS Telegram bot. Start here before touching the database or reinstalling.

Part of [[claudeclaw-business-os-overview|ClaudeClaw Business OS]]. Install lives at `~/claudeclaw-os`; config at `~/.claudeclaw`; runs via launchd job `com.claudeclaw.app`. (Path corrected 11 Aug 2026 from the older `~/claudeclaw-business-os` name - see incident below. Don't trust this line either: verify with `lsof`.)

---

## Golden rule: restart after any change

**Whenever you change anything the bot uses, restart it** - otherwise the running process keeps the old state and your change appears to do nothing. This includes: `~/.claudeclaw/CLAUDE.md`, agent personas, `.env`, skills, and any direct database edit.

Two ways to restart (they do the same thing - reload the process):

| Method | How |
|--------|-----|
| **Dashboard button** (what the ClaudeClaw video shows) | Open `http://127.0.0.1:3141` and click restart |
| **Terminal** | `launchctl kickstart -k gui/$(id -u)/com.claudeclaw.app` |

---

## Bot replies only "Done. [Opus]" to every message

**The one to remember.** Symptom: you ask the bot anything and it answers with a bare `Done.` (plus the model tag, e.g. `[Opus]`) instead of a real reply. Nothing you type works.

### Fix first, understand later

**In Telegram, send `/forget` to the bot, then send your question again.** That clears the stored session and the next message starts a fresh one. `/newchat` does the same thing. This resolves it in seconds - no terminal needed.

### Why it happens

- ClaudeClaw stores one Claude Code **session ID per chat** in `store/claudeclaw.db` (table `sessions`, keyed by `chat_id` + `agent_id`).
- Every turn, the Claude-SDK provider tries to **resume** that stored session by passing it to the `claude` binary. The actual conversation lives in Claude Code's own store at `~/.claude/projects/-Users-julianhart-claudeclaw-business-os/<session-id>.jsonl`.
- If that `.jsonl` is gone (session store rotated/cleared, ID left over from an old install, or a stale row restored during an update), the resume fails with `No conversation found with session ID: ...`. The turn ends with `hasResult: false` and no text, so the bot sends its `Done.` placeholder.
- The Claude-SDK adapter has **no "start fresh on failed resume" fallback** (the ACP adapter does). So once the pointer is stale, *every* message fails until the session is cleared.

### Manual fix (if `/forget` is unavailable)

Clear the stale row directly, then restart the service:

```bash
# back up first
cp ~/claudeclaw-business-os/store/claudeclaw.db ~/claudeclaw-business-os/store/claudeclaw.db.bak

# inspect what's stored
sqlite3 ~/claudeclaw-business-os/store/claudeclaw.db "SELECT * FROM sessions;"

# clear the stale session (all chats, or add WHERE chat_id='<id>')
sqlite3 ~/claudeclaw-business-os/store/claudeclaw.db "DELETE FROM sessions;"

# restart so no in-memory copy lingers
launchctl kickstart -k gui/$(id -u)/com.claudeclaw.app
```

To confirm a stored ID is genuinely orphaned: check whether `~/.claude/projects/-Users-julianhart-claudeclaw-business-os/<session-id>.jsonl` exists. Missing file = resume will fail.

> **Root cause was pre-existing, not update-related.** This first surfaced with a session row dated a month before a version update; the update did not cause it and reinstalling would not have fixed it (the stale pointer lives in `store/`, which is preserved across updates).

---

## Checking the running instance

| Question | Command |
|----------|---------|
| Is it running? | `launchctl list \| grep claw` (shows PID + exit code for `com.claudeclaw.app`) |
| What version? | `grep '"version"' ~/claudeclaw-os/package.json` |
| Which model/provider? | `cd ~/claudeclaw-os && npm run status` |
| Boot log / errors | `tail -30 /tmp/claudeclaw.log` and `/tmp/claudeclaw.err` |
| Restart clean | `launchctl kickstart -k gui/$(id -u)/com.claudeclaw.app` |

The bot runs on the **Claude Code CLI provider** (`claude-opus-4-8`), not the raw Gemini default that newer versions ship - so a changelog note about the default flipping to `gemini-2.5-flash` does not apply to this install.

---

## After a repo folder rename

Renaming the checkout changes the Claude Code project-session path. If the bot was previously running from `~/claudeclaw-os`, existing Claude Code session files may live under:

```text
~/.claude/projects/-Users-julianhart-claudeclaw-os/
```

After the rename to `~/claudeclaw-business-os`, new sessions use:

```text
~/.claude/projects/-Users-julianhart-claudeclaw-business-os/
```

If the bot starts replying with `Done.` after the rename, treat it as a stale session pointer: send `/forget` in Telegram, then retry. Also check launchd plists, shell aliases, notify scripts, and any hidden live config for hardcoded `/Users/julianhart/claudeclaw-os` paths.

---

## Verify before you delete or rename anything (critical, added 11 Aug 2026)

**Do not trust any folder name in this doc, the app's own instructions, or the token-server download page.** Names drift - this install itself was renamed from `claudeclaw-business-os` to `claudeclaw-os` at some point without every reference catching up, which is exactly what caused the incident below. The only thing that matters is where the **live process** actually runs from, not what any doc calls it.

Before touching any folder, confirm the real path:

```bash
launchctl list | grep claw                    # get the PID
lsof -p <PID> -a -d cwd                        # actual working directory
lsof -p <PID> | grep -E "\.db$|\.env"          # confirms where store/.env really live
```

If that path doesn't match the folder you're about to delete or rename, **stop**. You are about to orphan the running bot from its own `.env` and session database.

### Incident: 11 Aug 2026 - live install folder deleted outright

Followed the token-server's official steps ("delete your old claudeclaw-os folder, re-clone") without checking what the running process actually pointed at. The live bot had for some time been running out of `~/claudeclaw-business-os`, an older-named folder holding the real `.env` and `store/claudeclaw.db`, while the "claudeclaw-os" name the official instructions refer to was a separate, newer source checkout. Deleting the real one orphaned the running process onto now-nameless inodes: the bot kept working only until the process next stopped, and `.env` plus the session store were unrecoverable (no backup existed anywhere, including Time Machine).

**Fix required a full rebuild:** stop the process, `npm install && npm run build` on a fresh `~/claudeclaw-os` clone, re-run `npm run setup` to regenerate `.env` (Telegram token, chat ID), `npm run migrate`, restart.

**One thing that did NOT need to happen:** creating a brand-new Telegram bot. A lost `.env` only loses the *token value*, not the bot itself - the same bot's token can be re-fetched any time via BotFather (`/mybots` -> select bot -> API Token), keeping the same bot username and existing contact history. Worth trying before defaulting to `/newbot`.

**Not a vendor problem.** The official instructions only ever say to delete a folder literally named `claudeclaw-os` - that is ordinary, self-consistent update behavior. The trap was environment-specific: this install had drifted onto a second, differently-named folder (`claudeclaw-business-os`) left over from an earlier naming era, which the vendor's instructions never referenced and never told anyone to touch. That folder got deleted too, as part of the same cleanup.

**Resolved 11 Aug 2026, confirmed live:** rebuilt at `~/claudeclaw-os`, migrated, restarted under `launchctl bootstrap`. Verified via `lsof` that the running process's cwd, `store/claudeclaw.db`, and `node_modules` all resolve to that one path, with an established connection to Telegram's servers. **There is now exactly one claudeclaw folder.** The two-name trap this incident depended on cannot recur unless a second copy is created again.

---

## Safe update procedure (avoid data loss)

The official instructions say "delete your old install folder, then re-clone." Do **not** `rm` it - the folder holds gitignored, non-recoverable state (`.env`, `store/`). Rename instead, and **confirm the path first using the verification commands above** - don't assume the folder the instructions name is the one actually running:

1. Verify the live path (see above), then stop: `launchctl bootout gui/$(id -u)/com.claudeclaw.app`
2. Rename (don't delete): `mv ~/claudeclaw-os ~/claudeclaw-os.old`
3. Re-clone via the token link into `~/claudeclaw-os`
4. Restore state: copy `.env` and `store/` from `~/claudeclaw-os.old`
5. Build: `npm install && npm run build`
6. Migrate DB: `npm run migrate` (the app also migrates on boot)
7. Restart: `launchctl bootstrap gui/$(id -u) ~/Library/LaunchAgents/com.claudeclaw.app.plist`
8. Verify version + bot online, then delete `~/claudeclaw-os.old`

**Preserved across updates** (never lives in the repo): `.env`, `store/claudeclaw.db`, and `~/.claudeclaw/` config. See [[claudeclaw-business-os-overview]] for the version/distribution model.

---

## Key Takeaways

- **Bot says only "Done."** -> send **`/forget`** in Telegram, then retry. That is the whole fix 99% of the time.
- Cause is a **stale session pointer** in `store/claudeclaw.db`, not a broken model or a bad install.
- The Claude-SDK provider does not auto-recover from a dead session - it must be cleared.
- **Never `rm` the install folder to update** - rename it, because `.env` and `store/` are not in the repo.
- **Verify the live process's actual path with `lsof` before deleting or renaming anything** (added 11 Aug 2026) - folder names in this doc and in vendor instructions drift and can point at the wrong install.
- **A lost `.env` does not require a new Telegram bot** (added 11 Aug 2026) - re-fetch the existing bot's token from BotFather (`/mybots` -> API Token) instead of running `/newbot`.
