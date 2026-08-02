<!-- Mirror of ~/.claude/skills/youtube-notebook/scripts/build_notebook.py - do not edit here; edit the source file -->
<!-- Python scripts are stored as .md with embedded code blocks in the wiki per skill-conventions.md -->

# build_notebook.py

tags: [technical, skills, notebooklm, scripts]

> *Turns an approved manifest into a notebook: one source per video, one native briefing per source, four-way reconciliation.*

**Source:** `~/.claude/skills/youtube-notebook/scripts/build_notebook.py`

---

```python
#!/usr/bin/env python3
"""
build_notebook.py - turn an approved manifest into a NotebookLM notebook with
one source per video and (optionally) one native briefing doc per source.

Guarantees the two correlation rules:
  * source title      = "<MM-DD> <video title>"
  * briefing artifact title = the SAME string as its source title
  * downloaded filename     = the same string, filesystem-sanitised
  * in-file H1              = the same string, with the source URL beneath it

Briefing content is 100% NotebookLM's own `--format briefing-doc` output.
This script only sets titles and prepends a provenance block; it never
writes or paraphrases briefing prose.

Every phase reconciles against the manifest and the run aborts loudly rather
than reporting partial success as success.

Usage:
  python build_notebook.py --manifest manifest.json --notebook-title "NBJ June 2026"
  python build_notebook.py --manifest manifest.json --notebook-title "X" --no-briefings
  python build_notebook.py --manifest manifest.json --notebook-id <uuid> --resume
"""
from __future__ import annotations

import argparse
import json
import re
import sys
import time
from datetime import datetime
from pathlib import Path

sys.path.insert(0, str(Path(__file__).resolve().parent))
from nlm import NlmError, nlm, preflight  # noqa: E402

STATE_NAME = "run-state.json"


def log(msg: str = "") -> None:
    print(msg, file=sys.stderr, flush=True)


def safe_filename(title: str) -> str:
    """Filesystem-safe form of the title, kept as close to it as possible.

    Separator-like illegal characters become " - "; the rest are dropped so we
    don't leave a dangling separator (e.g. "Switch?" must not become "Switch -").
    """
    t = re.sub(r"[/\\|:]", " - ", title)
    t = re.sub(r"[*?\"<>]", "", t)
    t = re.sub(r"\s+", " ", t).strip()
    return t.strip(" .-") or "untitled"


def source_title(video: dict, date_fmt: str) -> str:
    d = datetime.strptime(video["upload_date"], "%Y%m%d")
    return f"{d.strftime(date_fmt)} {video['title']}".strip()


class State:
    """Small on-disk record so a failed run can resume without duplicating."""

    def __init__(self, path: Path):
        self.path = path
        self.data = json.loads(path.read_text()) if path.exists() else {}

    def get(self, vid: str) -> dict:
        return self.data.setdefault(vid, {})

    def save(self) -> None:
        self.path.write_text(json.dumps(self.data, indent=2, ensure_ascii=False),
                             encoding="utf-8")


def ingest(nb: str, videos: list[dict], date_fmt: str, state: State) -> None:
    log(f"\n=== Ingesting {len(videos)} sources ===")
    for i, v in enumerate(videos, 1):
        st = state.get(v["id"])
        title = source_title(v, date_fmt)
        if st.get("source_id"):
            log(f"[{i}/{len(videos)}] skip (done): {title}")
            continue
        url = f"https://www.youtube.com/watch?v={v['id']}"
        try:
            res = nlm("source", "add", "-n", nb, "--type", "youtube", url,
                      json_out=True, timeout=300)
            sid = (res.get("source") or {}).get("id")
            if not sid:
                raise NlmError(f"no source id in response: {res}")
            nlm("source", "rename", "-n", nb, sid, title, timeout=180)
            st.update({"source_id": sid, "title": title})
            log(f"[{i}/{len(videos)}] added: {title}")
        except (NlmError, Exception) as exc:  # noqa: BLE001
            st["source_error"] = str(exc)[:300]
            log(f"[{i}/{len(videos)}] FAILED: {title} :: {exc}")
        state.save()
        time.sleep(1)


def wait_sources(nb: str, state: State) -> None:
    log("\n=== Waiting for source processing ===")
    for vid, st in state.data.items():
        sid = st.get("source_id")
        if not sid or st.get("ready"):
            continue
        try:
            nlm("source", "wait", "-n", nb, sid, check=False, timeout=900)
            st["ready"] = True
        except Exception as exc:  # noqa: BLE001
            st["ready_error"] = str(exc)[:200]
    live = {s["id"]: s.get("status") for s in nlm("source", "list", "-n", nb,
                                                  json_out=True)["sources"]}
    for st in state.data.values():
        if st.get("source_id"):
            st["status"] = live.get(st["source_id"], "missing")
    state.save()
    bad = [s["title"] for s in state.data.values() if s.get("status") != "ready"]
    log(f"ready: {sum(1 for s in state.data.values() if s.get('status') == 'ready')}"
        f" / {len(state.data)}")
    for b in bad:
        log(f"  NOT READY: {b}")


def brief(nb: str, state: State) -> None:
    log("\n=== Generating native briefing docs (one per source) ===")
    items = [s for s in state.data.values() if s.get("status") == "ready"]
    for i, st in enumerate(items, 1):
        if st.get("artifact_id"):
            log(f"[{i}/{len(items)}] skip (done): {st['title']}")
            continue
        try:
            res = nlm("generate", "report", "--format", "briefing-doc",
                      "-n", nb, "-s", st["source_id"], "--no-wait", "--retry", "3",
                      json_out=True, timeout=300)
            tid = res.get("task_id")
            if not tid:
                raise NlmError(f"no task_id: {res}")
            st["artifact_id"] = tid
            log(f"[{i}/{len(items)}] queued: {st['title']}")
        except Exception as exc:  # noqa: BLE001
            st["brief_error"] = str(exc)[:300]
            log(f"[{i}/{len(items)}] FAILED: {st['title']} :: {exc}")
        state.save()
        time.sleep(3)

    log("\n=== Waiting for briefings, then retitling ===")
    for i, st in enumerate(items, 1):
        tid = st.get("artifact_id")
        if not tid or st.get("artifact_titled"):
            continue
        nlm("artifact", "wait", "-n", nb, tid, "--timeout", "900",
            check=False, timeout=960)
        got = nlm("artifact", "get", "-n", nb, tid, json_out=True)
        status = got.get("status") or (got.get("artifact") or {}).get("status")
        if status != "completed":
            st["artifact_status"] = status
            log(f"[{i}/{len(items)}] NOT COMPLETE ({status}): {st['title']}")
            continue
        st["notebooklm_title"] = got.get("title", "")
        nlm("artifact", "rename", "-n", nb, tid, st["title"], timeout=180)
        st["artifact_titled"] = True
        st["artifact_status"] = "completed"
        log(f"[{i}/{len(items)}] titled: {st['title']}")
        state.save()


def download(nb: str, state: State, outdir: Path, manifest: dict) -> None:
    log(f"\n=== Downloading to {outdir} ===")
    outdir.mkdir(parents=True, exist_ok=True)
    by_vid = {v["id"]: v for v in manifest["videos"]}
    for vid, st in state.data.items():
        tid = st.get("artifact_id")
        if not tid or st.get("artifact_status") != "completed":
            continue
        fname = safe_filename(st["title"]) + ".md"
        target = outdir / fname
        try:
            nlm("download", "report", "-n", nb, "-a", tid, str(target),
                "--force", timeout=300)
            add_provenance(target, st, by_vid.get(vid, {}), manifest)
            st["file"] = fname
            log(f"  {fname}")
        except Exception as exc:  # noqa: BLE001
            st["download_error"] = str(exc)[:300]
            log(f"  FAILED {fname} :: {exc}")
    state.save()


def add_provenance(path: Path, st: dict, video: dict, manifest: dict) -> None:
    """Prepend the correlating H1 + source link; demote NotebookLM's own H1 to H2.

    NotebookLM's prose is not modified. Its auto-title is preserved twice so
    nothing is lost: once as a metadata field, once as the H2.
    """
    body = path.read_text(encoding="utf-8")
    title = st["title"]
    if body.startswith(f"# {title}"):
        return
    m = re.match(r"#\s+(.+?)\n", body)
    nlm_title = m.group(1).strip() if m else st.get("notebooklm_title", "")
    if m:
        body = body[: m.start()] + f"## {nlm_title}\n" + body[m.end():]
    pretty = ""
    if video.get("upload_date"):
        pretty = datetime.strptime(video["upload_date"], "%Y%m%d").strftime("%-d %B %Y")
    hdr = [f"# {title}", ""]
    if video.get("id"):
        hdr.append(f"**Source video:** https://www.youtube.com/watch?v={video['id']}")
    if pretty:
        hdr.append(f"**Published:** {pretty}")
    hdr.append(f"**Channel:** {manifest.get('channel', '')}")
    hdr.append("**Briefing:** NotebookLM native briefing doc, generated from this source only")
    if nlm_title:
        hdr.append(f"**NotebookLM title:** {nlm_title}")
    hdr += ["", "---", "", ""]
    path.write_text("\n".join(hdr) + body, encoding="utf-8")


def reconcile(nb: str, state: State, manifest: dict, outdir: Path,
              briefings: bool, date_fmt: str, reused: bool = False) -> dict:
    log("\n=== Reconciliation ===")
    expected = sorted(source_title(v, date_fmt) for v in manifest["videos"])
    srcs = sorted(s["title"] for s in nlm("source", "list", "-n", nb,
                                          json_out=True)["sources"])
    arts_raw = nlm("artifact", "list", "-n", nb, json_out=True)["artifacts"]
    arts = sorted(a["title"] for a in arts_raw if a.get("type_id") == "report")
    files = sorted(p.stem for p in outdir.glob("*.md")) if outdir.exists() else []
    exp_files = sorted(safe_filename(t) for t in expected)

    def complete(actual: list[str], wanted: list[str]) -> bool:
        """Did this run land everything it owed?

        A notebook built from scratch should contain exactly the manifest. A
        reused one (--notebook-id) legitimately holds more: earlier months,
        unrelated sources, briefings from prior runs. There the question is
        "is every expected item present", not "is expected all there is" -
        equality would fail every incremental run even when nothing is missing.
        """
        return set(wanted) <= set(actual) if reused else actual == wanted

    # Same reasoning for artifact health: only the artifacts this run is
    # responsible for can be judged by this run. A stale or failed audio
    # overview someone generated by hand months ago is not this run's problem.
    completed_scope = ([a for a in arts_raw if a.get("title") in set(expected)]
                       if reused else arts_raw)

    hdr_ok = 0
    for t in expected:
        fp = outdir / (safe_filename(t) + ".md")
        if fp.exists() and fp.read_text(encoding="utf-8").startswith(f"# {t}"):
            hdr_ok += 1

    rep = {
        "expected_videos": len(expected),
        "notebook_reused": reused,
        "sources_in_notebook": len(srcs),
        "artifacts_in_notebook": len(arts),
        "files_in_output_dir": len(files),
        "sources_match": complete(srcs, expected),
        "sources_missing": [t for t in expected if t not in srcs],
        "briefings_expected": briefings,
        "artifacts_match": complete(arts, expected) if briefings else None,
        "artifacts_missing": [t for t in expected if t not in arts] if briefings else [],
        "all_artifacts_completed": all(a.get("status") == "completed"
                                       for a in completed_scope)
        if briefings else None,
        "files_match": complete(files, exp_files) if briefings else None,
        "files_missing": [f for f in exp_files if f not in files] if briefings else [],
        "headers_matching_title": f"{hdr_ok}/{len(expected)}" if briefings else None,
        "enumeration_verification": manifest.get("verification", {}).get("passed"),
        "topic_filter": manifest.get("topic_filter"),
        "excluded_by_topic": len(manifest.get("excluded_by_topic", [])),
    }
    checks = [rep["sources_match"]]
    if briefings:
        checks += [rep["artifacts_match"], rep["files_match"],
                   rep["all_artifacts_completed"], hdr_ok == len(expected)]
    rep["overall"] = "PASS" if all(bool(c) for c in checks) else "FAIL"

    for k, v in rep.items():
        log(f"  {k}: {v}")
    return rep


def main() -> None:
    p = argparse.ArgumentParser(description="Build a NotebookLM notebook from a manifest")
    p.add_argument("--manifest", required=True)
    p.add_argument("--notebook-title")
    p.add_argument("--notebook-id", help="use an existing notebook instead of creating one")
    p.add_argument("--output-dir", default="~/Downloads")
    p.add_argument("--date-format", default="%m-%d",
                   help="source-title date prefix (use %%Y-%%m-%%d for multi-year ranges)")
    p.add_argument("--no-briefings", action="store_true",
                   help="ingest sources only, skip per-source briefing docs")
    p.add_argument("--resume", action="store_true")
    args = p.parse_args()

    manifest = json.loads(Path(args.manifest).read_text(encoding="utf-8"))
    videos = manifest["videos"]
    if not videos:
        raise SystemExit("Manifest contains no videos.")
    briefings = not args.no_briefings

    info = preflight()
    log(f"CLI: {info['binary']}  auth: {info['auth']}")

    if not manifest.get("verification", {}).get("passed"):
        log("!! Enumeration verification did NOT pass. Continuing, but the result "
            "must not be described as complete.")

    if args.notebook_id:
        nb = args.notebook_id
    else:
        if not args.notebook_title:
            raise SystemExit("--notebook-title is required unless --notebook-id is given")
        nb = nlm("create", args.notebook_title, json_out=True)["notebook"]["id"]
        log(f"Created notebook: {args.notebook_title} ({nb})")

    outdir = Path(args.output_dir).expanduser()
    if briefings and args.notebook_title:
        outdir = outdir / f"{args.notebook_title} Briefings"

    state = State(Path(args.manifest).with_name(STATE_NAME))
    if not args.resume:
        state.data = {}

    ingest(nb, videos, args.date_format, state)
    wait_sources(nb, state)
    if briefings:
        brief(nb, state)
        download(nb, state, outdir, manifest)

    rep = reconcile(nb, state, manifest, outdir, briefings, args.date_format,
                    reused=bool(args.notebook_id))
    rep.update({"notebook_id": nb, "notebook_title": args.notebook_title,
                "output_dir": str(outdir)})
    Path(args.manifest).with_name("run-report.json").write_text(
        json.dumps(rep, indent=2, ensure_ascii=False), encoding="utf-8")

    log(f"\nOVERALL: {rep['overall']}")
    log(f"Notebook: {nb}")
    if briefings:
        log(f"Files: {outdir}")
    sys.exit(0 if rep["overall"] == "PASS" else 1)


if __name__ == "__main__":
    main()

```
