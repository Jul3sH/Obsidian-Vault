---
name: notebooklm-py
description: Automate Google NotebookLM — create notebooks, add wiki sources, generate flashcards and other study artifacts from Personal Log and wiki content.
---

<!-- Mirror of ~/.claude/skills/notebooklm-py/SKILL.md — do not edit here; edit the source file -->

# notebooklm-py Skill

> **Scope:** wiki content only. For **YouTube channels** use the `youtube-notebook` skill.
> **Command surface verified against CLI v0.7.0 on 2026-07-29.** The pre-0.7 signatures
> previously documented here were all broken; see `references/TESTING.md`.

Uses the `notebooklm-py` Python package (unofficial Google NotebookLM client) to automate notebook creation, source ingestion, and artifact generation. Primary use case: extract Personal MBA model content from the wiki and generate flashcards for spaced-repetition review.

---

## Installation (one-time)

```bash
pip install "notebooklm-py[browser]"
playwright install chromium
notebooklm login   # opens browser for Google OAuth; saves cookie file locally
```

Verify auth after login:

```bash
notebooklm auth check --test --json
```

---

## Activation Triggers

**Explicit:** `/notebooklm`

**Intent-based (NLP triggers):**
- "make flashcards from [article / topic]"
- "create flashcards about [model name]"
- "generate a study notebook for [topic]"
- "summarise [wiki topic] in NotebookLM"
- "create a podcast about [topic]"
- "add [topic] to NotebookLM"
- "quiz me on [topic]"

---

## Confirmation Rules

**Run without confirmation:**
- List notebooks: `notebooklm list`
- Check auth: `notebooklm auth check --test`
- Status checks and artifact listing
- Chat queries without note-saving

**Require confirmation before running:**
- Create or delete notebooks
- Add or remove sources
- Generate artifacts (flashcards, quiz, podcast, video, report, mind map, slide deck)
- Download files

---

## Primary Use Case: Flashcards from Wiki Personal Logs

When the user asks to create flashcards from a wiki topic:

1. Identify the relevant article(s) under `wiki/performance/`, `wiki/career/`, `wiki/relationships/`, or `wiki/wellbeing/`
2. Read the article(s) - focus on the Personal Log table and Key Takeaways section
3. Confirm scope with the user before proceeding
4. Run the orchestration script (see below) or execute the steps manually:

```bash
# Create notebook
NOTEBOOK_ID=$(notebooklm create "Personal MBA: [Topic]" --json | python3 -c "import sys,json; print(json.load(sys.stdin)['notebook']['id'])")

# Add wiki content as file source
# NOTE: resolve the path first — on macOS /tmp is a symlink and uploads of
# symlinked paths are refused. Use $(python3 -c "import os;print(os.path.realpath('/tmp/wiki_content.txt'))")
SOURCE_ID=$(notebooklm source add -n "$NOTEBOOK_ID" /private/tmp/wiki_content.txt --json | python3 -c "import sys,json; print(json.load(sys.stdin)['source']['id'])")

# Wait for source processing (30 seconds to 10 minutes)
notebooklm source wait -n "$NOTEBOOK_ID" "$SOURCE_ID"

# Generate flashcards
TASK_ID=$(notebooklm generate flashcards -n "$NOTEBOOK_ID" --json | python3 -c "import sys,json; print(json.load(sys.stdin)['task_id'])")

# Wait and download
notebooklm artifact wait -n "$NOTEBOOK_ID" "$TASK_ID"
notebooklm download flashcards -n "$NOTEBOOK_ID" -a "$TASK_ID" ~/Downloads/flashcards.md --force --format markdown
```

---

## Orchestration Script

For batch processing (all articles in a topic folder → one notebook):

```bash
python ~/.claude/skills/notebooklm-py/scripts/run_notebooklm.py \
  --topic working-with-others \
  --artifact flashcards \
  --output ~/Downloads/
```

Available topics: `working-with-others`, `working-with-yourself`, `the-human-mind`, `career`, `relationships`, `wellbeing`

Available artifacts: `flashcards`, `quiz`, `podcast`, `mind-map`, `report`

The script reads all `.md` articles in the topic folder, extracts Key Takeaways and Personal Log sections, creates a notebook, adds the content as a source, generates the artifact, and downloads it.

---

## Supported Artifact Types

| Artifact | CLI command | Output format | Typical duration |
|----------|-------------|---------------|-----------------|
| Flashcards | `generate flashcards` | .json / .md / .html | 5-15 minutes |
| Quiz | `generate quiz` | .json / .md / .html | 5-15 minutes |
| Podcast | `generate audio` | .mp3 | 10-20 minutes |
| Mind map | `generate mind-map` | .json | 5-10 minutes |
| Report | `generate report` | .md | 5-10 minutes |
| Slide deck | `generate slide-deck` | .pdf / .pptx | 10-20 minutes |

---

## Processing Times

| Operation | Expected duration |
|-----------|------------------|
| Source processing | 30 seconds to 10 minutes |
| Flashcard / quiz generation | 5-15 minutes |
| Podcast generation | 10-20 minutes |
| Mind map / report | 5-10 minutes |

For long operations, use the subagent pattern from the repo (spawn a background task to wait and download while the main conversation continues).

---

## Auth Notes

- Auth uses Google OAuth browser flow; cookie file stored locally by `notebooklm-py`
- Re-run `notebooklm login` if you get authentication errors
- Google APIs: route direct in HK - do NOT route through VPN (same rule as Google Sheets)
- Anthropic API is NOT used by this skill; no VPN requirement applies

---

## Error Handling

| Error | Likely cause | Fix |
|-------|-------------|-----|
| Auth failure | Expired OAuth cookie | `notebooklm login` |
| Source timeout | Large file or slow processing | Re-check with `notebooklm source list -n <notebook_id>` |
| Generation timeout | Long-running task | Check `notebooklm artifact list -n <notebook_id> --json` |
| Rate limit | Too many concurrent requests | Wait and retry |
| CLI not found | Package not installed | `pip install "notebooklm-py[browser]"` |

---

## JSON Output Pattern

Commands that support `--json` return structured data for scripting:

- `create` → `{ "notebook": { "id": "..." } }`
- `source add` → `{ "source": { "id": "..." } }`
- `generate *` → `{ "task_id": "...", "status": "..." }`

---

## Exit Codes

| Code | Meaning |
|------|---------|
| 0 | Success |
| 1 | Error (not found, processing failed, auth failure) |
| 2 | Timeout (wait commands only) |
