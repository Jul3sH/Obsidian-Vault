---
name: youtube-notebook
description: Ingest a YouTube channel's videos into a NotebookLM notebook with verified-complete enumeration, date-prefixed source titles, and one native briefing doc per video whose title matches its source. Use when the user wants to turn a YouTube channel (a blogger, creator, or commentator) into a NotebookLM notebook, restricted by month, date range, topic, or a combination - e.g. "all AI workflow videos from November", "put NateBJones June into NotebookLM", "make me a notebook of X's videos".
---

# youtube-notebook Skill

Turns a YouTube channel plus a restriction expression into a NotebookLM notebook:
one source per video, one native NotebookLM briefing doc per source, titles that
correlate end to end, and a reconciliation that proves nothing was silently dropped.

**This skill never writes briefing content.** All summarisation is NotebookLM's own
`--format briefing-doc`. The skill controls enumeration, filtering, titling and
verification only.

---

## Activation Triggers

**Explicit:** `/youtube-notebook`

**Intent-based:**
- "create a notebook of [channel]'s videos from [month]"
- "all [topic] videos from [channel] in [period]"
- "put [channel] into NotebookLM"
- "make me a NotebookLM notebook from this YouTube channel"

Do NOT use for wiki-content notebooks or flashcard generation - that is
`notebooklm-py`.

---

## Step 1: Interview (ALWAYS run this first)

Never guess the channel or the restriction. Ask, using `AskUserQuestion` where
the options are closed. Collect all of the following before touching a script.

| # | Question | Notes |
|---|----------|-------|
| 1 | **Which channel?** | `@handle` or full URL. Required. |
| 2 | **How should uploads be restricted?** | Month (`2026-06`), explicit date range, topic, or a combination. Required. |
| 3 | **Which content types?** | Long-form `videos` (default), `shorts`, `streams`. Shorts have thin transcripts and inflate source count; recommend long-form unless asked. |
| 4 | **Briefing docs per source?** | Default yes. `--no-briefings` ingests sources only. |
| 5 | **Notebook name?** | Suggest one, but check `notebooklm list` first and match the user's existing naming convention for that channel. |
| 6 | **Output folder for downloads?** | Default `~/Downloads/<notebook title> Briefings/`. |

If a restriction spans more than one calendar year, set `--date-format %Y-%m-%d`
so source titles stay unambiguous.

### Interpreting restriction expressions

"All AI workflow videos from November" is **two filters of different kinds**.
Keep them separate, because only one of them is provable.

| Filter | Kind | Applied by | Can completeness be proven? |
|--------|------|-----------|------------------------------|
| Date / period | Deterministic | `enumerate_channel.py` | **Yes** - dual-path verification |
| Content type (tab) | Deterministic | `enumerate_channel.py --tabs` | **Yes** |
| Topic / subject | Judgement | **You, in session** | **No** - must show exclusions |

Never let a topic filter be applied silently inside a script. See Step 3.

---

## Step 2: Enumerate and verify (deterministic)

```bash
python ~/.claude/skills/youtube-notebook/scripts/enumerate_channel.py \
  --channel @NateBJones --month 2026-06 --tabs videos \
  --out /tmp/nb/manifest.json
# date range instead of a month:
#   --since 2026-11-01 --until 2026-11-30
# add --descriptions when a topic filter will be applied
```

The script establishes completeness two independent ways and diffs them:

1. **Per-tab walk** of `/videos`, `/shorts`, `/streams`, reading each video's real
   `upload_date` metadata. It keeps widening the page window until it has fetched
   entries *older than* the window start, so truncation at the boundary is
   detectable rather than assumed.
2. **Uploads-playlist cross-check** against `UU<channel_id[2:]>`, which contains
   every upload regardless of tab. Any playlist ID missing from the tab walk is
   dated individually; those falling inside the window are reported as
   `genuine_gaps_in_window`.

**Verification always walks all three tabs even when only one is selected.** The
uploads playlist mixes content types, so comparing it against a single tab would
flag every Short as a false gap. Selection scope and verification scope are
separate fields in the manifest.

`verification.passed` is true only if every tab crossed the start boundary, the
playlist spanned the window, and there are zero genuine gaps.

> **If `passed` is false, do not describe the result as complete.** Report the
> specific gap to the user and let them decide whether to continue.

---

## Step 3: Apply any topic filter IN THE OPEN (judgement)

Only if the user asked for a topic restriction. Do this yourself, in session -
there is no script for it, deliberately.

1. Re-run enumeration with `--descriptions`.
2. Read the manifest's `videos` array (title + description excerpt).
3. Decide include/exclude per video.
4. **Show the user both lists** - what you kept and what you dropped, with a
   one-line reason per exclusion. Borderline calls go in front of the user, not
   into a silent decision.
5. On approval, rewrite the manifest: filter `videos`, and populate
   `topic_filter` (the expression) and `excluded_by_topic` (dropped items with
   reasons) so the run report records what was judged.

