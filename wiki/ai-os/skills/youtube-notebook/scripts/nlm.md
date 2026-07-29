<!-- Mirror of ~/.claude/skills/youtube-notebook/scripts/nlm.py — do not edit here; edit the source file -->
<!-- Python scripts are stored as .md with embedded code blocks in the wiki per skill-conventions.md -->

# nlm.py

tags: [technical, skills, notebooklm, scripts]

> *Shared NotebookLM CLI wrapper. Exists because `notebooklm` is a shell alias that scripts cannot see.*

**Source:** `~/.claude/skills/youtube-notebook/scripts/nlm.py`

---

```python
#!/usr/bin/env python3
"""
nlm.py - shared NotebookLM CLI wrapper for the youtube-notebook skill.

Exists for one reason: `notebooklm` is a SHELL ALIAS on this machine, not a
binary on PATH. `subprocess.run(["notebooklm", ...])` raises FileNotFoundError
because subprocess never sees shell aliases. Every call must resolve the real
binary first. See references/notebooklm-cli.md.
"""
from __future__ import annotations

import json
import os
import shutil
import subprocess
from pathlib import Path

CANDIDATE_PATHS = [
    Path.home() / ".venvs" / "notebooklm" / "bin" / "notebooklm",
    Path("/opt/homebrew/bin/notebooklm"),
    Path("/usr/local/bin/notebooklm"),
]

_BIN: str | None = None


class NlmError(RuntimeError):
    pass


def resolve_binary() -> str:
    """Find the real notebooklm executable. Env override wins."""
    global _BIN
    if _BIN:
        return _BIN
    env = os.environ.get("NOTEBOOKLM_BIN")
    if env and Path(env).expanduser().exists():
        _BIN = str(Path(env).expanduser())
        return _BIN
    for cand in CANDIDATE_PATHS:
        if cand.exists():
            _BIN = str(cand)
            return _BIN
    which = shutil.which("notebooklm")
    if which:
        _BIN = which
        return _BIN
    raise NlmError(
        "notebooklm CLI not found. Install with:\n"
        '  pip install "notebooklm-py[browser]"\n'
        "or set NOTEBOOKLM_BIN to the full path of the executable.\n"
        "Note: a shell alias is NOT enough - scripts cannot see aliases."
    )


def nlm(*args, json_out: bool = False, check: bool = True, timeout: int = 900):
    """Run a notebooklm command. Returns parsed JSON (json_out) or stdout text.

    The CLI writes progress/warnings to stderr and data to stdout, so stdout
    stays clean JSON even when the transport logs byte-count warnings.
    """
    cmd = [resolve_binary(), *[str(a) for a in args]]
    if json_out:
        cmd.append("--json")
    proc = subprocess.run(cmd, capture_output=True, text=True, timeout=timeout)
    if check and proc.returncode != 0:
        raise NlmError(
            f"command failed (rc={proc.returncode}): {' '.join(cmd[1:])}\n"
            f"{proc.stderr.strip()[:600]}"
        )
    if not json_out:
        return proc.stdout.strip()
    try:
        return json.loads(proc.stdout)
    except json.JSONDecodeError as exc:
        raise NlmError(
            f"expected JSON from: {' '.join(cmd[1:])}\n"
            f"stdout: {proc.stdout[:300]}\nstderr: {proc.stderr[:300]}"
        ) from exc


def preflight() -> dict:
    """Verify the CLI is present and authenticated before doing any work."""
    binary = resolve_binary()
    data = nlm("auth", "check", "--test", json_out=True, timeout=120)
    ok = data.get("status") == "ok"
    if not ok:
        raise NlmError(
            f"NotebookLM auth is not healthy: {data}\nRun: {binary} login"
        )
    return {"binary": binary, "auth": data.get("status")}


def yt_dlp_binary() -> str:
    which = shutil.which("yt-dlp")
    if not which:
        raise NlmError(
            "yt-dlp not found. Install with: brew install yt-dlp"
        )
    return which

```
