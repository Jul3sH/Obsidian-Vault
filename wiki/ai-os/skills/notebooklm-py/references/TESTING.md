<!-- Mirror of ~/.claude/skills/notebooklm-py/references/TESTING.md — do not edit here; edit the source file -->
# TESTING.md — notebooklm-py

tags: [technical, skills, testing, notebooklm]

> *Pre-flight checks, gotchas, and the test log. Command signatures here are
> verified against notebooklm-py CLI v0.7.0 (2026-07-29).*

---

## Key Takeaways

- The script was **entirely non-functional** from the v0.7.0 CLI upgrade until 2026-07-29
- Seven independent breakages, any one of which was fatal
- Repaired and verified end to end: wellbeing topic → 433-line flashcard deck
- Six were findable by reading `--help`; the seventh only by executing

---

## Pre-Flight Checklist

Run these before any debugging session:

| # | Check | Command | Catches |
|---|-------|---------|---------|
| 1 | Package installed | `notebooklm --version` | Missing package |
| 2 | Auth working | `notebooklm auth check --test --json` | Expired OAuth cookie |
| 3 | Playwright installed | `python -c "from playwright.sync_api import sync_playwright; print('ok')"` | Missing browser automation |
| 4 | Wiki topic folder exists | `ls ~/Obsidian\ Vault/wiki/wellbeing/` | Wrong WIKI_ROOT path |
| 5 | VPN routing | Google APIs are direct — do NOT route through VPN | Auth failure from wrong exit IP |
| 6 | List notebooks | `notebooklm list --json` | End-to-end auth check |
| 7 | Binary resolves for scripts | `python -c "import sys;sys.path.insert(0,'scripts');import run_notebooklm as r;print(r.notebooklm_bin())"` | The shell-alias trap (see Gotchas) |

## VPN Rule

Google APIs (including NotebookLM) must be routed direct, not through VPN. VPN exit IPs are blocked by Google in some cases. ExpressVPN bypass: all traffic through VPN except IPs in `160.79.104.0/21`. Google is outside this range and routes direct automatically.

---

## Test Log

| Date | What | Why | Revealed |
|------|------|-----|----------|
| 2026-07-29 | Full run: `--topic wellbeing --artifact flashcards` | First-ever execution; script had never been run since the v0.7.0 CLI upgrade | **7 fatal breakages** (below). After repair: exit 0, 433-line flashcard deck from 7 articles / 22,468 chars |

### 2026-07-29 — Repair after CLI v0.7.0 drift

| # | Symptom | Cause | Fix |
|---|---------|-------|-----|
| 1 | `FileNotFoundError: notebooklm` | `notebooklm` is a **shell alias**, not on PATH. `subprocess` cannot see aliases. | `notebooklm_bin()` resolves `$NOTEBOOKLM_BIN`, then known venv/brew paths, then `shutil.which` |
| 2 | `No such command 'notebook'` | v0.7.0 dropped the `notebook` command group | `notebooklm create "Title"` |
| 3 | `source add file ...` rejected | no `file` subcommand in v0.7.0 | `source add -n <nb> <path>` |
| 4 | notebook passed positionally to `source wait` / `artifact wait` | v0.7.0 takes it as `-n` | `-n <nb>` |
| 5 | `download ... --output <dir>` rejected | no `--output` flag; path is positional, artifact is `-a` | `download <type> -n <nb> -a <id> <path> --force` |
| 6 | `--format md` rejected | valid values are `json\|markdown\|html` | mapping now stores `(format_flag, extension)` per artifact type |
| 7 | `VALIDATION_ERROR: Path is a symlink` | On macOS `/tmp` symlinks to `/private/tmp`; v0.7.0 refuses symlinked upload paths as an exfiltration guard | resolve the temp path rather than passing `--follow-symlinks` |

```python
TMP_SOURCE = (Path(tempfile.gettempdir()) / "notebooklm_wiki_content.txt").resolve()
```

**Lesson:** breakages 1-6 were findable by reading `--help`. Breakage 7 was only
findable by execution. A static review would have declared the script fixed while
it was still dead. Do not report a repair verified without running it.

---

## Not yet tested

| Gap | Risk | How to close |
|-----|------|--------------|
| `--artifact podcast` (audio, no `--format` flag) | Medium — the only path with a `None` format flag | Run one podcast generation |
| `--artifact mind-map` (json) | Low | Run one |
| `--artifact quiz` / `report` | Low — identical code path to flashcards | — |
| Topics other than `wellbeing` | Low — only affects input size | — |

---

## Known Gotchas

- **`notebooklm` is a shell alias, not a binary on PATH.** Scripts must resolve the real path; a bare `notebooklm` in a script fails, silently if stderr is redirected.
- `notebooklm login` must be run in a terminal with a display browser available — does not work headless
- Source processing for a large wiki topic folder (30+ articles) can take up to 10 minutes — `source wait` blocks until ready
- Rate limiting on generation: if multiple notebooks are generated simultaneously, tasks may queue silently
- The CLI writes warnings to **stderr** and data to **stdout**, so `--json` parsing from stdout is safe
- `--json` is required for scripted parsing; without it output is human-readable and not parseable

---

## First Run Steps

1. Install: `pip install "notebooklm-py[browser]" && playwright install chromium`
2. Auth: `notebooklm login` (opens browser, complete Google OAuth)
3. Verify: `notebooklm auth check --test --json`
4. Smoke test: `notebooklm list --json`
5. Test with a small topic (`wellbeing`) before running a large batch

---

## Related

- [[youtube-notebook]] — sibling skill on the same CLI, for YouTube channels
- [[notebooklm-cli]] — full verified v0.7.0 command surface
