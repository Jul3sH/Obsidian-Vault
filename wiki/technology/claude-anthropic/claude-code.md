# Claude Code

> *Anthropic's CLI tool for using Claude as a coding and knowledge agent directly in your terminal.*

tags: [technical, claude, anthropic]

Claude Code is a command-line tool that runs Claude inside a folder on your machine. It has access to read, write, and edit files, run terminal commands, and search the web — making it useful far beyond coding.

---

## Key Concepts

- **Works in your file system** — Claude can read, create, and edit files directly in whatever folder you open it in
- **Session-based** — no persistent memory between sessions unless you use [[claude-md-and-memory|CLAUDE.md files]]
- **Project-aware** — picks up `CLAUDE.md` from the current folder automatically
- **Tool use** — can run bash commands, search the web, read PDFs, and more depending on permissions
- **Agents** — can spawn sub-agents to handle parallel or complex tasks

---

## How to Use

- Open your terminal inside the folder you want to work in
- Run `claude` to start a session
- Claude loads any `CLAUDE.md` in that folder and begins with that context

---

## Permissions

Claude Code asks for permission before running commands or editing files. You can pre-approve common operations in `.claude/settings.json` to reduce interruptions.

---

## Keyboard Shortcuts

- `Escape` — interrupt a running response
- `Ctrl+C` — exit the session

---

## See Also
- [[claude-md-and-memory]] — how to give Claude persistent instructions
- [[claude-cowork]] — multi-agent collaboration features
- [[claude-chat]] — the browser-based chat interface

---

## Key Takeaways
- Claude Code turns Claude into a file-system-aware agent that can actually do things, not just answer questions
- Always open it from the right folder to activate the correct CLAUDE.md rules
- Permissions can be pre-approved to reduce friction on routine operations
