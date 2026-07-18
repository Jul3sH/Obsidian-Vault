# Claude Cowork

> *Collaborative multi-agent features in Claude Code — Claude working alongside you or other agents.*

tags: [technical, claude, anthropic]

Claude Cowork refers to the collaborative and multi-agent capabilities within Claude Code. It allows Claude to spawn sub-agents, work in parallel on complex tasks, and operate within shared workflows.

---

## Key Concepts

### Sub-agents
Claude Code can spawn separate agent instances to handle independent parts of a task in parallel — for example, compiling multiple wiki sections simultaneously. Each sub-agent operates in isolation and reports back.

### Skills
Pre-built instruction sets that can be invoked with `/skill-name`. Skills encode best practices for specific tasks (e.g. compiling a wiki, reviewing a PR, setting up a config). They can be created and customised.

### MCP Servers (Model Context Protocol)
A protocol that allows Claude to connect to external tools and data sources — e.g. Jira, Confluence, Google Drive. MCP servers extend what Claude can read and act on beyond the local file system.

### Hooks
Automated behaviours triggered by events (e.g. "after every compile, update the log"). Configured in `.claude/settings.json` rather than relying on Claude's memory. Hooks run **outside Claude's control** — they fire at the defined event regardless of what Claude decides, which makes them reliable for enforcement rather than just guidance.

### Plugins
A structured, shareable way to bundle **skills + hooks together** as a versioned unit. Key distinction:
- A **skill** tells Claude what to do when invoked
- A **hook** runs automatically at a defined event regardless of Claude's decision
- A **plugin** packages both into a portable unit that can be distributed across projects

Turning a skill into a plugin makes its associated hooks more likely to fire because the plugin is loaded as a unit. Hooks can also be defined standalone in a `.claude/` directory without a plugin wrapper.

---

## This Vault's Use of Cowork
- Sub-agents were used to compile the lessons learnt wiki in parallel (working-with-yourself, working-with-others, the-human-mind compiled simultaneously)
- The CLAUDE.md file in this vault effectively acts as the standing instruction set for all sessions

---

## See Also
- [[claude-code]] — the underlying CLI tool
- [[claude-md-and-memory]] — persistent instructions across sessions

---

## Key Takeaways
- Cowork features let Claude handle large, complex tasks by splitting them across parallel agents
- Skills and hooks enable automated, repeatable workflows without manual prompting
- MCP servers extend Claude's reach to external tools and platforms
