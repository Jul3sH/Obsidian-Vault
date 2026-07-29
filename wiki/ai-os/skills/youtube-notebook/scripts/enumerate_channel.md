<!-- Mirror of ~/.claude/skills/youtube-notebook/scripts/enumerate_channel.py — do not edit here; edit the source file -->
<!-- Python scripts are stored as .md with embedded code blocks in the wiki per skill-conventions.md -->

# enumerate_channel.py

tags: [technical, skills, notebooklm, scripts]

> *Enumerates a channel window and proves completeness two independent ways. Applies the deterministic date filter only; topic filtering is left to the agent, in the open.*

**Source:** `~/.claude/skills/youtube-notebook/scripts/enumerate_channel.py`

---

```python
#!/usr/bin/env python3
"""
enumerate_channel.py - enumerate a YouTube channel's uploads, verify the
enumeration is complete, and apply a DETERMINISTIC date filter.

Emits a manifest JSON consumed by build_notebook.py.

Topic filtering is deliberately NOT done here. Date filtering is provable;
topic filtering is a judgement call. This script emits every date-qualifying
video (with descriptions if asked) so the agent can apply a topic filter in
the open and show the user what it excluded.

Completeness is established two independent ways and then diffed:
  1. Per-tab walk of /videos, /shorts, /streams reading real upload_date
     metadata, continuing past the window's start boundary so truncation
     is detectable.
  2. A flat pull of the channel's uploads playlist (UU...), which contains
     every upload regardless of tab.
Any ID present in path 2 within the window but absent from path 1 is a
verification failure and is reported loudly.

Usage:
  python enumerate_channel.py --channel @NateBJones --month 2026-06 \\
      --tabs videos --out manifest.json
  python enumerate_channel.py --channel @NateBJones \\
      --since 2026-11-01 --until 2026-11-30 --tabs videos,shorts \\
      --descriptions --out manifest.json
"""
from __future__ import annotations

import argparse
import calendar
import json
import subprocess
import sys
from datetime import date, datetime
from pathlib import Path

sys.path.insert(0, str(Path(__file__).resolve().parent))
from nlm import yt_dlp_binary  # noqa: E402

TABS = ("videos", "shorts", "streams")
PAGE = 60          # entries fetched per widening step
MAX_ENTRIES = 900  # hard stop per tab


def log(msg: str) -> None:
    print(msg, file=sys.stderr, flush=True)


def channel_url(channel: str) -> str:
    c = channel.strip().rstrip("/")
    if c.startswith("http://") or c.startswith("https://"):
        for suffix in ("/videos", "/shorts", "/streams", "/featured"):
            if c.endswith(suffix):
                c = c[: -len(suffix)]
        return c
    if not c.startswith("@"):
        c = "@" + c
    return f"https://www.youtube.com/{c}"


def ytdlp(args: list[str], timeout: int = 900) -> list[str]:
    proc = subprocess.run(
        [yt_dlp_binary(), *args], capture_output=True, text=True, timeout=timeout
    )
    if proc.returncode != 0 and not proc.stdout.strip():
        raise RuntimeError(f"yt-dlp failed: {' '.join(args)}\n{proc.stderr[:500]}")
    return [ln for ln in proc.stdout.splitlines() if ln.strip()]


def fetch_tab(base: str, tab: str, since: str, want_desc: bool) -> list[dict]:
    """Walk a tab newest-first until we pass `since`, so the boundary is proven.

    Returns entries as dicts. Includes entries older than `since`: the caller
    filters. Their presence is the evidence that we did not truncate.
    """
    url = f"{base}/{tab}"
    fields = "%(upload_date)s\t%(id)s\t%(title)s\t%(channel_id)s"
    if want_desc:
        fields += "\t%(description).400s"
    rows: dict[str, dict] = {}
    start, crossed = 1, False
    while start <= MAX_ENTRIES and not crossed:
        end = start + PAGE - 1
        try:
            lines = ytdlp([
                "--skip-download", "--no-warnings", "--ignore-errors",
                "--playlist-start", str(start), "--playlist-end", str(end),
                "--print", fields, url,
            ])
        except RuntimeError as exc:
            log(f"  ! {tab}: {exc}")
            break
        if not lines:
            log(f"  {tab}: exhausted at entry {start}")
            break
        for ln in lines:
            parts = ln.split("\t")
            if len(parts) < 4 or not parts[0] or parts[0] == "NA":
                continue
            rows[parts[1]] = {
                "upload_date": parts[0],
                "id": parts[1],
                "title": parts[2],
                "channel_id": parts[3],
                "description": parts[4] if len(parts) > 4 else "",
                "tab": tab,
            }
            if parts[0] < since:
                crossed = True
        log(f"  {tab}: {len(rows)} fetched, oldest {min(r['upload_date'] for r in rows.values())}")
        start = end + 1
    if not crossed and rows:
        log(f"  ! {tab}: reached limit WITHOUT crossing {since} - may be truncated")
    return list(rows.values())


def date_ids(ids: list[str]) -> dict[str, str]:
    """Date a small set of video IDs individually. Used only for gap triage."""
    out: dict[str, str] = {}
    for vid in ids:
        try:
            lines = ytdlp([
                "--skip-download", "--no-warnings", "--print", "%(upload_date)s",
                f"https://www.youtube.com/watch?v={vid}",
            ], timeout=180)
            if lines:
                out[vid] = lines[0]
        except RuntimeError:
            out[vid] = "UNKNOWN"
    return out


def uploads_crosscheck(channel_id: str, since: str) -> tuple[list[str], bool]:
    """Flat-pull the uploads playlist. Returns (ids, spans_window)."""
    if not channel_id or not channel_id.startswith("UC"):
        return [], False
    pl = "UU" + channel_id[2:]
    ids: list[str] = []
    start = 1
    while start <= MAX_ENTRIES:
        end = start + 100 - 1
        try:
            lines = ytdlp([
                "--flat-playlist", "--no-warnings", "--ignore-errors",
                "--playlist-start", str(start), "--playlist-end", str(end),
                "--print", "%(id)s",
                f"https://www.youtube.com/playlist?list={pl}",
            ])
        except RuntimeError as exc:
            log(f"  ! uploads playlist: {exc}")
            break
        if not lines:
            break
        ids.extend(lines)
        # Cheap boundary probe: date the oldest entry we just pulled.
        try:
            probe = ytdlp([
                "--skip-download", "--no-warnings", "--print", "%(upload_date)s",
                f"https://www.youtube.com/watch?v={lines[-1]}",
            ], timeout=180)
            if probe and probe[0] < since:
                return ids, True
        except RuntimeError:
            pass
        start = end + 1
    return ids, False


def resolve_window(args) -> tuple[str, str, str]:
    if args.month:
        y, m = (int(x) for x in args.month.split("-"))
        last = calendar.monthrange(y, m)[1]
        return (f"{y}{m:02d}01", f"{y}{m:02d}{last:02d}",
                date(y, m, 1).strftime("%B %Y"))
    if not (args.since and args.until):
        raise SystemExit("Provide --month YYYY-MM, or both --since and --until.")
    s = args.since.replace("-", "")
    u = args.until.replace("-", "")
    label = (f"{datetime.strptime(s, '%Y%m%d'):%-d %b %Y} to "
             f"{datetime.strptime(u, '%Y%m%d'):%-d %b %Y}")
    return s, u, label


def main() -> None:
    p = argparse.ArgumentParser(description="Enumerate and verify a YouTube channel window")
    p.add_argument("--channel", required=True, help="@handle or full channel URL")
    p.add_argument("--month", help="YYYY-MM shorthand for a whole calendar month")
    p.add_argument("--since", help="YYYY-MM-DD inclusive")
    p.add_argument("--until", help="YYYY-MM-DD inclusive")
    p.add_argument("--tabs", default="videos",
                   help="comma-separated: videos,shorts,streams (default: videos)")
    p.add_argument("--descriptions", action="store_true",
                   help="fetch truncated descriptions to support topic filtering")
    p.add_argument("--out", default="manifest.json")
    args = p.parse_args()

    since, until, label = resolve_window(args)
    tabs = [t.strip() for t in args.tabs.split(",") if t.strip() in TABS]
    if not tabs:
        raise SystemExit(f"--tabs must name at least one of {TABS}")

    base = channel_url(args.channel)
    log(f"Channel : {base}")
    log(f"Window  : {label}  ({since}..{until})")
    log(f"Tabs    : {', '.join(tabs)}")

    # Verification walks EVERY tab, even when only some are selected. The
    # uploads playlist mixes all content types, so comparing it against a
    # single tab would flag every Short as a false gap.
    all_rows: list[dict] = []
    for tab in TABS:
        log(f"Walking /{tab} ...{'' if tab in tabs else '  (verification only)'}")
        all_rows.extend(fetch_tab(base, tab, since, args.descriptions and tab in tabs))

    if not all_rows:
        raise SystemExit("No entries found. Check the channel handle.")

    channel_id = next((r["channel_id"] for r in all_rows if r.get("channel_id")), "")
    in_window = sorted(
        (r for r in all_rows
         if since <= r["upload_date"] <= until and r["tab"] in tabs),
        key=lambda r: (r["upload_date"], r["title"]),
    )

    # --- verification -------------------------------------------------
    present = {r["tab"] for r in all_rows}
    boundary_ok = {
        t: any(r["tab"] == t and r["upload_date"] < since for r in all_rows)
        for t in TABS if t in present
    }
    log("Cross-checking against the uploads playlist ...")
    upload_ids, spans = uploads_crosscheck(channel_id, since)
    known = {r["id"] for r in all_rows}
    unaccounted = [i for i in upload_ids if i not in known]

    # An unaccounted ID only matters if it actually falls inside the window.
    # Date them individually rather than assuming.
    gap_dates = date_ids(unaccounted[:40]) if unaccounted else {}
    genuine_gaps = [
        {"id": i, "upload_date": d}
        for i, d in gap_dates.items() if since <= d <= until
    ]

    verification = {
        "verification_tabs": sorted(present),
        "selection_tabs": tabs,
        "boundary_crossed_per_tab": boundary_ok,
        "all_boundaries_crossed": all(boundary_ok.values()),
        "uploads_playlist_ids_seen": len(upload_ids),
        "uploads_playlist_spans_window": spans,
        "unaccounted_ids_total": len(unaccounted),
        "unaccounted_dated": len(gap_dates),
        "genuine_gaps_in_window": genuine_gaps,
        "passed": (all(boundary_ok.values()) and spans and not genuine_gaps),
    }

    manifest = {
        "channel": base,
        "channel_id": channel_id,
        "window": {"since": since, "until": until, "label": label},
        "tabs": tabs,
        "counts": {
            "fetched_total": len(all_rows),
            "in_window": len(in_window),
            "by_tab": {t: sum(1 for r in in_window if r["tab"] == t) for t in tabs},
        },
        "verification": verification,
        "topic_filter": None,       # set by the agent if a topic filter is applied
        "excluded_by_topic": [],    # agent records what it dropped, and why
        "videos": in_window,
    }

    Path(args.out).write_text(json.dumps(manifest, indent=2, ensure_ascii=False),
                              encoding="utf-8")

    log("")
    log(f"In window        : {len(in_window)}  {manifest['counts']['by_tab']}")
    log(f"Boundary crossed : {verification['all_boundaries_crossed']}  {boundary_ok}")
    log(f"Playlist spans   : {spans} ({len(upload_ids)} ids)")
    log(f"Genuine gaps     : {len(genuine_gaps)}  {genuine_gaps if genuine_gaps else ''}")
    log(f"VERIFICATION     : {'PASS' if verification['passed'] else 'REVIEW REQUIRED'}")
    log(f"Manifest         : {args.out}")
    if not verification["passed"]:
        log("!! Do not present this as complete. Report the gap to the user.")


if __name__ == "__main__":
    main()

```
