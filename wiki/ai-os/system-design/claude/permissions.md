---
type: reference
created: 2026-06-30
updated: 2026-08-20
---

# Claude Code Permissions

> How permission prompts are reduced in this environment, the policy for what is safe to allowlist, the current allowlist, and the project-level hooks. The embedded snapshot below is a verbatim mirror of the full hidden project config `<vault>/.claude/settings.json`. No secrets present, nothing redacted.

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

## Current project settings snapshot

Verbatim snapshot of `<vault>/.claude/settings.json` as of 2026-08-20. Two parts:
the `permissions.allow` list (maintained via `/fewer-permission-prompts`) and a
`hooks` block added 2026-08-20.

```json
{
  "permissions": {
    "allow": [
      "Bash(python3 -c ' *)",
      "Bash(node -e ' *)",
      "Bash(npm info *)",
      "Edit(~/.claude/skills/project-planner/**)",
      "Edit(~/.claude/skills/define-task/**)",
      "mcp__claude_ai_Atlassian__getAccessibleAtlassianResources",
      "mcp__claude_ai_Atlassian__getJiraIssue",
      "mcp__claude_ai_Atlassian__getTransitionsForJiraIssue"
    ],
    "additionalDirectories": [
      "/Users/julianhart/.claude/skills/define-task"
    ]
  },
  "hooks": {
    "UserPromptSubmit": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "echo '{\"hookSpecificOutput\":{\"hookEventName\":\"UserPromptSubmit\",\"additionalContext\":\"Time-tracking check: if this prompt hands back completed attended work on a deliverable (a finished review, a sign-off, corrections returned), ask Julian how many focused minutes it took and record it in that deliverable file under ## Time Log. If the prompt is not a work handback, ignore this note.\"}}'"
          }
        ]
      }
    ]
  }
}
```

## Hooks in the project file

**Time-log reminder (`UserPromptSubmit`, added 2026-08-20).** Fires on every
prompt Julian submits in this vault and injects a short instruction into
Claude's context: if the prompt hands back completed attended work on a
deliverable (a finished review, a sign-off, corrections returned), Claude must
ask Julian how many focused minutes it took and record the answer in that
deliverable's `## Time Log` table. Supports the execution-time baseline agreed
for [[ai-engineering-pattern-articles]]: machine effort is recorded in tokens,
Julian's effort in minutes, and only Julian's minutes roll up into `Actual hrs`
in the [[estimation-baseline|Estimation Baseline]]. A hook is used rather than
an instruction in memory because only a hook fires deterministically on every
prompt.

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
