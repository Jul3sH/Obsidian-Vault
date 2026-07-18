<!-- Mirror of ~/.claude/skills/notebooklm-py/scripts/run_notebooklm.py — do not edit here; edit the source file -->
<!-- Python scripts are stored as .md with embedded code blocks in the wiki per skill-conventions.md -->

# run_notebooklm.py

**Source:** `~/.claude/skills/notebooklm-py/scripts/run_notebooklm.py`

Orchestration script: reads all wiki articles in a topic folder, creates a NotebookLM notebook with the content as source, and generates a study artifact (flashcards, quiz, podcast, mind map, or report).

## Usage

```bash
python ~/.claude/skills/notebooklm-py/scripts/run_notebooklm.py \
  --topic <topic> \
  --artifact <type> \
  [--output <path>]
```

| Argument | Required | Values |
|----------|----------|--------|
| `--topic` | Yes | `working-with-others`, `working-with-yourself`, `the-human-mind`, `career`, `relationships`, `wellbeing` |
| `--artifact` | Yes | `flashcards`, `quiz`, `podcast`, `mind-map`, `report` |
| `--output` | No | Output directory path (default: `~/Downloads/`) |

## Script

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
import subprocess
import sys
from pathlib import Path

WIKI_ROOT = Path.home() / "Obsidian Vault" / "wiki"
DEFAULT_OUTPUT = Path.home() / "Downloads"
TMP_SOURCE = Path("/tmp/notebooklm_wiki_content.txt")

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

ARTIFACT_FORMATS = {
    "flashcards": "md",
    "quiz": "md",
    "podcast": "mp3",
    "mind-map": "json",
    "report": "md",
}


def run(cmd: list[str], capture: bool = True) -> str:
    result = subprocess.run(cmd, capture_output=capture, text=True)
    if result.returncode != 0:
        print(f"Error running {cmd[0]}: {result.stderr.strip()}", file=sys.stderr)
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
    raw = run(["notebooklm", "notebook", "create", notebook_title, "--json"])
    notebook_id = parse_json_field(raw, "notebook", "id")
    print(f"Notebook ID: {notebook_id}")

    print("Adding wiki content as source...")
    raw = run(["notebooklm", "source", "add", "file", notebook_id, str(TMP_SOURCE), "--json"])
    source_id = parse_json_field(raw, "source", "id")
    print(f"Source ID: {source_id}")

    print("Waiting for source processing (may take several minutes)...")
    run(["notebooklm", "source", "wait", notebook_id, source_id], capture=False)

    print(f"Generating {args.artifact}...")
    artifact_cmd = ARTIFACT_COMMANDS[args.artifact]
    raw = run(["notebooklm", "generate", artifact_cmd, notebook_id, "--json"])
    task_id = parse_json_field(raw, "task_id")
    print(f"Task ID: {task_id}")

    print(f"Waiting for {args.artifact} generation (this may take 5-20 minutes)...")
    run(["notebooklm", "artifact", "wait", notebook_id, task_id], capture=False)

    fmt = ARTIFACT_FORMATS[args.artifact]
    print(f"Downloading to {output_dir}...")
    run([
        "notebooklm", "download", artifact_cmd,
        notebook_id, task_id,
        "--format", fmt,
        "--output", str(output_dir),
    ], capture=False)

    TMP_SOURCE.unlink(missing_ok=True)
    print(f"Done. Check {output_dir} for your {args.artifact}.")


if __name__ == "__main__":
    main()
```

## Notes

- Uses `notebooklm source add file` (not `add text`) to handle large content without shell argument length issues
- Writes wiki content to `/tmp/notebooklm_wiki_content.txt` as an intermediate file; cleaned up on exit
- Skips `_index.md` files (starts with `_`) to avoid ingesting navigation content
- No API keys required: auth handled by `notebooklm login` OAuth cookie
- No VPN needed: Google APIs route direct in HK