State plainly that the date filter is verified exhaustive while the topic filter
is interpretive. Never claim a topic-filtered set is "all" of anything.

---

## Step 4: Build the notebook

```bash
python ~/.claude/skills/youtube-notebook/scripts/build_notebook.py \
  --manifest /tmp/nb/manifest.json \
  --notebook-title "NBJ June 2026" \
  --output-dir ~/Downloads
```

Options: `--no-briefings`, `--notebook-id <uuid>` (reuse an existing notebook),
`--resume` (continue a failed run from `run-state.json`), `--date-format`.

Phases: create notebook -> add each video as a YouTube source and rename it ->
wait for processing -> generate one briefing per source -> wait and retitle ->
download -> reconcile. State is checkpointed to `run-state.json` after every
item, so `--resume` never duplicates work.

### Extending an existing notebook

`--notebook-id` adds a new window to a notebook that already holds earlier ones
(e.g. adding July to a June notebook). Pass `--notebook-title` alongside it so
the briefings folder is named correctly; renaming the notebook first keeps the
title honest about what it now contains.

Reconciliation adapts: a reused notebook legitimately holds more than this run's
manifest, so completeness becomes a **subset** test (every expected item present)
rather than equality (expected is all there is). Equality would fail every
incremental run even with nothing missing. Artifact health is likewise scoped to
this run's titles, so a hand-made audio overview from months ago cannot fail the
report. `run-report.json` records `notebook_reused` plus the notebook's total
counts so the superset is visible. Without `--notebook-id`, strict equality still
applies - a fresh notebook should contain exactly the manifest and nothing else.

---

## The correlation rules (the point of this skill)

NotebookLM auto-titles briefing docs from their content, so a briefing for
*"Opus 4.8 Scored 81"* comes back named *"Analysis of Opus 4.8 and the 2026 AI
Competitive Landscape"*. Nothing links it to the video. Four surfaces are forced
into agreement:

| Surface | Value |
|---------|-------|
| Source title in NotebookLM | `06-03 Opus 4.8 Scored 81. Your Workflow Doesn't Care.` |
| Briefing artifact title | **identical string** |
| Downloaded filename | same, filesystem-sanitised |
| H1 inside the file | same, with source URL and publish date beneath |

The source title format is `<date-prefix> <original YouTube title>`, default
`%m-%d`. NotebookLM's own auto-title is never discarded: it is preserved as the
`**NotebookLM title:**` metadata field and as the `##` heading below the divider.
Only the heading level is changed, never the prose.

---

## Step 5: Report

Reconciliation is written to `run-report.json` and the script exits non-zero on
failure. Report to the user:

- The inventory table (per tab, in window) and what was excluded, by which filter
- `verification.passed`, and the specific gap if false
- The four-way reconciliation: sources / artifacts / files / headers vs expected
- Notebook ID and output folder

Never report success from an exit code alone - read `run-report.json` and quote
the counts.

---

## Confirmation Rules

**Without confirmation:** enumeration, verification, `notebooklm list`, auth checks,
reading manifests.

**Confirm first:** creating or deleting a notebook, adding sources, generating
artifacts, downloading files. Always show the manifest count and the proposed
notebook name before building.

---

## Known Gotchas

See `references/notebooklm-cli.md` for the verified command surface. The three
that cost real debugging time:

1. **`notebooklm` is a shell alias, not a binary on PATH.** `subprocess.run(["notebooklm", ...])`
   raises `FileNotFoundError`; a bare `notebooklm` in a `bash script.sh` fails
   silently. Always resolve the real path - `scripts/nlm.py` does this.
2. **`artifact get` returns `status` at the top level**, not nested under `artifact`.
3. **The CLI writes warnings to stderr and data to stdout**, so `--json` output is
   clean if you read stdout only.
4. **Never pipe `build_notebook.py` into `tail`/`head`.** The pipeline reports the
   *last* command's status, so a hard failure mid-run still exits 0 and reads as
   success. Redirect to a file and read it instead. This is why the rule above is
   "read `run-report.json`", not "check the exit code".

---

## Error Handling

| Error | Cause | Fix |
|-------|-------|-----|
| `FileNotFoundError: notebooklm` | alias not visible to scripts | set `NOTEBOOKLM_BIN`, or rely on `nlm.resolve_binary()` |
| Auth failure | expired OAuth cookie | `notebooklm login` |
| `yt-dlp not found` | missing dependency | `brew install yt-dlp` |
| `may be truncated` warning | tab walk hit `MAX_ENTRIES` | raise `MAX_ENTRIES` or narrow the window |
| Source stuck not-ready | slow processing | re-run with `--resume` |
| Rate limit on generate | too many concurrent | already retried 3x; re-run with `--resume` |

## Dependencies

`notebooklm-py[browser]` (authenticated), `yt-dlp`, Python 3.10+.
Google APIs route direct in HK - do NOT route through VPN.
