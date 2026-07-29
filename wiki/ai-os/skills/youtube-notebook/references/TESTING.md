<!-- Mirror of ~/.claude/skills/youtube-notebook/references/TESTING.md — do not edit here; edit the source file -->
# youtube-notebook - Testing Log

tags: [technical, skills, testing, notebooklm]

> *What was tested, how, and what it proved. Append a row per session.*

---

## Key Takeaways

- The enumerator was validated by reproducing a manually verified result byte for byte
- The first verification design produced 61 false positives and was rebuilt
- Full ingest -> brief -> download -> reconcile was proven end to end on a 2-video window

---

## 2026-07-29 - Build and validation

### T1: Enumerator against a known-good result
The June 2026 NateBJones set had already been produced by hand (19 long-form
videos, verified via tab walk + uploads-playlist diff). The enumerator was run
over the same window and its output compared.

```bash
python enumerate_channel.py --channel @NateBJones --month 2026-06 \
  --tabs videos --out test_manifest.json
```

**Result:** 19 videos, `VERIFICATION: PASS`. Diff of `(upload_date, id)` tuples
against the hand-built list: **IDENTICAL**. This is the load-bearing test - it
proves the automated path reproduces a result whose completeness was established
independently.

### T2: Verification false-positive bug (found and fixed)
First run reported `Unaccounted ids: 61` and `REVIEW REQUIRED` despite the video
count being correct.

**Cause:** with `--tabs videos`, only `/videos` was walked, but the uploads
playlist contains Shorts too. Every Short registered as an unaccounted ID.

**Fix:** separated *selection scope* from *verification scope*. Verification now
always walks all three tabs regardless of `--tabs`; selection filters afterwards.
Unaccounted IDs are additionally dated individually and only count as gaps if
they fall inside the window. Post-fix: `Genuine gaps: 0`, `PASS`.

**Lesson:** a cross-check comparing a broad source against a narrow one will
manufacture false gaps. Scope both sides identically before diffing.

### T3: End-to-end build
2-video window (28-29 Jun 2026) into a throwaway notebook.

```bash
python build_notebook.py --manifest e2e/manifest.json \
  --notebook-title "ZZ TEST youtube-notebook" --output-dir ./e2e
```

**Result:** `OVERALL: PASS`, exit 0. All reconciliation checks true:
`sources_match`, `artifacts_match`, `files_match`, `all_artifacts_completed`,
`headers_matching_title: 2/2`. Test notebook deleted afterwards.

### T4: Filename sanitiser edge cases
`Switch?` was becoming `Switch -.md` - `?` was being replaced by a separator that
then dangled.

**Fix:** separator-like illegal characters (`/ \ | :`) become `" - "`; the rest
(`* ? " < >`) are dropped; trailing `" .-"` stripped.

| Input | Output |
|-------|--------|
| `...Companies Switch?` | `...Companies Switch` |
| `...Codex \| Do This Instead` | `...Codex - Do This Instead` |
| `Apple WWDC 2026: The AI Story...` | `Apple WWDC 2026 - The AI Story...` |
| `...Doesn't Care.` | `...Doesn't Care` |

---

## Not yet tested

| Gap | Risk | How to close |
|-----|------|--------------|
| Topic filtering | Medium - the interpretive path is untested in anger | Run "all AI workflow videos from November" on a real channel |
| `--resume` after a genuine mid-run failure | Medium - only the happy path was exercised | Kill a run mid-ingest and resume |
| Channels with >900 uploads in window | Low | `MAX_ENTRIES` guard; raise if hit |
| A channel that genuinely has a gap | Medium - the failure path has never fired on real data | Construct a case, or trust the false-positive fix in T2 |
| Shorts/streams as *selected* tabs | Low - walked during every verification, never ingested | Run with `--tabs videos,shorts` |
| Multi-year windows (`--date-format %Y-%m-%d`) | Low | Run a Dec-Jan window |

---

## Pre-flight checklist

1. `notebooklm auth check --test --json` -> `"status": "ok"`
2. `which yt-dlp` -> resolves
3. `python -c "import sys; sys.path.insert(0,'scripts'); from nlm import resolve_binary; print(resolve_binary())"`
4. Enumerate first and read `verification.passed` before building anything
