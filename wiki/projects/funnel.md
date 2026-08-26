---
type: funnel
updated: 2026-08-17
---

# Project Funnel

Parked Project candidates across all workstreams — not yet gate-qualified. When ready, promote via `/project-planner`.

Each item carries just enough information to make a meaningful go/no-go decision at the commitment gate without re-researching from scratch. Sizing and WSJF scoring happen later, during the Review stage (via `/project-planner`).

**Fields:**
- **Item** — name of the idea
- **Hypothesis** — one sentence: the concrete payoff if this gets done
- **Trigger** — what needs to be true for this to move to Review
- **Added** — date parked
- **Jira** — POR board card (Epic, label `funnel`, status `Funnel`) — sits in the board's Backlog view as a visual reminder, not on the active columns. Created alongside the row; removed (transitioned/relabelled) when the row graduates via `/project-planner`.

---

## Career

| Item | Hypothesis | Trigger | Added | Jira |
|------|------------|---------|-------|------|
| Claude Architect | Positioning as a GenAI-era Solution/Cloud Architect will materially improve employability in HK and UK, building on 20+ years of enterprise architecture capital with targeted AI upskilling | [[genai-sa-market-validation\|GenAI SA Go/No-Go (POR-16)]] returns a "go" verdict — without it, this is hobby activity, not a funded project | 2026-06-21 | [POR-14](https://agileict.atlassian.net/browse/POR-14) |

## Finance

| Item | Hypothesis | Trigger | Added | Jira |
|------|------------|---------|-------|------|

## Performance

| Item | Hypothesis | Trigger | Added | Jira |
|------|------------|---------|-------|------|
| [[agile-claw-mvp\|Agile Claw MVP]] | Creating an open-code-based ClaudClaw OS will build skills for AI leverage and AI agentic engineering development, and generate enough conviction to commit to testing AI consulting as a real revenue stream. Full original build scope preserved in the project file under "Parked — Awaiting Validation". | Treat as a hobby until I decide consulting is a path | 2026-05-25 | [POR-1](https://agileict.atlassian.net/browse/POR-1) |
| Early Adopters ClaudClaw OS | Deploying ClaudClaw OS with early adopters will produce concrete findings for Agile Claw MVP, build skills for AI leverage and AI agentic engineering development, and generate enough conviction to commit to testing AI consulting as a real revenue stream | Treat as a hobby until I decide consulting is a path | 2026-06-17 | [POR-10](https://agileict.atlassian.net/browse/POR-10) |
| Agentic Academy Agentic OS | Hands-on testing of Agentic Academy's Agentic OS will produce concrete findings for Agile Claw MVP, build skills for AI leverage and AI agentic engineering development, and generate enough conviction to commit to testing AI consulting as a real revenue stream | Treat as a hobby until I decide consulting is a path | 2026-06-17 | [POR-12](https://agileict.atlassian.net/browse/POR-12) |
| [[memory-system-explained\|Claude Memory System — understand & document]] | A clean, correct mental model + permanent reference for how Claude's memory works (auto-memory vs rulebook vs transcripts; the folder/index/naming trap) stops this recurring as a distraction and lets me govern memory deliberately. Summary + open threads already parked in [[memory-system-explained]] (§ Parked). | A dedicated AI-OS documentation session — NOT during a job-search / relocation timebox. Resume by finishing the restructure listed in the doc's Parked section. | 2026-07-23 | TBD (create on next `/jira-sync`) |
| Claude-only work admission lane | A lightweight admission path for technical-debt-type enablers executed entirely by Claude (near-zero attended minutes, token cost only) removes ceremony friction sized for Julian-attended work: today the Deliverable-First gate demands `/define-task` + `/prompt-zero` even when Julian's role is a one-line brief and a review, which pushes him to override the gate ad hoc instead (first instance: the mental-models rebuild, 26 Aug 2026). The rethink defines what the gates protect against (scope drift, model-filled assumptions) and what replaces them at this effort class - e.g. a standing brief template, token budget, and review-only DoD. | Next AI-OS service-design session; or the second ad-hoc gate override, whichever comes first | 2026-08-26 | TBD (create on next `/jira-sync`) |
| Source attribution convention (`source:` frontmatter) | Extending the existing `source:` field from data provenance (pricing pages, Sheets, raw files: ~18 files today) to **idea attribution by named person** makes "everything in the vault that came from Nate B Jones / Kashef / Kaufman / Karpathy" a one-line grep instead of a memory exercise. 26 files currently attribute in prose only. Sized 2 (5-8h), almost entirely backfill. Cheap write-time answer to the provenance question that would otherwise be the argument for a vector index: see [[memory-recall]] (§ Assessment of one environment). | A dedicated AI-OS documentation session, same trigger as the row above and best done alongside it. **Deliberately parked, not queued:** `grep -rli "nate b jones" wiki/` already finds all 26 files, so the incremental gain is consistency and odd-spelling coverage only. Promote only if a provenance query actually fails in practice. | 2026-08-05 | TBD (create on next `/jira-sync`) |
| Start-here enforcement hook | A `UserPromptSubmit` hook that greps the prompt for a tight workstream keyword list and injects a one-line pointer to that workstream's `start-here` file would stop high-value prep being missed at exactly the moment it matters. **Evidenced failure, 8 Aug 2026:** [[tti-ea-governance-value]] - the EA-value argument built specifically for Ty conversations and hardened through two Fable passes - was not consulted while drafting [[tti-ty-engagement-proposal]] for Ty. [[tti-start-here]] points at it three times; the index was fine, the agent simply never opened it. The lesson is that **an index only works if something forces it to be read**, and instructions in CLAUDE.md still depend on the agent remembering, whereas a hook is executed by the harness regardless. Secondary finding: only ONE start-here file exists in the vault (TTI's) - [[uk-relocation-project]] carries ~30 files with no entry point, so the convention itself is under-adopted. | After the TTI Ty engagement concludes. Two things to decide at Review: the keyword list must stay tight (a hook that fires on everything becomes noise the agent skims past, reproducing the failure), and whether to write start-here files for the other large workstreams first, since the hook is only worth building once there is more than one to point at. | 2026-08-08 | TBD (create on next `/jira-sync`) |

## Personal

| Item | Hypothesis | Trigger | Added | Jira |
|------|------------|---------|-------|------|

## Relationships

| Item | Hypothesis | Trigger | Added | Jira |
|------|------------|---------|-------|------|
| [[banter-trainer-mvp\|Banter Trainer (for Sophia)]] | A Claude-powered app that drills Sophia on responding to UK-style banter under time pressure, coaching her toward ~5 rehearsed "stay cool, don't take the bait" moves, will reduce over-sensitive reactions and lower her bullying risk in the UK move - and may generalise into a product for other kids | UK move is committed (done); decide the simplest-path MVP (likely just using/enhancing an existing app - see [[banter-trainer-mvp]]) is worth a session vs competing relocation priorities. Objective = a usable tool for Sophia, NOT a build project; productization is a separate, later, Performance decision gated on "useful to others AND not a distraction from the job search" | 2026-07-08 | TBD (create on next `/jira-sync`) |

## Wellbeing

| Item | Hypothesis | Trigger | Added | Jira |
|------|------------|---------|-------|------|
