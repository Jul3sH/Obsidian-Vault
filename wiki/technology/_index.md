---
type: index
updated: 2026-05-21
---

# Technology

> *Reference library for technical tools, products, and concepts - not a workstream, but a shared knowledge base.*

This folder is for **technical reference material**: product capabilities, pricing, APIs, infrastructure concepts, and tool comparisons. It is not for skills (those live in [[ai-os/skills/_index|AI OS / Skills]]) or operational process (that lives in [[ai-os/service-design/_index|AI OS / Service Design]]).

**Filing test: technology vs AI OS**
> Would this content be useful to *anyone* using this tool, regardless of their personal setup?
> - **Yes** → file here in `wiki/technology/`
> - **No, it only makes sense in this specific environment** → file in [[ai-os/service-design/_index|wiki/ai-os/service-design/]]

*Example: Claude Code platform docs belong here (generic). VPN routing rules for Hong Kong belong in AI OS service-design (environment-specific).*

## Sections

| Section | What's in it |
|---------|-------------|
| [[technology/sales-marketing-tech/_index\|Sales & Marketing Technology]] | Vendor capabilities, price books, use-case coverage, and pipeline architecture for cold email outreach and lead enrichment |
| [[technology/claude-anthropic/_index\|Claude & Anthropic]] | Platform documentation: Claude Code, Claude Chat, Claude Cowork, and CLAUDE.md memory system |
| [[technology/claudeclaw-business-os/_index\|ClaudeClaw Business OS]] | Telegram bot that pipes Claude Code to your phone: public vs members editions, versioning, and relationship to Claude Code |
| [[technology/claudeclaw-enterprise-os/_index\|ClaudeClaw Enterprise OS]] | Enterprise product line placeholder, to be documented |
| [[technology/agentic-os/_index\|Agentic OS]] | Turn Claude Code into an agentic operating system: identity, skills, semantic memory, multi-client isolation |

## AI Memory Architecture

How AI context layers are structured, and how the main implementations compare.

- [[wiki-vs-openbrain|AI Memory Paradigms: Write-Time vs Query-Time]] - The fork every AI knowledge system must answer, Karpathy's wiki versus OpenBrain, where each wins and breaks, and the hybrid resolution.
- [[openbrain-vs-agentic-os|OpenBrain (OB1) vs Agentic OS Memory]] - Two query-time database systems compared: multi-tool bus versus multi-client runtime, faithful store versus Haiku pre-compile.
- [[openbrain-vs-personal-ai-os|OpenBrain (OB1) vs This Wiki]] - Why this vault is a Karpathy wiki, and how its wiki-to-Jira flow inverts the proposed hybrid.
- [[postgres-pgvector|Postgres, pgvector, PGLite and Supabase]] - What each term actually is. Only one of them is a database engine.
- [[memory-pillars|The Four Pillars of Memory Systems]] - **the model.** Capture, Storage, Injection, Recall, each with its two sub-types; the pillar-versus-enabler distinction; and the amendment splitting capture out of Simon Scrapes' three pillars.
- [[memory-observation-layer|Observation Layer]] - **enabler for Capture.** What counts as one, when it is justified, and three hypotheses that would have required one, all tested and failed.
- [[memory-curated-index|Curated Index Retrieval]] - **enabler for Recall (write-time).** The hand-authored index and wikilink scheme: how the hop chain works, why the one-line descriptions are the ranking function, and its dominant failure mode of invocation.
- [[memory-semantic-search|Semantic Search]] - **enabler for Recall (query-time) and Injection (triggered).** The five-criteria test for justifying a vector index, and scoring of the commonly-cited use cases.

## Data Sources

- [[adzuna-uk-job-market-data-source|Adzuna as a UK Job-Market Data Source]] - Coverage, reliability, and limitations of Adzuna for UK job-market analysis. ONS- and academic-validated for trends/relative comparison; an indicator not a census for absolute counts.

## Reports

- [[where-ai-automates-cybersecurity-processes-briefing|Where AI Automates Cybersecurity Processes, and Where It Can't]] - Storm Research briefing on which cybersecurity workflows AI can automate and where human authority remains necessary.

## Adding New Content

File technical reference material here when it is:
- A product or vendor capability profile
- A pricing reference or price book
- A technical concept or protocol reference
- A tool comparison or decision framework

If it involves how a skill *uses* a tool, that documentation lives in [[ai-os/skills/_index|AI OS / Skills]] instead.
