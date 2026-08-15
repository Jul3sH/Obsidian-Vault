> Mirror copy, exact. Source: `~/.claude/skills/whatsapp-someday/SKILL.md`

---
name: whatsapp-someday
description: Process a new WhatsApp "Someday" self-chat export from the Dropbox drop folder into the wiki - substantive personal notes routed to their existing wiki home, share links fetched and categorised into raw/brain-dump.md, attachments and dead links dropped. Runs weekly (Saturday) via a local launchd job, or on demand with /whatsapp-someday.
---

# WhatsApp Someday Import

Julian keeps a running "Someday" self-chat in WhatsApp (personal reminders + links he shares to himself to look at later). He periodically exports it (Settings > Export Chat > Without Media) and drops the `.txt` file into a Dropbox folder that syncs locally. This skill turns a new export into wiki content, using the exact method established manually on 2026-08-15 (see `wiki/ai-os/logs/log-2026-Q3.md`, 2026-08-15 Compile entries).

**Drop folder (local, synced):** `~/Library/CloudStorage/Dropbox/5-Performance/Whatsapp someday/`
Julian names each export by its download date (his convention, not enforced by this skill) so multiple files can sit there without colliding. This skill does not depend on the filename - it treats **any `.txt` file directly in that folder** (not already inside its `_processed/` subfolder) as new and unprocessed.

## Step 0 - Find new exports

```bash
ls "$HOME/Library/CloudStorage/Dropbox/5-Performance/Whatsapp someday/"*.txt 2>/dev/null
```

