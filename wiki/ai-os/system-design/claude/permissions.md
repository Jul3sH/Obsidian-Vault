---
type: reference
created: 2026-06-30
updated: 2026-06-30
---

# Claude Code Permissions

> How permission prompts are reduced in this environment, the policy for what is safe to allowlist, and the current allowlist. The embedded snapshot below is a verbatim mirror of the hidden project config `<vault>/.claude/settings.json` (`permissions.allow`). No secrets present, nothing redacted.

## Purpose

Claude Code prompts before running a tool call unless the call matches an
allowlist. Recurring read-only calls (Jira reads, file reads, board lookups)
generate friction when they prompt every time. This doc records how that
friction is reduced safely, so the allowlist stays auditable and does not drift
into granting more than intended.

## The permission model

Three decision buckets in `settings.json` under `permissions`:

| Bucket | Effect |
|--------|--------|
| `allow` | Matching calls run without prompting |
| `ask` | Matching calls always prompt (even if also in `allow`) |
| `deny` | Matching calls are blocked outright |

Pattern forms: `Bash(npm info *)` (prefix - note the space before `*`),
`Bash(git log)` (exact), `mcp__server__tool_name` (MCP tools are already
specific, no wildcard). We only ever touch `allow` via the
`/fewer-permission-prompts` skill - never `ask` or `deny`.

**Auto-allowed already (do NOT add these):** a large set of read-only Bash
commands never prompt and need no entry - `cat`, `ls`, `cd`, `grep`, `find`,
`tail`, `head`, `wc`, `sed` (read expressions), `diff`, `wc`, all git/gh/docker
read-only subcommands, and more. Adding them is clutter. The
`/fewer-permission-prompts` skill knows this list and skips them.

## Where permissions live (precedence high → low)

| Tier | File | Scope |
|------|------|-------|
| Project-local | `<vault>/.claude/settings.local.json` | This machine only, not shared. Where in-the-moment "always allow" picks accumulate. |
| Project | `<vault>/.claude/settings.json` | Shared project allowlist. **`/fewer-permission-prompts` writes here.** This is the mirrored, documented surface. |
| User / global | `~/.claude/settings.json` | Applies across all projects. Holds the broad vault Edit/Write/Read grants and common read-only Bash. |

A higher tier wins on conflict. The deliberate, reviewed allowlist lives in the
**project** file (this doc's snapshot); the local file is the noisy scratch tier.

## Policy: read-only first

The rule for what may be blanket-allowed:

- **Safe to allowlist:** read-only operations - MCP tools whose names contain
  `get`/`list`/`search`/`view`/`read`, read-only Bash, and vault `Edit`/`Write`/`Read`
  (the wiki is the librarian's domain).
- **Keep prompting (do NOT blanket-allow):** anything **outward-facing or
  mutating** - Jira **writes** (`createJiraIssue`, `transitionJiraIssue`,
  `editJiraIssue`, `jira_update_issue`, `jira_delete_issue`), sending email,
  external posts. These cross a boundary or change someone else's system; the
  prompt is the deliberate checkpoint. They can be allowlisted individually via
  `/update-config` if a recurring workflow (e.g. `/jira-sync`) justifies it, but
  that is a conscious decision, not a default.
- **Never allowlist:** arbitrary code execution - interpreters (`python`,
  `node`, `bun`, `ruby`), shells (`bash`, `sh`, `eval`, `ssh`), package runners
  (`npx`, `uvx`), task-runner wildcards (`npm run *`, `make *`), `gh api *`,
  `sudo`. A wildcard on any of these is equivalent to "run anything."

## Workflow: `/fewer-permission-prompts`

Purpose-built skill. It:
1. Scans the 50 most-recent session transcripts across `~/.claude/projects/`.
2. Tallies Bash leading-command and MCP tool-call frequencies.
3. Filters to read-only, drops already-auto-allowed and anything mutating or
   code-executing, drops entries seen fewer than ~3 times.
4. Presents a ranked table, then merges into the **project** `.claude/settings.json`
   `permissions.allow`, de-duplicating against what is already there (project +
   global).

**Cadence:** re-run when permission prompts start to feel frequent again (e.g.
after adopting a new MCP server or a new recurring ceremony). It is additive and
idempotent - safe to run repeatedly.

## Current project allowlist

Verbatim snapshot of `<vault>/.claude/settings.json` as of 2026-06-30. The first
block of entries are historical one-offs; the read-only MCP/Bash block at the end
was added by `/fewer-permission-prompts` on 2026-06-30 (10 entries: legacy
`mcp__atlassian__` reads, active `mcp__claude_ai_Atlassian__` reads, and
`npm info`).

```json
{
  "permissions": {
    "allow": [
      "Bash(rm -rf \"/Users/julianhart/.claude/skills/epic-planner/\" && echo \"Deleted ~/.claude/skills/epic-planner/\")",
      "Edit(~/.claude/skills/project-planner/**)",
      "Bash(python3 -c ' *)",
      "Edit(~/.claude/skills/define-task/**)",
      "Bash(mkdir -p \"/Users/julianhart/Obsidian Vault/wiki/ai-os/skills/define-task\" && cp ~/.claude/skills/define-task/SKILL.md \"...\")",
      "Bash(node -e ' *)",
      "Bash(node modify13.js)",
      "Bash(node rebuild5.js \"...goals-roadmap.excalidraw.md\")",
      "Bash(node -e \"console.log(require('/tmp/excalidraw-edit/node_modules/lz-string'))\")",
      "Bash(node build-career-goals-diagram.js)",
      "Bash(grep -n \"...\" \"...ed2c29d2....jsonl\")",
      "mcp__atlassian__jira_search_issues",
      "mcp__atlassian__jira_get_transitions",
      "mcp__atlassian__jira_get_issue",
      "mcp__claude_ai_Atlassian__getTransitionsForJiraIssue",
      "mcp__atlassian__jira_get_agile_boards",
      "mcp__atlassian__jira_get_backlog_issues",
      "Bash(npm info *)",
      "mcp__claude_ai_Atlassian__getAccessibleAtlassianResources",
      "mcp__claude_ai_Atlassian__getJiraIssue",
      "mcp__atlassian__jira_get_board_issues"
    ],
    "additionalDirectories": [
      "/Users/julianhart/.claude/skills/epic-planner",
      "/Users/julianhart/.claude/skills/define-task"
    ]
  }
}
```

> Note: several read-only entries (`searchJiraIssuesUsingJql`, the Excalidraw
> reads, `getIssueLinkTypes`) are already granted in the **global**
> `~/.claude/settings.json`, so they are not duplicated here.

## Known gap

The hidden settings files are not yet fully mirrored per the
[[hidden-file-sync|Hidden File Sync]] rule. This doc mirrors the **project**
`settings.json` allowlist; the **global** `~/.claude/settings.json` and the two
`settings.local.json` files remain unmirrored. Tracked in
[[brain-dump|raw/brain-dump.md]] (Wiki / AI OS).

## Links

- [[hidden-file-sync|Hidden File Sync Checklist]]
- [[_index|Claude System Design]]
- `/fewer-permission-prompts` skill - the mechanism
- `/update-config` skill - for individually allowlisting a justified write tool
