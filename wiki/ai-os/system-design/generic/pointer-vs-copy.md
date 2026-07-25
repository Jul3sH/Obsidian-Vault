---
type: reference
created: 2026-07-25
tags: [ai-os, system-design, memory, knowledge-management, retrieval]
---

# Pointer vs. Copy (Filing External Knowledge)

> *When knowledge lives in an external source (Google Docs, a webpage, another repo), decide whether to **copy** a distilled version into the wiki or merely **point** to the source. Open this when filing anything sourced from outside the vault.*

Every piece of external knowledge you bring into the OS faces one decision: **copy it in, or link out to it.** The wrong default quietly breaks retrieval. This note sets the rule.

---

## The two modes

- **Copy (transcribe inline)** — distil the source into a local markdown note in the vault. The content now lives on disk, owned, indexed, graph-connected.
- **Point (link out)** — the note holds only a reference (URL / Doc link / MCP resource). The content stays in the external system.

They are the same *pointer-vs-copy* trade-off used inside the memory layer (vectors that copy text vs. reference offsets — see [[session-transcripts-and-memory|Session Transcripts & Memory]]), applied at the **source** level.

---

## The rule

**Copy the load-bearing synthesis; point to the bulky living source; never pointer-only for critical knowledge — and where possible, do both in one note (inline summary + link back).**

- **Copy** when the knowledge is load-bearing, retrieved often, decision-relevant, or must be reliable in headless/scheduled runs.
- **Point** when the source is large, living (updated by someone else), and only consulted in full occasionally.
- **Both** is the strongest pattern: an always-available, indexed local summary *plus* a breadcrumb to the full source for when you want depth and the connector is up.

---

## Why copy beats pointer for anything that matters

| Dimension | Copy (local wiki note) | Point (link to Google Doc / external) |
|---|---|---|
| Availability | Always — local file, no auth, no network | Only when the connector/auth/network is up |
| Headless/cron runs | Works | May be entirely absent (interactive MCP servers drop out) |
| Semantic index | Embedded in the memory vector store → recall by meaning | Invisible — the index cannot read what it can't fetch locally |
| Obsidian graph | Backlinks + graph view | Outside the graph |
| Cost/latency | Instant read of a few KB | Re-fetch large doc every time; token-limit chunking tax |
| Ownership/durability | Markdown you own, git-able, survives source deletion | Rots silently if source is moved/deleted/permission-revoked |
| Staleness | Can drift from an updated source | Always current with the source |

The single advantage of pointing — **no duplication / always current** — only wins when the content changes often *and* you don't need it reliably.

---

## The failure mode to avoid

**Pointer-only for critical knowledge.** A note that merely links to a Google Doc half-works at random, because the claude.ai Drive/Docs MCP connector disconnects frequently and is often missing in scheduled runs (observed dropping repeatedly within a single session). If the OS must be able to retrieve something, that something has to be *copied local*. Reserve pointer-only for genuinely disposable or purely-reference material.

---

## Quick decision test

> Will the OS ever need to *retrieve or reason over* this content when the source connector might be down (including any cron/headless run)?
> - **Yes** → **Copy** (distil inline; optionally also link the source).
> - **No, it's bulk reference I'll open manually and rarely** → **Point**.
> - **In doubt** → **Copy.** Local, indexed, and owned is the safe default.

---

## See Also
- [[session-transcripts-and-memory|Session Transcripts & the Memory Layer]] — the same trade-off inside the vector store
- [[documentation-conventions|Documentation Conventions]] — how notes are structured
- [[system-design-principles|System Design Principles]]
