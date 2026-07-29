<!-- Mirror of ~/.claude/skills/notebooklm-py/scripts/run_notebooklm.py — do not edit here; edit the source file -->
<!-- Python scripts are stored as .md with embedded code blocks in the wiki per skill-conventions.md -->

# run_notebooklm.py

tags: [technical, skills, notebooklm, scripts]

> *Wiki topic folder -> one concatenated source -> one artifact. Repaired 2026-07-29 after being found entirely non-functional against CLI v0.7.0 (7 breakages).*

**Source:** `~/.claude/skills/notebooklm-py/scripts/run_notebooklm.py`

---

```python
#!/usr/bin/env python3
"""
run_notebooklm.py — Generate NotebookLM artifacts from wiki Personal MBA content.

Usage:
    python run_notebooklm.py --topic <topic> --artifact <type> [--output <path>]

Examples:
    python run_notebooklm.py --topic working-with-others --artifact flashcards
    python run_notebooklm.py --topic the-human-mind --artifact quiz --output ~/Downloads/
"""

import argparse
import json
import os
import shutil
import subprocess
import sys
import tempfile
from pathlib import Path

WIKI_ROOT = Path.home() / "Obsidian Vault" / "wiki"
DEFAULT_OUTPUT = Path.home() / "Downloads"
# .resolve() is REQUIRED: on macOS /tmp is a symlink to /private/tmp, and
# `source add` refuses symlinked paths ("pass --follow-symlinks") as an
# exfiltration guard. Resolving up front avoids relaxing that guard.
TMP_SOURCE = (Path(tempfile.gettempdir()) / "notebooklm_wiki_content.txt").resolve()

# `notebooklm` is a SHELL ALIAS, not a binary on PATH. subprocess never sees
# shell aliases, so a bare "notebooklm" raises FileNotFoundError. Resolve the
# real executable once, up front.
NLM_CANDIDATES = [
    Path.home() / ".venvs" / "notebooklm" / "bin" / "notebooklm",
    Path("/opt/homebrew/bin/notebooklm"),
    Path("/usr/local/bin/notebooklm"),
]


def notebooklm_bin() -> str:
    env = os.environ.get("NOTEBOOKLM_BIN")
    if env and Path(env).expanduser().exists():
        return str(Path(env).expanduser())
    for cand in NLM_CANDIDATES:
        if cand.exists():
            return str(cand)
    found = shutil.which("notebooklm")
    if found:
        return found
    print(
        'notebooklm CLI not found. Install with: pip install "notebooklm-py[browser]"\n'
        "or set NOTEBOOKLM_BIN. A shell alias is not enough - scripts cannot see aliases.",
        file=sys.stderr,
    )
    sys.exit(1)


NLM = None

TOPIC_FOLDERS = {
    "working-with-others": WIKI_ROOT / "performance" / "working-with-others",
    "working-with-yourself": WIKI_ROOT / "performance" / "working-with-yourself",
    "the-human-mind": WIKI_ROOT / "performance" / "the-human-mind",
    "career": WIKI_ROOT / "career",
    "relationships": WIKI_ROOT / "relationships",
    "wellbeing": WIKI_ROOT / "wellbeing",
}

ARTIFACT_COMMANDS = {
    "flashcards": "flashcards",
    "quiz": "quiz",
    "podcast": "audio",
    "mind-map": "mind-map",
    "report": "report",
}

# (download --format value, file extension). v0.7.0 accepts json|markdown|html
# only: "md" is NOT valid. Audio takes no --format flag.
ARTIFACT_FORMATS = {
    "flashcards": ("markdown", "md"),
    "quiz": ("markdown", "md"),
    "podcast": (None, "mp3"),
    "mind-map": ("json", "json"),
    "report": ("markdown", "md"),
}


def run(args: list[str], capture: bool = True) -> str:
    """Run a notebooklm subcommand. `args` excludes the executable itself."""
    cmd = [NLM, *args]
    result = subprocess.run(cmd, capture_output=capture, text=True)
    if result.returncode != 0:
        err = (result.stderr or "").strip() if capture else ""
        print(f"Error running: notebooklm {' '.join(args)}\n{err}", file=sys.stderr)
        sys.exit(1)
    return result.stdout.strip() if capture else ""


def extract_wiki_content(folder: Path) -> str:
    articles = sorted(folder.glob("*.md"))
    sections = []
    for article in articles:
        if article.name.startswith("_"):
            continue
        text = article.read_text(encoding="utf-8")
        title = article.stem.replace("-", " ").title()
        sections.append(f"# {title}\n\n{text}")
    if not sections:
        print(f"No articles found in {folder}", file=sys.stderr)
        sys.exit(1)
    return "\n\n---\n\n".join(sections)


def parse_json_field(raw: str, *keys: str) -> str:
    data = json.loads(raw)
    result = data
    for key in keys:
        result = result[key]
    return str(result)


def main() -> None:
    parser = argparse.ArgumentParser(
        description="Generate NotebookLM artifacts from wiki Personal MBA content"
    )
    parser.add_argument("--topic", required=True, choices=list(TOPIC_FOLDERS.keys()))
    parser.add_argument("--artifact", required=True, choices=list(ARTIFACT_COMMANDS.keys()))
    parser.add_argument("--output", default=str(DEFAULT_OUTPUT))
    args = parser.parse_args()

    global NLM
    NLM = notebooklm_bin()

    folder = TOPIC_FOLDERS[args.topic]
    if not folder.exists():
        print(f"Wiki topic folder not found: {folder}", file=sys.stderr)
        sys.exit(1)

    output_dir = Path(args.output).expanduser()
    output_dir.mkdir(parents=True, exist_ok=True)
    notebook_title = f"Personal MBA: {args.topic.replace('-', ' ').title()}"

    print(f"Reading wiki content from: {folder}")
    content = extract_wiki_content(folder)
    TMP_SOURCE.write_text(content, encoding="utf-8")
    print(f"Extracted {len(content):,} characters from {len(list(folder.glob('*.md')))} articles")

    print(f"Creating notebook: {notebook_title}")
    raw = run(["create", notebook_title, "--json"])
    notebook_id = parse_json_field(raw, "notebook", "id")
    print(f"Notebook ID: {notebook_id}")

    print("Adding wiki content as source...")
    raw = run(["source", "add", "-n", notebook_id, str(TMP_SOURCE), "--json"])
    source_id = parse_json_field(raw, "source", "id")
    print(f"Source ID: {source_id}")

    print("Waiting for source processing (may take several minutes)...")
    run(["source", "wait", "-n", notebook_id, source_id], capture=False)

    print(f"Generating {args.artifact}...")
    artifact_cmd = ARTIFACT_COMMANDS[args.artifact]
    raw = run(["generate", artifact_cmd, "-n", notebook_id, "--json"])
    task_id = parse_json_field(raw, "task_id")
    print(f"Task ID: {task_id}")

    print(f"Waiting for {args.artifact} generation (this may take 5-20 minutes)...")
    run(["artifact", "wait", "-n", notebook_id, task_id], capture=False)

    fmt, ext = ARTIFACT_FORMATS[args.artifact]
    target = output_dir / f"{notebook_title.replace('/', '-')}.{ext}"
    print(f"Downloading to {target}...")
    dl = ["download", artifact_cmd, "-n", notebook_id, "-a", task_id,
          str(target), "--force"]
    if fmt:
        dl += ["--format", fmt]
    run(dl, capture=False)

    TMP_SOURCE.unlink(missing_ok=True)
    print(f"Done. Check {output_dir} for your {args.artifact}.")


if __name__ == "__main__":
    main()

```