If nothing matches, stop here - this is a no-op run. Do not touch the wiki, do not write a log row. (This is expected most weeks if Julian hasn't exported anything new.)

If one or more `.txt` files are found, process each in turn, oldest first (by file mtime).

## Step 1 - Parse the export

WhatsApp "without media" export format: `[D/M/YYYY, H:MM:SS AM/PM] Sender: message`. Attachments appear as `<attached: filename>` placeholders with no retrievable content.

Split every message into exactly one of three buckets:

1. **Bare share link** - the entire message body is a single URL (Instagram, YouTube, LinkedIn, or other). This is the overwhelming majority of the content.
2. **Substantive text** - anything else: a personal note, a reflection, a message drafted to someone else, a question, an instruction. If a message mixes a short comment with a link, treat the comment as substantive text and the link separately.
3. **Attachment placeholder** (`<attached: ...>`) - the underlying photo/video/PDF is not in the text export and cannot be read. Drop these without trying to process them. If a filename suggests real value (e.g. a named PDF guide), note it in the run's summary so Julian can supply the actual file if he wants it kept - do not chase it yourself.

Also drop, without processing: messages that are clearly stale/logistics for a dated one-off event that has already passed (e.g. trip planning for a trip months prior), and any message that is Claude Code's own prior session output pasted into the chat as a note-to-self (these aren't "someday" content, they're operational scratch).

## Step 2 - Route substantive text

For each substantive-text item, search the wiki for an existing, clearly-matching home before writing anything - the same judgement call made for the 22 Jun Father's Day note (routed to [[dad-health-discussions]]) and the 16 Jul self-notes (routed to [[commitment-avoidance]]) on 2026-08-15. A "clearly matching home" means an existing article whose subject the note is unambiguously about (a family member's health file, a named behavioural-pattern article, a project's status doc) - not a vague thematic association.

- **Match found:** append the note there, in that file's existing style and dated, exactly as done for those two examples. Update the file's own "last updated" line if it has one.
- **No clear match:** do not create a new wiki file (per AGENTS.md - new-file names are agreed with Julian first, never done unattended). Instead, drop it into `raw/brain-dump.md`'s **Personal** section as an ordinary capture-inbox item, in the same `| Item | Note |` table style as everything else there. This is Julian's own stated default for unattended runs (2026-08-15) - safe, reversible, zero-evaluation.

## Step 3 - Fetch and categorise share links

For each bare share link, try to retrieve real content before writing a description - never invent one from the URL slug alone.

- **Instagram** (`instagram.com/reel/...`, `instagram.com/p/...`): plain WebFetch is blocked by Instagram's bot-wall and returns nothing useful. Append `embed/captioned/` to the path before fetching, e.g. `https://www.instagram.com/reel/XXXXX/embed/captioned/` - this reliably returns the caption, account handle, and engagement stats even without login. This was discovered and verified working on 2026-08-15 (~85% success rate across ~140 links).
- **YouTube** (`youtu.be/...`, `youtube.com/shorts/...`, `youtube.com/post/...`): follow the redirect to the full watch page and fetch that; the oEmbed endpoint (`youtube.com/oembed?url=...`) is a faster fallback for just the title.
- **LinkedIn posts**: fetch directly - the URL slug is usually already a strong signal of the post's first line even before fetching, but confirm against the fetched page/description where possible rather than relying on the slug alone.
- Anything that fails after one retry (login wall, deleted, private, no usable content) goes on a dropped/unavailable list. Do not force a description for these - just count them.

Classify each successfully-described item into one of the four `raw/brain-dump.md` workstreams:
- **Career** - job search, hiring, interviews, career strategy
- **Performance** - self-management, mindset, communication, productivity, leadership, business/founder advice
- **Wiki / AI OS** - Claude/Claude Code, AI agents, AI tools and skills, prompting, anything that could feed this vault's own AI-OS tooling
- **Personal** - everything else: fitness, sport, hobbies, relationships/dating, home, lifestyle, entertainment, nostalgia. This bucket will usually be the largest.

## Step 4 - Write to the wiki

Append a new dated subsection to each affected workstream in `raw/brain-dump.md`:

```
### WhatsApp Someday import (<today's date>)

| Item | Note |
|------|------|
| ... |

**Source links:**
- ...
```

Keep descriptions to one line each - this file explicitly treats verbosity as a defect (see its own header). Where several links are near-duplicate saves of the same account/theme (this happens a lot - the same handful of Instagram accounts get re-saved repeatedly), collapse them into one row noting the count rather than listing near-identical rows.

Update `raw/brain-dump.md`'s frontmatter `updated:` date to today.

If any dropped/unavailable links exist, list them under a `**Dropped as unavailable (N):**` line so nothing silently vanishes - Julian can always paste one back in manually if a description turns out to be needed after all.

## Step 5 - Close out the file

1. `mkdir -p` a `_processed/` subfolder inside the Dropbox "Whatsapp someday" folder if it doesn't exist, and move the processed `.txt` file into it (mirrors the vault's own `raw/` → `raw/_processed/` convention). This is what makes the next run's Step 0 naturally idempotent - a file that's been moved out won't be picked up again.
2. Append a row to `wiki/ai-os/logs/raw-manifest.md` recording the source filename, its wiki destination(s), and today's date.
3. Append one row to the current quarter's ops log (`wiki/ai-os/logs/log-2026-Q3.md` or whichever quarter is current - check `CLAUDE.md`'s "current log file" pointer) as type `Compile`, summarising: how many personal notes were routed and where, how many links were categorised per workstream, and how many were dropped as unavailable.

## Manual invocation

Run `/whatsapp-someday` any time to process whatever's currently sitting in the drop folder, exactly as the automated weekly run would. Useful if Julian wants a batch processed sooner than the next Saturday.

## Automated weekly run

A local launchd LaunchAgent (`com.julianhart.whatsapp-someday`, see `wiki/ai-os/system-design/claude/local-automation.md` for the mirrored config and rationale) fires on a schedule confined to Saturdays and invokes this skill headlessly via `claude -p "/whatsapp-someday"`. Because Step 0 is naturally idempotent (processed files are moved out of the drop folder), the job can fire more than once on a Saturday without duplicating work - it only ever acts on files that are still sitting unprocessed.

The automated run operates in full-auto mode per Julian's explicit instruction (2026-08-15): no approval is sought before writing to the wiki or moving files. It uses a scoped tool allowlist (Read/Edit/Write/WebFetch plus a narrow set of Bash commands for the file-move) rather than a blanket permission bypass, so the blast radius of an unexpected action stays bounded even though nobody is watching the run. See `local-automation.md` for the exact allowlist and the reasoning against `--dangerously-skip-permissions`.
