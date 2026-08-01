---
type: reference
created: 2026-07-29
tags: [technology, ai, memory, architecture, comparison]
---

# OpenBrain (OB1) vs This Wiki

> *How Nate B Jones's OpenBrain compares to the Obsidian wiki plus Claude memory setup documented in [[ai-os/_index|AI OS]]. Assessed against the framework in [[wiki-vs-openbrain|AI Memory Paradigms]].*

**Headline:** this vault is **Karpathy's wiki, not OpenBrain.** It is the write-time, file-over-app, single-maintainer compiled artifact that OpenBrain was explicitly built as an alternative to. The system Jones compares *against* is, structurally, the one already running here.

## What OB1 Is

[OB1](https://github.com/NateBJones-Projects/OB1) describes itself as "the infrastructure layer for your thinking": one database, one AI gateway, one chat channel, with any AI able to plug in.

| Aspect | Detail |
|---|---|
| **Storage** | PostgreSQL plus pgvector, base `thoughts` table, extended via schema sidecars |
| **Hosting** | Supabase by default; Kubernetes for self-hosting |
| **Ingest** | Import recipes (ChatGPT, Obsidian, Gmail, Instagram, X, Google Activity) plus Slack and Discord capture bots |
| **Access** | MCP servers, so Claude Desktop, ChatGPT, Claude Code, and Cursor share one memory |
| **Provenance** | Agent Memory schema adds provenance, review, use-policy, source-reference, relation, recall-trace, and audit sidecars |
| **Stack** | Node/Deno edge functions, SvelteKit and Next.js dashboards, TypeScript, FSL-1.1-MIT licence |

See [[postgres-pgvector]] for what those storage terms actually mean.

## Side by Side

| Dimension | OpenBrain / OB1 | This wiki + Claude memory |
|---|---|---|
| **Substrate** | PostgreSQL plus pgvector | Markdown files in an Obsidian vault, plus a small `memory/` folder of plain text files |
| **When the AI thinks** | **Query time.** Stores faithfully, synthesises on ask | **Write time.** Claude compiles `raw/` into wiki articles on ingest, then moves the source to `raw/_processed/` |
| **AI's role** | **Reader / librarian**, pulling entries and synthesising fresh | **Writer / maintainer.** AGENTS.md states it directly: "You are the librarian" |
| **Retrieval** | Vector search plus MCP gateway, structured and filterable | `_master-index` to topic `_index` to article, plus bare `[[wiki links]]` and grep. Navigation, not query |
| **Multi-agent** | MCP gateway, concurrent read and write by many tools | AGENTS.md invites Codex and OpenCode, but all agents edit the **same markdown files** |
| **Provenance** | Timestamps, source references, recall traces, audit sidecars | `raw/` to `raw/_processed/` plus `raw-manifest.md`. Raw is kept, but synthesis is baked into article prose |
| **Contradictions** | Not native; needs a contradiction-surfacing extension | Compile step can flag them, but prose tends to smooth. Partly solved by the **risk register** (cause to event to effect), which preserves tension by design |
| **Scale ceiling** | Thousands of entries and upward, corporate grade | Jones's stated wiki range of roughly 100 to 10,000 high-signal documents. This vault sits comfortably inside it |
| **Ownership** | "No middleware, no SaaS chains" | "File over app", a vault on disk. **Identical conviction** |

## Where This Vault Already Agrees With Both

- **Own the artifact, not the tool.** OB1's no-SaaS-middleman stance and this vault's plain-markdown-in-Obsidian are the same principle.
- **The human's job is curation and questioning.** The compile, audit, and lint rituals plus the two-key memory approval process (Claude proposes, Julian approves) are exactly this.
- **The primary user is an agent, not a browser reader.** `CLAUDE.md` and `AGENTS.md` are written *for the model*; Obsidian readability is the bonus. This is Jones's stated principle verbatim.

## Where This Vault Differs From Both

**1. The memory folder is already a miniature hybrid.**
`MEMORY.md` (an index, loaded every session) sitting over atomic `feedback-*.md` bodies (loaded on demand) is "index always on, bodies just-in-time". That is a compiled index layer over atomic single-fact rows: wiki-shaped on top, database-shaped underneath. A two-layer memory already runs here, in miniature. See [[memory-system-explained]].

**2. Jones's hybrid already exists here, but inverted.**

| | Jones's proposal | This vault |
|---|---|---|
| Source of truth | SQL database | **The wiki** |
| Generated layer | Wiki pages, compiled from the database | **Jira**, pushed from the wiki by `/jira-sync` |
| Rule | Never edit the wiki directly | **"Wiki always wins"**; Jira gets corrected, never the wiki |

Both a compiled narrative layer and a structured queryable layer exist. The difference is which one is canonical. Jones makes the database authoritative because he is solving for scale and multi-agent access. Making the narrative authoritative is arguably correct here, where the value is in connections rather than filtering 10,000 rows.

**3. No vector search and no query-time synthesis.**
This is the genuine capability gap. There is no way to ask "every deliverable touching pricing across the vault" and get a filtered, ranked answer. Navigation and grep are the only retrieval. For deep synthesis with one primary agent, Jones says this is precisely where the wiki wins and a database is overkill.

## The Risks Jones's Framework Flags for This Setup

| Risk | Why it applies here | Current mitigation |
|---|---|---|
| **Staleness reads as confident misinformation** | A neglected article keeps its authoritative tone while going wrong | The audit and lint rituals, which depend on discipline (the same discipline Jones says most adopters fail) |
| **Multi-agent writes** | The moment Codex and Claude both write the same file, the wiki hits the merge conflict a database exists to prevent | Effectively single-writer today (Claude), which is why it works |
| **Source-of-truth drift** | `raw/_processed/` is archived and the compiled article becomes what is read | `raw-manifest.md` keeps the thread back to source, but only if it is actually followed |

## Key Takeaways

- **This vault is a Karpathy wiki**: write-time compile, file over app, single maintainer, narrative artifact.
- **OB1 is the opposite pole**: query-time synthesis, SQL plus vectors, multi-tool access via MCP, built for scale.
- **The conviction is shared**, only the implementation differs: own your own context layer, no platform in the middle.
- **A hybrid already runs here, inverted.** Wiki is canonical and Jira is the structured projection, the reverse of Jones's database-canonical model.
- **The one real gap is query-time structured recall.** No vector search means no filtered, ranked queries across the vault.
- **The live risks are wiki staleness and any future genuine multi-agent write pattern**, both inherent to the write-time paradigm rather than to this implementation.

## Related

- [[wiki-vs-openbrain|AI Memory Paradigms]] - the write-time versus query-time framework this assessment uses
- [[openbrain-vs-agentic-os]] - OB1 compared to the Agentic OS memory system
- [[postgres-pgvector]] - what Postgres, pgvector, PGLite, and Supabase each actually are
- [[memory-system-explained]] - how the Claude memory layer in this vault works
