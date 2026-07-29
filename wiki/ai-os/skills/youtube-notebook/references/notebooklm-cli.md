<!-- Mirror of ~/.claude/skills/youtube-notebook/references/notebooklm-cli.md — do not edit here; edit the source file -->
# notebooklm CLI - Verified Command Surface (v0.7.0)

tags: [technical, skills, notebooklm, cli, reference]

> *Command signatures verified by execution against notebooklm-py v0.7.0 on 2026-07-29.
> The upstream package is an unofficial client and its CLI surface has already changed
> once in a breaking way. Re-verify with `--help` before assuming any signature here.*

---

## Key Takeaways

- `notebooklm` is a **shell alias**, not a binary on PATH: scripts must resolve the real path
- Notebook is passed with `-n/--notebook`, never as a positional argument
- `artifact get` returns `status` at the **top level**, not nested under `artifact`
- Warnings go to stderr, data to stdout, so `--json` parsing from stdout is safe
- v0.7.0 dropped the `notebook` command group and the `source add file` subcommand
- On macOS, `/tmp` is a symlink and file uploads from it are refused: resolve the path

---

## Gotcha 1: the alias problem (cost 19 silent failures)

```bash
$ which notebooklm
notebooklm: aliased to ~/.venvs/notebooklm/bin/notebooklm
```

```python
>>> shutil.which("notebooklm")
None                       # not on PATH
>>> subprocess.run(["notebooklm", "--version"])
FileNotFoundError
```

Shell aliases exist only in interactive shells. Neither `bash script.sh` nor
Python `subprocess` can see them. A bare `notebooklm` inside a script fails, and
if stderr is redirected the failure is **silent**.

Always resolve explicitly. `scripts/nlm.py::resolve_binary()` checks
`$NOTEBOOKLM_BIN`, then known venv/homebrew locations, then `shutil.which`.

## Gotcha 2: `artifact get` status is top-level

```json
{ "id": "...", "title": "...", "status": "completed", "status_id": 3, "found": true }
```

Not `{"artifact": {"status": ...}}`. Parsing the nested shape yields an empty
string, which silently reads as "not complete" and skips every item.

## Gotcha 3: `/tmp` is a symlink on macOS and file uploads are refused

```
VALIDATION_ERROR: Path is a symlink; pass --follow-symlinks to follow it
explicitly. Refusing to upload: /tmp/wiki_content.txt
```

`/tmp` symlinks to `/private/tmp`, and `source add` rejects symlinked paths as an
exfiltration guard (a workspace symlink could otherwise point at `/etc/passwd`).

Resolve the path rather than passing `--follow-symlinks`, which would disable the
guard entirely:

```python
TMP = (Path(tempfile.gettempdir()) / "content.txt").resolve()   # -> /private/tmp/...
```

Affects file sources only. YouTube URL sources are unaffected.

## Gotcha 4: stdout vs stderr

The RPC layer emits `WARNING ... Byte-count mismatch in chunked response` to
**stderr** during normal healthy operation. It is tolerated by the client and does
not indicate failure. Data goes to **stdout**, so JSON parsing is unaffected as
long as you read stdout only.

---

## Verified signatures

### Session
| Command | Signature |
|---------|-----------|
| Login | `notebooklm login` |
| Auth check | `notebooklm auth check --test --json` -> `{"status": "ok", ...}` |

### Notebooks
| Action | v0.7.0 | Pre-0.7 (BROKEN) |
|--------|--------|------------------|
| List | `notebooklm list --json` | - |
| Create | `notebooklm create "Title" --json` | ~~`notebooklm notebook create`~~ |
| Delete | `notebooklm delete -n <id> --yes` | ~~`delete <id> --force`~~ |
| Rename | `notebooklm rename -n <id> "New"` | - |

`create` returns `{"notebook": {"id": "..."}}`.

There is **no `notebook` command group** in v0.7.0.

### Sources
| Action | Signature |
|--------|-----------|
| Add | `notebooklm source add -n <nb> --type youtube <url> --json` |
| Add file | `notebooklm source add -n <nb> /path/to/file --json` |
| List | `notebooklm source list -n <nb> --json` |
| Rename | `notebooklm source rename -n <nb> <source_id> "Title"` |
| Wait | `notebooklm source wait -n <nb> <source_id>` |

`source add` returns `{"source": {"id", "title", "type", "url"}}`.
Type is auto-detected; `--type` overrides. There is **no `file` subcommand** -
`source add file <nb> <path>` fails.

`--title` applies only to text and uploaded-file sources. **YouTube sources take
their title from YouTube**, so a per-source title must be set with
`source rename` after adding.

`source list` entries carry `status` (`ready`) and `status_id` (`2`).

### Artifacts
| Action | Signature |
|--------|-----------|
| Generate briefing | `notebooklm generate report --format briefing-doc -n <nb> -s <src> --no-wait --json` |
| Wait | `notebooklm artifact wait -n <nb> <task_id> --timeout 900` |
| Get | `notebooklm artifact get -n <nb> <id> --json` |
| List | `notebooklm artifact list -n <nb> --json` |
| Rename | `notebooklm artifact rename -n <nb> <id> "Title"` |
| Download | `notebooklm download report -n <nb> -a <id> <output_path> --force` |

`generate` returns `{"task_id": "...", "status": "pending"}`. The `task_id` **is**
the artifact id.

`--format` on `generate report`: `briefing-doc` (default) | `study-guide` |
`blog-post` | `custom`. `-s/--source` may repeat to scope to specific sources;
**omitting it uses every source in the notebook**, which is what makes per-source
briefings possible.

`--format` on `download`: `json` | `markdown` | `html`. Note `md` is **not** valid.
Download output path is **positional**; there is no `--output` flag.

### Generate/download types
`audio`, `cinematic-video`, `data-table`, `flashcards`, `infographic`,
`mind-map`, `quiz`, `report`, `slide-deck`, `video` (+ `revise-slide` on generate).

---

## Exit codes

| Code | Meaning |
|------|---------|
| 0 | Success |
| 1 | Error (not found, processing failed, auth failure) |
| 2 | Timeout (wait commands only) |

---

## Related

- [[youtube-notebook]] - the skill using this surface
- [[notebooklm-py]] - the wiki-content/flashcards skill on the same CLI
