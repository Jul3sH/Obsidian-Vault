---
created: 2026-06-09
type: reference
---

# Google Operations — Setup, Commands & Best Practices

## Terminal Process Management

### Killing Frozen or Unresponsive Processes

- `Ctrl + C` — Standard process interrupt; halts autonomous file-scanning loops
- `Ctrl + \` — Hard terminal kill command; terminates unresponsive binary execution layers

## API & Session Initialization

### Setup Commands

```bash
# 1. Export your secure Google AI Studio Developer Key into active session memory
export GEMINI_API_KEY="AIzaSy..."

# 2. Change directory into your target Obsidian folder
cd "/Users/julianhart/Obsidian Vault"

# 3. Boot up the open-source terminal agent framework
gemini
```

## In-App Agent Slash Commands

Internal TUI (Terminal User Interface) commands typed inside the running agent window:

- `/exit` — Gracefully terminates the running agent session and returns to Mac shell
- `/stats model` — Reviews model invocation counters for the active shell lifecycle
- `/stats session` — Loads overall account metrics, input/output token structures, and token counts
- `/usage` — Pulls live telemetry mapping remaining free-tier daily request limits (250/day cap)

## Security & Permissions

### Trust Boundaries

Upon launching the terminal tool, choose **Option 1 (Trust specific folder)**. Do not trust the parent root directory (`/Users/julianhart`), as this grants the autonomous agent sweeping write access over your broader machine profile.

### Avoiding Credit Interception

Refrain from typing raw terminal commands directly into AI-integrated editor windows (like Claude Code windows). Background agents read text commands as natural instructions, spinning up internal bash sub-shells that aggressively consume external platform credits. Keep your agentic operations distinctly separated in a native Mac Terminal pane.
