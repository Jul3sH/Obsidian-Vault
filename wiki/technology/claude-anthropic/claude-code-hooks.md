---
type: reference
created: 2026-08-19
tags: [technical, claude, anthropic, hooks]
---

# Claude Code Hooks

> *Shell commands that fire automatically on session and tool-use events, outside Claude's control.*

This is what a hook is and how to wire one, for anyone using Claude Code regardless of setup. It exists because [[mm-steering]] names "hook" as the mechanism for anything that must happen every time without judgement, but defers the implementation detail to Anthropic's steering guide rather than carrying it in the model. For the hooks actually running in Julian's environment, see [[hooks|Claude Code Hooks (this environment)]] in system-design/claude.

---

## Key Concepts

### What a hook is
An external command Claude Code runs when a defined event fires, regardless of what the model would have chosen to do. [[claude-cowork|Cowork]] frames the distinction: a skill is something Claude decides to invoke; a hook happens whether Claude decides to or not.

### Events
Claude Code exposes roughly 30 hook events covering session lifecycle, tool use, permissions, subagents, tasks, config/filesystem changes, and compaction. The ones actually in use anywhere in this vault's setup:

| Event | Fires |
|---|---|
| `SessionStart` | A session begins or resumes (matcher can narrow to `startup`, `resume`, `clear`, `compact`) |
| `SessionEnd` | A session terminates |
| `UserPromptSubmit` | A prompt is submitted, before Claude processes it |
| `PreToolUse` | Before a tool call executes |
| `Stop` | Claude finishes responding to a turn |

The rest — `PostToolUse`/`PostToolUseFailure`, `Notification`, `SubagentStart`/`SubagentStop`, `PreCompact`/`PostCompact`, `TaskCreated`/`TaskCompleted`, `WorktreeCreate`/`WorktreeRemove`, `ConfigChange`, `FileChanged`, `Elicitation`, and more — exist for narrower cases. Full canonical list: [Anthropic's hooks reference](https://code.claude.com/docs/en/hooks).

### Wiring
Declared under a `hooks` key, keyed by event name:

```json
{
  "hooks": {
    "EventName": [
      {
        "matcher": "ToolName|OtherTool",
        "hooks": [
          { "type": "command", "command": "/path/to/script.sh", "timeout": 600 }
        ]
      }
    ]
  }
}
```

- `matcher` (optional) filters by tool name (`PreToolUse`/`PostToolUse`) or start reason (`SessionStart`). Omit it to fire on every instance of the event.
- `if` further filters using permission-rule syntax, e.g. `"Bash(rm *)"` — fire only when the call would also match that pattern.
- `type` is usually `"command"` (a shell command) but can also be `"http"`, `"mcp_tool"`, `"prompt"`, or `"agent"`.
- `async: true` runs the hook without blocking the turn; `asyncRewake: true` wakes Claude when it exits with code 2.

Two places to declare hooks:
- **`settings.json`** — global (`~/.claude/settings.json`) or project (`.claude/settings.json` / `settings.local.json`) — scoped to a user or a project.
- **A plugin's `hooks/hooks.json`** — bundles the hook with the plugin so it travels with the install; `${CLAUDE_PLUGIN_ROOT}` resolves to the plugin's own folder inside the command string.

### Input and output
A hook receives the event as JSON on stdin: common fields (`session_id`, `prompt_id`, `transcript_path`, `cwd`, `permission_mode`, `hook_event_name`) plus event-specific ones (`PreToolUse` etc. add `tool_name`/`tool_input`/`tool_use_id`).

It replies by printing JSON to stdout with exit code 0:
- `continue: false` — stop processing, with `stopReason` shown to the user
- `systemMessage` — a note shown to Claude (not the user)
- `hookSpecificOutput.additionalContext` — text injected into the conversation as if the harness said it
- `hookSpecificOutput.permissionDecision` (`allow`/`deny`/`escalate`, tool events only) plus `permissionDecisionReason`
- `hookSpecificOutput.updatedInput` — a modified version of the tool call to run instead

For `PreToolUse` specifically, the exit code itself carries meaning independent of the JSON: `0` honours the JSON, `1` or anything else is a non-blocking error (the call proceeds through normal permissions), and `2` **blocks the call outright** — stderr is shown as the reason, and no JSON is needed to make that stick.

## Guidelines
- Match the event to the moment: "must happen before this tool runs" is `PreToolUse`; "must happen once per day/session" is `SessionStart` plus a stamp file, since the bare event fires on every session, not once a day.
- Prefer `matcher`/`if` over an unfiltered hook with internal branching — it keeps the hook from paying its own startup cost on events it will just no-op on.
- A hook that must never break the session should fail open: catch its own errors and exit 0 (or exit 1 on `PreToolUse`) rather than let a bug in the hook block Claude Code from starting or acting.
- A plugin's hooks are only live if the plugin is both installed *and* enabled (`enabledPlugins` in `settings.json`); some hooks are further gated by their own opt-in flag file, so "installed" is not the same as "firing."
- `exit 2` is the only reliable block on `PreToolUse` — a `deny` in the JSON with a non-2 exit code is advisory, not enforced.

## Limitations
- A hook only sees the event payload, not the model's reasoning — any conditional logic has to be re-derived from scratch inside the hook script.
- `additionalContext` is advisory once it lands in the conversation: the model can still choose to disregard it, same as any other instruction ([[mm-steering]]).
- Harness-specific and perishable: this is Claude Code's current hook surface, not a general agent concept, and the event list grows across versions.

## Detail
Source: [Claude Code Hooks Reference](https://code.claude.com/docs/en/hooks) (Anthropic), and the broader [Steering Claude Code](https://claude.com/blog/steering-claude-code-skills-hooks-rules-subagents-and-more) guide. Companions: [[mm-steering]] (why hooks are the right mechanism for must-happen behaviour), [[hooks|this environment's hooks]] (which hooks actually run for Julian and why), [[claude-cowork]] (hooks alongside skills, plugins, and MCP).

## Key Takeaways
- A hook is an event-triggered command, not a request to Claude — it fires whether or not the model would have chosen to.
- Two declaration points: `settings.json` (user/project-scoped) or a plugin's `hooks/hooks.json` (travels with the plugin).
- A hook reads the event payload on stdin and can act on the session via `additionalContext` / `permissionDecision` / `updatedInput` on stdout — but only if it says so.
- On `PreToolUse`, exit code `2` is the only enforcement lever that doesn't depend on JSON being parsed correctly.
