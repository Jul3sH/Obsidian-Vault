---
type: reference
tags: [notebooklm, integration, claude, mcp, browser-automation]
created: 2026-06-03
---

# NotebookLM Integration Options

> *How to connect Claude-style agents to NotebookLM. Two main patterns exist — choose based on how much programmatic control you need.*

---

## Two Integration Patterns

There are two main ways to connect Claude-style agents to NotebookLM:

| Pattern | How it works | Primary strength |
|---|---|---|
| **MCP / browser-automation** | Drives the NotebookLM web UI through Chrome (Patchright/Playwright) | Fast path to source-grounded Q&A with minimal setup |
| **Tenglin / direct-client** | Authenticates once, then calls undocumented NotebookLM backend endpoints directly | Full programmatic control; NotebookLM as a backend service |

---

## Pattern 1 — MCP / Browser Automation

**Example:** `PleasePrompto/notebooklm-skill` and its companion MCP server.

**How it works:**
- Opens Chrome, logs into Google, stores browser/session state locally
- Asks NotebookLM questions via automated web interactions
- MCP-server variant adds persistent chat sessions and wider client compatibility (Claude Code, Codex, Cursor)

**Capabilities:**
- Source-grounded Q&A over existing notebooks
- Citation-backed answers
- Notebook library management
- Persistent auth across sessions

**Typical use cases:**
- Quick CLI access to NotebookLM
- Reducing hallucinations by letting Claude consult a private knowledge base
- Research assistance without copy-pasting

**Limitations:**
- Brittle — dependent on UI layout and session behaviour
- Slower due to browser overhead
- Some variants are stateless per question (no persistent conversation context)
- Ongoing browser use during queries

---

## Pattern 2 — Tenglin / Direct-Client

**Example:** `teng-lin/notebooklm-py`.

**How it works:**
- One-time browser-based login or cookie import for authentication
- Normal operation via undocumented internal NotebookLM APIs (no browser required after auth)

**Capabilities:**
- Full notebook CRUD (create, read, update, delete)
- Source ingestion
- Chat and research agents
- Artifact generation: audio, video, slide decks, quizzes, flashcards, infographics, data tables, mind maps
- Downloads/exports
- Sharing controls
- Multi-account profiles
- Agent integration via Python, CLI, or skill install

**Typical use cases:**
- Research automation pipelines
- Batch content generation
- CI/CLI workflows
- Using NotebookLM as a backend service for agents rather than as a chat window

**Limitations:**
- Unofficial — relies on undocumented endpoints that may break if Google changes internals
- No SLA or support from Google
- Auth tokens expire and require periodic refresh

---

## Comparison Table

| Aspect | MCP / Browser Automation | Tenglin / Direct-Client |
|---|---|---|
| How it works | Automates the web UI in Chrome | Calls undocumented backend endpoints after auth |
| Browser dependency | Ongoing during queries | Login/cookie extraction only |
| Setup model | Clone or add MCP, log in once | Python SDK / CLI with broader automation patterns |
| Main strength | Fast path to source-grounded Q&A | Much richer programmatic control and non-UI features |
| Main weakness | Brittle, slower, tied to UI/session behaviour | Unofficial; endpoints may break without notice |

---

## Decision Rule

- Use **MCP/browser** when you mainly want Claude to ask NotebookLM questions through the web product with minimal setup.
- Use **Tenglin** when you want NotebookLM to behave like an unofficial programmable platform for automation, batch workflows, and richer artifact generation.

---

## Key Takeaways

- Both patterns require an auth step with the NotebookLM web UI (either ongoing or one-off)
- The Tenglin approach is significantly more capable but carries unofficial-API risk
- Neither pattern is officially supported by Google
- For this wiki's own deployment, the Tenglin approach was chosen — see [[notebooklm-tenglin]] in AI OS System Design for the technical implementation

---

## Related

- [[notebooklm-tenglin]] — Implementation design for the Tenglin integration in this AI OS
- [[claude-cowork]] — MCP servers, skills, and how Claude Code integrates with external tools
