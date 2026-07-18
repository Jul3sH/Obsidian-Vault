---
type: system-design
tags: [notebooklm, tenglin, integration, python, api]
created: 2026-06-03
updated: 2026-06-03
repo: https://github.com/teng-lin/notebooklm-py
status: installed
---

# NotebookLM — Tenglin Integration Design

> *Technical design and installation record for Julian's NotebookLM integration, using the `teng-lin/notebooklm-py` direct-client approach. This is environment-specific infrastructure — for the vendor-neutral pattern comparison see [[notebooklm-integration-options]].*

---

## What This Is

`notebooklm-py` is a reverse-engineered CLI by Teng-lin that wraps NotebookLM's internal API (Google's `batchexecute` RPC). It is not an official Google SDK — it is a community tool that gives scriptable, programmatic access to features that are normally only available through the web UI.

---

## Why Tenglin Was Chosen

The MCP/browser-automation pattern was evaluated and rejected on two grounds:
1. **Fragility** — ongoing browser dependency makes it unsuitable for pipeline automation
2. **Capability gap** — browser approach only covers Q&A; Tenglin covers CRUD, artifact generation, batch workflows, and agent integration

The Tenglin approach enables NotebookLM to act as a backend service — consistent with how other enrichment tools (Apollo, RapidAPI) are used in this AI OS.

---

## Installation Record

**Status: ✅ Installed and auth verified** — `notebooklm list` confirmed access to 24+ notebooks.

| Component | Location / Detail |
|---|---|
| Python | 3.13 |
| Virtual environment | `~/.venvs/notebooklm` |
| CLI package | Installed from GitHub (`teng-lin/notebooklm-py`) |
| Browser automation | Playwright (used for auth and some operations) |
| Auth cookies | `~/.notebooklm/profiles/default/storage_state.json` |
| Shell alias | `notebooklm` resolves to the venv binary |

---

## Integration Architecture

```
Claude Code / skill
      │
      ▼
notebooklm CLI / Python client  (~/.venvs/notebooklm)
      │
      ├── Auth: Playwright browser login → stored cookies
      │         (~/.notebooklm/profiles/default/storage_state.json)
      ▼
NotebookLM internal APIs (Google batchexecute RPC — undocumented)
      │
      ├── Notebook CRUD
      ├── Source ingestion
      ├── Chat / Q&A
      ├── Research agents
      ├── Artifact generation
      └── Notes, sharing, profiles
```

---

## Authentication

- **Method:** One-time Playwright browser login; cookies persisted to `storage_state.json`
- **Multi-account:** Supported via named profiles (`--profile` flag)
- **Refresh:** Auth cookies expire — re-run login when `doctor` reports auth failure
- **Diagnosis:** `notebooklm doctor` checks auth and setup health

---

## Full CLI Capability Catalogue

### Notebooks
| Command | What it does |
|---|---|
| `list` | List all notebooks in the account |
| `create` | Create a new notebook |
| `delete` | Delete a notebook |
| `rename` | Rename a notebook |
| `summary` | AI-generated insights about a notebook |
| `metadata` | Export notebook metadata with its source list |

### Sources
| Command | What it does |
|---|---|
| `source add` | Add a file or URL as a source |
| `source add-drive` | Add a Google Drive document as a source |
| `source add-research` | Add research links as a source |
| `source list` | List all sources in a notebook |
| `source get` | Get details of a specific source |
| `source fulltext` | Retrieve full text of a source |
| `source delete` | Remove a source |
| `source clean` | Remove all sources from a notebook |
| `source refresh` | Update/re-process a source |
| `source wait` | Poll until a source finishes processing |

### Chat / Q&A
| Command | What it does |
|---|---|
| `ask` | Ask the notebook a question (core conversational feature) |
| `configure` | Set chat persona and response settings |
| `history` | View or save conversation history |

### Artifact Generation
| Command | What it does |
|---|---|
| `generate audio` | Create podcast-style audio overview |
| `generate slide-deck` | Generate a slide deck |
| `generate mind-map` | Generate a mind map |
| `generate flashcards` | Generate flashcards |
| `generate quiz` | Generate a quiz |
| `generate report` | Generate a structured report |
| `generate infographic` | Generate an infographic |
| `generate data-table` | Generate a data table |
| `generate video` | Generate a video |
| `generate cinematic-video` | Generate a cinematic-style video |
| `download <type>` | Fetch a generated artifact to a local file |
| `artifact list` | List all artifacts in a notebook |
| `artifact get` | Get details of an artifact |
| `artifact poll` | Track artifact generation status |

### Notes
| Command | What it does |
|---|---|
| `note create` | Create a note within a notebook |
| `note list` | List all notes |
| `note get` | Get a specific note |
| `note save` | Save note content |
| `note rename` | Rename a note |
| `note delete` | Delete a note |

### Sharing
| Command | What it does |
|---|---|
| `share public` | Make a notebook publicly accessible |
| `share view-level` | Set view-level sharing permissions |
| `share add` | Add a specific user |
| `share remove` | Remove a specific user |

### Research & Utilities
| Command | What it does |
|---|---|
| `research status` | Check status of a deep-research job |
| `research wait` | Wait until a deep-research job completes |
| `profile` | Manage multiple Google account profiles |
| `language` | Get or set notebook language |
| `doctor` | Diagnose auth and setup issues |
| `skill` / `agent` | Internal skill and agent management hooks |

---

## Planned Use Cases (in this AI OS)

- **Knowledge base ingestion:** push compiled wiki articles into dedicated notebooks for source-grounded Q&A
- **Research automation:** feed raw source material into NotebookLM; retrieve structured summaries back into the wiki
- **Artifact generation:** batch-generate audio overviews or slide decks from wiki content for sharing/presentation
- **Pipeline integration:** use as a downstream step in enrichment or research skills
- **Multi-account:** separate personal and professional notebooks via profiles

---

## Known Risks

| Risk | Mitigation |
|---|---|
| Undocumented APIs may break at any time | Pin library version; monitor for breakage; MCP/browser is the fallback |
| Auth cookies expire | Run `notebooklm doctor` if commands fail; re-run browser login to refresh |
| Google may lock internal endpoints | Accepted risk — no mitigation beyond using the official web UI |

---

## Next Steps

- [ ] Build `~/.claude/skills/notebooklm/` skill wrapping common pipeline operations
- [ ] Test `source add` + `ask` loop for wiki knowledge base ingestion
- [ ] Test `generate audio` for batch artifact generation
- [ ] Document token refresh cadence from real-world usage

---

## Key Takeaways

- Installation complete — auth verified against 24+ live notebooks
- The tool wraps Google's internal `batchexecute` RPC — not official, but fully functional
- Shell alias `notebooklm` is the entry point; Playwright handles auth transparently after initial login
- Covers the full notebook lifecycle: CRUD, sources, Q&A, artifact generation, notes, sharing, and multi-account profiles

---

## Related

- [[notebooklm-integration-options]] — Vendor-neutral comparison of both integration patterns
- [[claude-cowork]] — How MCP servers and skills integrate with Claude Code
- [[skill-conventions]] — Standard structure for building skills in this AI OS
