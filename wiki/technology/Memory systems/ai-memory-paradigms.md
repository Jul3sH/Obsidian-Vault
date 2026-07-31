---
type: reference
created: 2026-07-29
tags: [technology, ai, memory, architecture]
---

# AI Memory Paradigms: Write-Time vs Query-Time

> *The two fundamental ways to structure an AI context layer, and the trade-offs that follow from each. Source: Nate B Jones, "Karpathy's Wiki vs. OpenBrain" (2026-04-22), [YouTube](https://www.youtube.com/watch?v=dxq7WtWxi44).*

Andrej Karpathy posted a deceptively simple idea: use your AI to build and maintain a personal wiki of folders and text files. It drew 41,000 bookmarks. Nate B Jones, who built OpenBrain (a database-backed memory system), argues the two approaches are not the same thing at all and that choosing between them is one of the highest-leverage decisions of 2026.

## The Fork Everything Follows From

> **When does the AI do the hard thinking: when information comes *in*, or when you *ask* about it?**

Every AI knowledge system must answer this. Everything else is downstream.

| | **Write-time** (Karpathy's wiki) | **Query-time** (OpenBrain) |
|---|---|---|
| **On ingest** | AI reads the source, extracts what matters, updates topic pages, builds cross-references, flags contradictions | AI stores faithfully: tags, categorises, makes searchable. No synthesis |
| **On query** | Browse pre-built understanding. Retrieval only, near-zero AI work | AI reads relevant entries and synthesises fresh, on the fly |
| **AI's role** | **Writer / maintainer** doing editorial work | **Reader / librarian** doing analytical work |
| **Cost profile** | Heavy on the front end, cheap answers thereafter | Cheap ingest, cost recurs on every query |
| **Metaphor** | A study guide a great tutor keeps rewriting as you learn | A pristine filing cabinet with a brilliant librarian beside it |

Karpathy's own framing: knowledge is **compiled once and then kept current**, not re-derived on every query. Most AI tools burn tokens re-deriving; the wiki compiles.

## Karpathy's Wiki: Principles

- **Compile once, keep current.** The synthesis persists instead of being thrown away after each question.
- **A persistent artifact of evolving thinking**, not merely file organisation. It tracks how understanding changed over time.
- **AI as maintainer.** Working setup is an AI agent on one side and Obsidian on the other; the LLM is "the programmer for the codebase of the wiki".
- **File over app.** Plain folders and text files. You own it, no platform can reprice or lock you in.
- **Raw sources kept untouched** in their own folders, so you can always return to originals.

## OpenBrain: Principles

- **Store faithfully now, synthesise later.** Structured tables wait until a question arrives.
- **AI as reader.** Searches the database, reads entries, returns a precise synthesis grounded in detail.
- **Structured data enables precise operations**: filter by date, client, or value; sort; work across hundreds of entries.
- **Multi-agent by design.** Multiple tools read and write the same store concurrently.
- **No SaaS middlemen.** Data lives in a database you own.

## Where Each Wins

| Wiki wins | OpenBrain wins |
|---|---|
| Deep solo research mode (10 papers over weeks) | Precise structured queries ("every Q1 meeting where pricing was discussed") |
| Value lies in the *connections between* sources, not any one source | Value lies in exact, filterable facts |
| Watching your own understanding evolve over months | Multi-agent access: Claude, ChatGPT, Cursor, automations hitting one store |
| Contradictions surfaced at the moment of ingest | High volume across many categories |
| Solo practitioner, thinking by reading and browsing | Teams, audit-ready provenance, infrastructure meant to scale |

Karpathy's approach is explicitly built for a researcher thinking deeply about a problem. As Jones puts it: "it's written for him, you could tell".

## Where Each Breaks

**Wiki breakpoints**
- **Scale ceiling: roughly 100 to 10,000 high-signal documents.** Above that you need extra search tooling. It is not corporate-level memory, and Jones is emphatic that orgs should not use it as a company context layer.
- **Teams and multi-agent break it.** Two agents editing the same markdown page creates conflicts and a merged synthesis that reflects nobody's actual understanding. The structure presupposes a single agent writing in one place.
- **Speed mismatch.** Optimised for papers-and-articles pace, not Slack-message-and-ticket pace. Live deal flow or daily project status makes re-synthesis punishing, because one change ripples across multiple pages.
- **Staleness reads as active misinformation.** A neglected wiki drifts: old syntheses become wrong but still read with the confidence of well-written prose. You will not question the gap you cannot see.

**OpenBrain breakpoints**
- **Deep synthesis quality.** Synthesising 15 facts at once works, but unpredictably, because it searches the shelves from scratch each time with no prior map. Rarely as good as a deliberately pre-built synthesis.
- **Browsability.** Deliberately headless. There is no artifact to open and wander through (mitigated by bolting on a viewer such as Obsidian).
- **Contradiction blindness.** Contradictory facts sit silently in adjacent rows unless you ask exactly the right question. Databases are not contradiction-aware by default.
- **Staleness reads as ignorance**, which is safer: a gap looks like a gap, not like a confident wrong answer.

## The Editorial Risk (The Wiki's Quiet Trap)

Every time the AI turns a raw source into a wiki page it makes **editorial decisions**: what to frame, what to connect, what to drop. Those are the AI's choices, not yours.

- Important nuance can vanish and you would never know, because the wiki reads so cleanly.
- Jones's analogy: the same trap as **dashboards versus spreadsheets**. A dashboard is easier to read but is a condensation that can hide exactly what you need to see.
- Karpathy's design keeps raw sources intact, but **most people will not maintain the discipline to go back to them.** The source of truth quietly shifts from raw material to the AI's summary of it, and errors bake into your understanding.
- Consequence: **the instruction file telling the AI how to organise the wiki becomes the highest-leverage document in the whole system.** Most people will underinvest in it.

## Contradictions Are Sometimes the Point

The most important nuance in the comparison.

- Engineering thinks the build is 12 weeks. Sales promised the client 8.
- A well-meaning wiki may resolve that into a coherent narrative: "roughly 10 weeks".
- **That gap was the strategic signal.** It is exactly the misalignment leadership needed to see.
- A database that stores both views without resolving them preserves the tension.

Corollary: an organisation's AI-generated knowledge (meeting summaries, strategy docs, research outputs) is currently **write-once, read-never**. It is either a compounding asset or a growing pile of noise, and most teams choose by accident.

## What Both Approaches Agree On

Despite the implementation split, the underlying theses converge:

1. **You own the artifact, not the tool.** "File over app" and "no SaaS middlemen" are the same conviction. Nobody should be paid to own your context layer.
2. **The human's job is curation and questioning.** What goes in, what to ask. There is no substitute for thinking carefully about how to organise your context layer.
3. **Memory compounds through intentional structure**, not random accumulation. Only the timing and location of that structure differ.
4. **The primary user is an AI agent working on your behalf, not you reading in a browser.** Human readability is a bonus; agent accessibility is the requirement.

## The Hybrid Resolution

Jones's proposed architecture, rather than choosing one:

- **Database stays the single source of truth.** All new information ingests there first.
- A **compilation agent** runs on a schedule (daily, weekly, on demand), reads the structured data, forms a knowledge graph, and generates wiki pages.
- **The wiki is never edited directly.** If a page is wrong, you fix the source data and regenerate.
- This kills the error-compounding problem: the wiki cannot drift from reality because it is always rebuilt from ground truth.
- The generated synthesis is *richer* than raw-file ingest, because it can filter by date, category, or confidence before synthesising.
- Result: structured storage and agent access underneath, a browsable compiled understanding layer on top.

## Two Ideas Worth Adopting Regardless

- **The idea file as a publishing format.** Karpathy did not ship a tool. He published a high-level description designed to be pasted into an AI agent that builds the specifics with you. It respects the reader's agency: they add their own commentary and decide details with the agent, starting from a proven pattern.
- **AI from oracle to maintainer.** The deepest insight. Most people treat AI as something you ask questions to. Karpathy treats it as something with an **ongoing job**: maintaining a knowledge artifact that improves over time. The shift is from an answer engine to a maintainer of thinking systems, leaving humans to curate, select, and explore.

## Key Takeaways

- **One decision drives everything: does the AI think at ingest or at query?** Write-time (wiki) versus query-time (database).
- **Wiki = study guide** (pre-built understanding, cheap answers, solo, narrative). **Database = filing cabinet plus librarian** (faithful storage, precise queries, multi-agent, scalable).
- **The wiki's scale ceiling is roughly 100 to 10,000 documents** and it breaks on teams, multi-agent writes, and fast-moving operational data.
- **Wiki staleness is more dangerous than database staleness**: confident prose that is quietly wrong versus a visible gap.
- **Synthesis is lossy and editorial.** The AI's framing choices silently become your source of truth unless you deliberately return to raw sources.
- **Contradictions can be the most valuable content in a knowledge base.** A wiki may smooth them away; a database preserves them.
- **Both camps agree** on owning your own artifact, human curation, intentional structure, and agent-first access.
- **The hybrid answer**: database as source of truth, wiki as a regenerated compiled view that is never edited directly.

## Scope note: which "memory" this article means

This article uses **memory** in the broad sense: any mechanism that persists knowledge
across sessions. In that sense a maintained wiki is a memory paradigm, which is why
it appears here as one of the two options.

That is a different sense from the narrow one used by an agent's own memory rules,
where "memory" means the small curated behavioural store loaded at session start and
protected from bloat. A knowledge base can be memory in the first sense while rules
correctly forbid putting knowledge-base content into memory in the second sense.

Both are branches of the **Storage** pillar, split by the question they answer:
"is this true?" versus "does this change how I act?". See
[[memory-observation-layer]] for the derivation, and the four-pillar model
(Capture, Storage, Injection, Recall) that both sit inside.

## Related

- [[memory-observation-layer]] - the capture pillar, and where the canonical and behavioural branches of Storage divide
- [[memory-semantic-search]] - the injection and recall pillars, including scheduled versus triggered injection
- [[openbrain-vs-agentic-os]] - OB1 and the Agentic OS memory system compared, both query-time
- [[openbrain-vs-personal-ai-os]] - how this vault maps onto the paradigms
- [[postgres-pgvector]] - what Postgres, pgvector, PGLite, and Supabase each actually are
- [[agentic-os/memory-system-architecture|Agentic OS Memory System Architecture]]
