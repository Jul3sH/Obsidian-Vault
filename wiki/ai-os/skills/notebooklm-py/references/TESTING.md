<!-- Mirror of ~/.claude/skills/notebooklm-py/references/TESTING.md — do not edit here; edit the source file -->

# TESTING.md — notebooklm-py

## Pre-Flight Checklist

Run these checks before any debugging session:

| # | Check | Command | Catches |
|---|-------|---------|---------|
| 1 | Package installed | `notebooklm --version` | Missing package |
| 2 | Auth working | `notebooklm auth check --test --json` | Expired OAuth cookie |
| 3 | Playwright installed | `python -c "from playwright.sync_api import sync_playwright; print('ok')"` | Missing browser automation |
| 4 | Wiki topic folder exists | `ls ~/Obsidian\ Vault/wiki/performance/working-with-others/` | Wrong WIKI_ROOT path |
| 5 | VPN routing | Google APIs are direct — do NOT route through VPN | Auth failure from wrong exit IP |
| 6 | List notebooks | `notebooklm notebook list --json` | End-to-end auth check |

## VPN Rule

Google APIs (including NotebookLM) must be routed direct, not through VPN. VPN exit IPs are blocked by Google in some cases. ExpressVPN bypass: all traffic through VPN except IPs in `160.79.104.0/21`. Google is outside this range and routes direct automatically.

## Test Log

| Date | What | Why | Revealed |
|------|------|-----|---------|
| — | Not yet tested | Skill newly created | — |

## Known Gotchas

- `notebooklm login` must be run in a terminal with a display browser available — does not work headless
- Source processing for a large wiki topic folder (30+ articles) can take up to 10 minutes — `source wait` will block until ready
- Rate limiting on generation: if multiple notebooks are being generated simultaneously, tasks may queue silently
- `notebooklm source add file` is preferred over `add text` for large content (avoids shell argument length limits)
- The `--json` flag is required for scripted parsing; without it, output is human-readable and not parseable

## First Run Steps

1. Install: `pip install "notebooklm-py[browser]" && playwright install chromium`
2. Auth: `notebooklm login` (opens browser, complete Google OAuth)
3. Verify: `notebooklm auth check --test --json`
4. Smoke test (list notebooks): `notebooklm notebook list --json`
5. Test with single article before running full topic batch
