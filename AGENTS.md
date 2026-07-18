# AGENTS.md - Canonical Cross-Agent Operating Layer

This file is the single source of truth for the **always-on, agent-agnostic rules**
that govern this Obsidian wiki. It is read directly by Codex and OpenCode, and
imported by `CLAUDE.md` for Claude Code. Any rule that must hold on every turn,
regardless of which agent is running, lives here and nowhere else.

Three layers exist (do not move content between them without reason):

1. **This file (`AGENTS.md`)** - always-on universal rules. The auto-loaded surface.
2. **The wiki (`wiki/ai-os/`)** - deep doctrine and rationale, read on demand. The
   canonical reference. This file points to it; it does not duplicate it.
3. **Agent wrappers (`CLAUDE.md`, and any future Codex/OpenCode-only file)** - thin
   adapters holding only tool-specific mechanics that cannot be shared.

If something is universal, it belongs here. If it exists only because of one agent's
loading model, memory system, or skill mechanism, it belongs in that agent's wrapper.

---

# Writing Style

- NEVER use em dashes (—) or en dashes (–) in any output: wiki articles, messages,
  drafts, documents, commit messages, or chat responses. They are a recognisable
  AI-writing tell. Use a comma, full stop, colon, parentheses, or a spaced hyphen
  (" - ") instead. This applies to everything written from now on, including
  drafts intended for the user to send onward.

---

# Knowledge Base Rules

- When creating or editing wiki content, follow
  `wiki/ai-os/system-design/generic/documentation-conventions.md` (dual-audience:
  succinct for the LLM, navigable for the human; visual-first: tables + Excalidraw;
  and the human-navigation vs LLM-flatness balance: challenge hierarchy that would
  burn excessive tokens rather than silently building it).
- This is an LLM-maintained knowledge base. You are the librarian.
- The wiki/ folder is YOUR domain: you write and maintain everything in it.
  The user rarely edits wiki files directly.
- raw/ is the inbox. When the user dumps files here, you process them into the wiki
  during a "compile" step.
- After every compile, move the processed raw file(s) to raw/_processed/.
  This keeps raw/ root as a clean pending-only inbox. Update raw-manifest.md
  (wiki/ai-os/logs/raw-manifest.md) with a row for every file moved.
- **Exception: `raw/brain-dump.md` is a persistent capture inbox**, not a
  one-shot file. It is the zero-evaluation "Someday/Capture" dump for raw,
  unclassified ideas (the stage before the project funnel). Do NOT move it to
  raw/_processed/. Instead, when processing it, triage each *item* to its
  destination: the project funnel (`wiki/projects/funnel.md`, including XXS
  standalone deliverable ideas), a wiki article, or the bin, and remove
  the triaged item from brain-dump.md. The file itself stays. See
  `wiki/ai-os/service-design/prioritization-framework.md` (capture, funnel,
  scheduled) for the model.
- wiki/_master-index.md is the entry point. It lists every topic folder with
  a one-line description. Always keep this up to date.
- Each topic gets its own subfolder in wiki/ (e.g., wiki/ai-agents/) with its
  own _index.md that lists all articles in that topic with brief descriptions.
- Always use [[wiki links]] to connect related concepts across topics.
- When compiling raw material:
  1. Read the raw file
  2. Decide which topic it belongs to (or create a new one)
  3. Write a wiki article with key takeaways and relevant links
  4. Update that topic's _index.md
  5. Update wiki/_master-index.md
  6. If a raw file spans multiple topics, create articles in both and cross-link
- Keep articles concise: bullet points over paragraphs.
- Include a ## Key Takeaways section in every wiki article.
- All outputs (reports, summaries, query results) are saved inside wiki/
  as articles or a dedicated report file. There is no separate output folder.
- When answering questions, read _master-index.md first to navigate, then
  drill into the relevant topic _index.md, then read specific articles.
- When the user asks you to "compile", process everything in raw/ root that hasn't
  been compiled yet into the wiki. raw/ root = pending only; raw/_processed/ = done.
  Do not reprocess files already in _processed/. Cross-reference
  wiki/ai-os/logs/raw-manifest.md for the full compiled file list and destinations.
  After compiling each file, move it to raw/_processed/ and add a row to the manifest.
- When the user asks you to "audit" or "lint", review the wiki for inconsistencies,
  broken links, gaps, and suggest improvements.

---

# Project Status Updates (all agents)

Whenever any agent produces output that is linked to a Project (a new file, a corrected artefact,
a completed review, or any work that results in a new row in a Project's File Map), the Project
status surface (`wiki/projects/[project].md`) MUST be updated in the same operation. No exceptions.

**Three things must all be updated together:**

1. **Status section header** - rewrite it to reflect the current position as of today. The most
   recent development goes first, before older standing paragraphs. A reader opening the file
   should see the newest thing at the top, not appended at the bottom. The section must be a
   complete current picture, not a growing list of tacked-on additions.

2. **Next Actions list** - add, remove, or reprioritise items to reflect what actually needs to
   happen next. If a piece of work is done, remove or mark it. If new work is unblocked or
   required, add it. Do not leave the list in a stale state from a prior session.

3. **Status log** - add a new row (newest first) summarising what was done, what was found, and
   what the decision impact is. Link directly to every artefact produced, including spreadsheets
   (.xlsx) and companion docs separately. Do not link only to one and expect the reader to find
   the other.

**Why this matters:** the Status section is the only surface Julian reads to understand where a
project stands. If it is not updated, the project is invisible - the work happened but the project
does not know about it. A File Map entry alone is not enough: it shows what exists, not what it
means or what comes next.

---

# Single Source of Truth for Project Numbers (all agents)

When a project accumulates many analyses that quote the same figures (burn rates, runway,
costs, salaries, pot sizes), those numbers drift across files and no one can tell which is
current. This is a recurring failure mode. To prevent it:

- **Each project with material financials has ONE canonical model file**, and that file carries a
  **`## 0. Canonical Summary` block at the very top**: the authoritative table of the project's
  key numbers. **If any number, in that file or any other, disagrees with the canonical summary,
  the summary WINS and the other must be corrected to match.** State this supremacy explicitly in
  the block.
- **Supporting and derivation docs are referenced FROM the canonical model**, not surfaced
  independently to the reader. The project status surface links to the model, not to every
  underlying workbook or reconciliation.
- **When you fold a standalone analysis into the canonical summary, delete the standalone file**
  and repoint its inbound links to the canonical block. A superseded duplicate is the mess this
  rule exists to prevent.
- **Reference implementation (UK Relocation Decision):** [[uk-move-financial-model]] `§0` is the
  authoritative money surface (burn, pot, runway for Stay HK / London-direct / Malvern interim);
  all other UK-move finance docs feed it. The project is being consolidated (from ~30 scattered
  files) to **four hubs** referenced from `wiki/projects/uk-relocation-decision.md`:
  (1) the financial model, (2) `job-market-analysis`, (3) `decision-register`
  (decision journal + criteria matrix merged), and (4) a RAID register. Everything else is a
  Tier-3 supporting doc referenced only from inside its parent hub, or archived if superseded.

---

# Source Document Integrity and Adversarial Review Protocol

These rules apply whenever any agent writes an adversarial review of an existing wiki document.

- **Before beginning any adversarial review, read the multi-agent protocol.** Read `wiki/ai-os/system-design/generic/multi-agent-protocol.md` in full before starting. It defines your role as the reviewer, the output file naming convention (`[topic]-[reviewer]-review-[date].md`), handoff discipline, the authority-level frontmatter to use, and the confirmation-amplification directions to hunt. The rules below are the enforceable subset; the protocol is the full context.
- **Reviews go in new files only.** When conducting an adversarial review of source document X, create a new review file (e.g. `X-[agent]-review-[date].md`). NEVER modify the source document to inject review content, verdict tables, or review summaries. All review output lives in the review file, not the source.
- **Permitted edits to source documents:** you may only edit a source document to correct specific factual errors the review identified (e.g. update a stale number, reframe a biased conclusion). Do not add cross-references from source documents pointing to the review file; add those in the review file and in the relevant index only.
- **YAML frontmatter is strictly key-value YAML.** Only YAML-valid content belongs between the opening and closing `---` delimiters. A markdown table, blockquote, or any other markdown construct is NOT a valid YAML field value and must never appear inside a frontmatter block. The closing `---` delimiter must be on a line by itself with no other characters; a markdown table separator row (`| --- |`) is NOT a frontmatter delimiter.
- **Never truncate an existing frontmatter field value.** When editing any file, preserve all existing YAML fields exactly. If you are adding a new field, add it below the existing ones. Do not overwrite, shorten, or concatenate onto an existing field's value.
- **Read the full file before editing it.** Before modifying any file, read it completely. Confirm the frontmatter structure, where the document body begins, and what existing content your edit would displace or truncate. A partial read before an edit is not sufficient.

---

# Hidden File Visibility (all agents)

Julian works from inside the Obsidian vault and cannot see files that live
outside it. Any agent that keeps **configuration, instruction, memory, command,
prompt, or skill files at a path OUTSIDE this vault** (a hidden path not visible
in Obsidian) MUST mirror each of those files into the wiki so Julian can see and
understand them.

- **Scope, mirror only Julian's own setup:** config files (redacted), global
  `AGENTS.md` deltas, and custom skills / prompts / commands / memory that Julian
  or the agent authored for this environment. **Never mirror the agent's
  shipped/built-in/vendor product files** (e.g. default "system" skills that ship
  with the tool), binary assets (images, archives), licence files, or generated
  caches. The point is to show Julian *his* configuration, not the tool's
  installation.
- **Destination:** `wiki/ai-os/system-design/<your-harness>/` (Claude → `claude/`,
  Codex → `codex/`, OpenCode → `opencode/`), preserving the source's relative
  folder structure and filename, **except: strip leading dots** from any folder or
  file name in the mirror path (`.system` → `system`, `.config.json` →
  `config.json`), because Obsidian hides dot-prefixed names. Record the true dotted
  source path in the harness setup doc's mirror map.
- **Format:** wrap any non-Markdown text file (config, script) in a fenced code
  block inside a `.md` so it renders in Obsidian. Store code/scripts as Markdown,
  never as raw `.py` / `.js`. Do not mirror binaries.
- **Exact copy** of the content, not a summary or adaptation.
- **Update the mirror immediately** after creating or changing the source file.
- **Confirm to Julian** which wiki file mirrors which hidden source path: this
  confirmation is how he knows a file he cannot see has become visible.
- **Never mirror secrets or noise:** no credentials, API keys, auth tokens, OAuth
  files, logs, caches, or session/transient state.
  - When a config file **mixes** secrets with useful settings, mirror the file but
    redact each secret value: keep the key, replace the value with the literal
    token `<REDACTED>` (optionally typed, e.g. `<REDACTED: API key>`). Do **not**
    use length-matching stars (`********`): they leak the secret's length and read
    like a real masked value rather than a deliberate redaction.
  - Add a header note to the mirror so the redaction is explicit:
    `> Mirror copy, secrets redacted. Source: <hidden source path>`.
  - When a file is **nothing but** secrets (e.g. `auth.json`), do not mirror it at
    all; leave a one-line note in the harness folder that the file exists but is
    omitted because it is purely secret material.

Each harness's specific source paths and mirror map live in its setup doc under
`wiki/ai-os/system-design/<harness>/`. This universal rule is the why and the
shape; the per-harness docs are the what.

---

# Wiki Index Structure

The wiki is organised into the following top-level indexes. Always file content
into the correct index. If content doesn't fit any of them, flag it before
creating a new index so the structure can be agreed first.

## Index Files Are Navigation Only (hard rule)

An index file (`_index.md`, `_master-index.md`, or any file whose job is to list
other files) contains ONLY navigation: links to other documents, each with at
most a one-line description of what that document IS. Nothing else.

Indexes MUST NOT contain:
- Current position, strategy, or "what we are doing now"
- Next actions, to-dos, or status
- Decisions, working notes, or any content that changes as work progresses

That mutable state lives in its dedicated home, never duplicated into an index:
- **Current position / strategy** lives in the workstream's living strategy doc
  (root-level, e.g. `tti-engagement-strategy`).
- **Next action / snapshot / status log** lives in the Project status surface
  (`wiki/projects/[project].md`).
- **Draft-level next steps** live inside the working draft itself.
- **Project evidence maps** live in the Project file itself. Every new Project
  page must include a `## Project Summary File Map` near the top, after Status
  and before the Status log, listing the live supporting files grouped by area
  (decision control, domain evidence, source-of-truth docs, reviews, and family
  or stakeholder context as relevant). Use bare `[[wiki links]]`, one row per
  file, and a one-line "Role" explaining what the file is for. This is the
  human navigation hub; do not bury project-critical files only in domain
  indexes.

Why: state copied into an index goes stale the moment the real document moves on,
because the update obligation is silent and easy to miss. A pure-navigation index
never goes stale on state because it holds none. When tempted to write a status or
next-action into an index, put it in the dedicated doc and link to it instead. A
one-line description of what a linked doc *is* (not what its current state *says*)
is the only permitted annotation.

## Top-Level Wiki Indexes

- **wiki/projects/** - All active Projects (Objective + Key Results) across workstreams,
  ranked by T-shirt size. Created by `/project-planner`. Cross-linked to workstreams.
  **Jira mapping:** wiki "Project" = Jira "Epic" issue type. Jira issue types are not renamed.
- **wiki/deliverables/** - Backlog of all deliverables (stories, enablers, tasks) across Projects.
  Created by `/define-user-story`, `/define-enabler`, or `/define-task`. Cross-linked to Projects and workstreams.
- **wiki/ai-os/** - The AI operating layer: all skills, memory conventions,
  service design (workflow), system design (infrastructure), and operations
  logs. See the agent-specific skills rule in each wrapper. The filing taxonomy
  is documented at `wiki/ai-os/taxonomy.md`:
  - `wiki/ai-os/service-design/` - people and process: project workflow,
    ceremonies, prioritisation methodology, operational troubleshooting
  - `wiki/ai-os/system-design/` - tools and infrastructure: architectural
    principles, Jira integration, skill conventions, mirroring rules
  - `wiki/ai-os/skills/` - hybrid: SKILL.md = service, scripts/ = system
  Generic platform/product documentation belongs in wiki/technology/ instead.
- **wiki/career/** - Professional progression, interviews, workplace politics,
  personal brand, and career strategy. Its _index.md also cross-links to
  career-relevant articles filed under wiki/performance/.
- **wiki/finance/** - Personal finances only: budgeting, savings, investments,
  and financial planning. If content is about *learning* a finance concept or
  skill, file it under wiki/performance/ instead.
- **wiki/performance/** - Personal effectiveness, productivity, self-management,
  and working with others. Contains the Personal MBA sub-folders (see below).
  If content is about *learning a concept or skill* in any domain, it belongs
  here rather than in the domain index.
- **wiki/personal/** - Hobbies, enjoyment, life goals, and things personally
  wanted from life that don't fall under any other category.
- **wiki/relationships/** - Personal relationships: partner, family, social
  dynamics, and interpersonal patterns outside of work.
- **wiki/technology/** - Reference library for technical tools, products, and
  concepts. NOT a workstream: a shared knowledge base. Covers anything
  technical: cloud, infrastructure, networking, APIs, and product/vendor
  reference catalogues (capabilities and pricing). Organised into sections
  by domain, e.g. Sales & Marketing Technology. Skills and AI tooling do
  NOT go here: they go in wiki/ai-os/.
  **Filing test:** would this content be useful to anyone using this tool,
  regardless of their personal setup? If yes, wiki/technology/. If it only
  makes sense in the context of this specific environment, wiki/ai-os/service-design/.
- **wiki/enterprise-architecture/** - Reference library for enterprise
  architecture knowledge: frameworks, governance, service design,
  organisational patterns, and market intelligence on how large enterprises
  are architected. NOT a workstream: a shared knowledge base. Covers
  EA frameworks (TOGAF, Zachman), AI strategy and organisational design,
  industry-specific architectural patterns, solution assurance methodology,
  cost management (CTBME, FinOps, TBM). Distinct from wiki/technology/
  (which is product/vendor catalogues) and wiki/ai-os/ (which is Julian's
  own AI operating layer).
  **Filing test:** is this generic enterprise-architecture knowledge:
  frameworks, patterns, governance, organisational design, or market
  intelligence about how enterprises are architected? If yes,
  wiki/enterprise-architecture/. If it's about a specific tool/vendor,
  wiki/technology/. If it's Julian's own setup, wiki/ai-os/.
- **wiki/wellbeing/** - Sleep, energy, alcohol, physical and mental health,
  personal state management.

## Personal MBA Sub-Folders (inside wiki/performance/)
These three sub-folders use Josh Kaufman's Personal MBA framework (Chapters 6-8).
Articles within them should reference relevant Personal MBA concepts where applicable.

- **wiki/performance/the-human-mind/** - Cognition, mental models, decision-making,
  and cognitive biases. How people perceive information and make decisions.
- **wiki/performance/working-with-yourself/** - Self-management: time, energy,
  attention, emotions, habits, focus, and personal effectiveness.
- **wiki/performance/working-with-others/** - Interpersonal effectiveness:
  communication, influence, leadership, conflict resolution, trust, and group dynamics.

## Flagging Rule
If raw material covers "how things work" in a domain not listed above (e.g. a
new subject area), DO NOT create a new index. Instead, flag it to the user with
a suggested structure and wait for agreement before proceeding.

## Folder Structure & Linking Within Project Areas
Full convention: `wiki/ai-os/system-design/generic/documentation-conventions.md`
(Part 2 - Folder structure & linking; Part 3 - current-position surfaces incl. the
engagement-strategy doc). TTI (`wiki/career/tti/`) is the reference implementation. Summary:

- **Active project/workstream folders organise by workflow state**, not type:
  `(root)` = index ONLY (nothing else lives at root); `_wip/` = active drafts plus
  the living strategy doc (live, must-stay-current records); `_reference/` =
  stable knowledge consulted while working; `_on-hold/` = paused, may be
  repurposed; `_archived/` = done/dead, kept for record.
- **Two jobs:** `_on-hold` + `_archived` *hide* paused/dead work from sightline
  (the core value); `_reference` + `_wip` merely *tidy* a large active set.
- **Structure emerges: don't pre-build empty folders.** Start flat; add
  `_on-hold`/`_archived` at the first pause/death, `_reference` when the root
  exceeds ~8-10 files, `_wip` when there are several active drafts.
- **Pure reference libraries (`wiki/technology/`, `wiki/enterprise-architecture/`)
  do NOT use state-folders**: organise them by topic.
- **Use bare `[[note-name]]` links, never path links** (`[[../../area/file]]`).
  Bare links survive file moves between state folders; path links break and force
  link surgery. Use a path only to disambiguate a duplicate filename, and prefer
  keeping basenames unique across the vault so disambiguation is never needed.
- **On a state-move:** move the file and update the source `_index`, destination
  `_index`, and master `_index` if it lists the item. Links are NOT touched
  (they're bare). The index update is mandatory: skipping it rots the structure.

---

# Cold Email Outreach TCO Analysis Rules

When the user asks about cold email tooling, vendor selection, or TCO for outreach:

1. **Read use-cases first, vendors second.** Always read `wiki/technology/sales-marketing-tech/use-cases/_index.md` before opening any vendor file. Use cases define dependencies; vendors only show coverage.

2. **Map the full pipeline before recommending anything.** Check `wiki/technology/sales-marketing-tech/_index.md` for the complete 6-step data flow. Identify which steps the user already has covered vs. which need to be sourced.

3. **Personalisation requires upstream data, always verify.** If the user wants personalised emails using LinkedIn data, confirm these two steps are covered before costing the sequencer:
   - Step 1: Email to LinkedIn URL (reverse lookup)
   - Step 2: LinkedIn URL to profile/posts data (scraping)
   Do not assume the sending platform handles this. It does not.

4. **Cross-reference existing skills before adding cost.** Check `wiki/ai-os/skills/linkedin-enrichment/` and `wiki/ai-os/skills/apollo-person-match/`: these may already cover steps 1 and 2. If active, treat as $0 incremental cost.

5. **Check active subscriptions before adding vendors to TCO.** A vendor the user is already paying for is a sunk cost. Flag it as $0 incremental in the TCO table.

6. **TCO ranking must be cost-first, not judgment-first.**
   The recommended option MUST be the lowest verified incremental cost that covers all required use cases. If a qualitative concern (e.g. warm-up confidence, transparency, reliability) would lead to recommending a more expensive option, you MUST:
   - Verify the concern is supported by a specific wiki fact (a documented limitation, a rating difference, a missing capability). If it is not in the wiki, it is not a valid reason to override cost.
   - Present the lowest-cost option as the recommendation AND the concern as an explicit trade-off.
   - Ask the user to decide, never decide for them that a higher cost is worth it.

7. **For each required use case, find the cheapest qualified vendor, do not anchor.**
   Before selecting any vendor for a use case, read ALL vendors rated as covered for that use case from the wiki and sort by price at the user's stated volume. The cheapest covered option must be identified and presented. Do not anchor on vendors mentioned earlier in the analysis, vendors in the pipeline diagram, or vendors you have already read. The cheapest qualified vendor wins unless the user decides otherwise.

8. **Validation checklist before presenting any TCO recommendation:**
   - [ ] Full 6-step pipeline mapped?
   - [ ] Upstream data steps (lookup + enrichment) confirmed or costed?
   - [ ] Existing skills cross-referenced?
   - [ ] Active subscriptions marked as sunk cost?
   - [ ] Use-case dependencies checked in `use-cases/_index.md`?
   - [ ] Recommendation is the lowest verified incremental cost option?
   - [ ] All covered vendors compared by price for each required use case before selection?
   - [ ] Any qualitative reason to recommend a more expensive option verified against a specific wiki fact?

---

# Risk Framework and Methodology

Risk registers (e.g., decision-support judgement tools) use a **cause -> event -> effect -> response** chain to surface, assess, and track both **risks (threats)** and **opportunities**. This section defines the universal structure so all projects use the same format.

## Risk Anatomy: The Cause-Event-Effect Chain

**Cause** - A root condition or uncertainty that creates the risk environment. Example: "Limited cash and poor job prospects".

**Risk Event** - A specific triggering event that flows from the cause. There can be many events from one cause. Example: "Stay in Hong Kong for a year and don't get a job".

**Risk Effect** - The specific harm (for threats) or positive outcome (for opportunities) that flows from the event. Multiple effects can flow from one event, and each effect has its own impact/probability/response. Format: *bold scenario sentence* (memorable, salient, like you would speak it aloud) followed by impact and probability reasoning (high/medium/low justification in plain language).

Example effect: "**Sophia gets another year behind with French, creating a significant two-year gap** - High impact as two years may be unaddressable and will impact GCSE grades. High probability as two years is significant and hard to bridge."

**Response** - An action that addresses the effect. For threats: reduces impact or probability. For opportunities: exploits, enhances, or accepts the upside. Keep descriptions simple and actionable; long sentences overcomplicate.

## Structure: One Response Row Per Effect

Each risk or opportunity effect gets **one** response row. The Response column names the action type:

**For threats (RISK):**
- **Reduce Impact** - makes the effect less severe if it occurs
- **Reduce Probability** - makes the event less likely to occur
- **Reduce Impact & Probability** - does both; use labelled prefixes in Response Description:

```
Probability: [probability actions, semicolon-separated]
Impact: [impact actions, semicolon-separated]
```

For single-type threat rows, no prefix is needed - list the actions directly, semicolon-separated.

**For opportunities (OPP):**
- **Exploit** - take action to ensure the opportunity occurs; highest-priority response
- **Enhance** - increase the probability or magnitude of the opportunity
- **Accept** - no proactive action; capture it if conditions allow

## Style Conventions (match Julian's register)

Learned from Julian's own edits. Match these when writing rows:

- **Risk Cause** - a terse noun phrase naming the driver, NOT a full sentence. Examples: "Hybrid job requirement", "DBIS has no French curriculum", "Malvern is an interim solution", "Relocation required mid-term". Compress; do not write "Crash-pad interim needs a London hybrid job while the family is Malvern-based".
- **Risk Event** - a terse phrase naming the trigger, not a sentence. Examples: "In London midweek nights away (Tue-Thu)", "Relocate to London from Malvern mid term".
- **Risk Effect** - two parts:
  1. A **bold scenario sentence**, simple and speakable - something Julian would say out loud and remember (e.g. "Sophia loses her bedtime cuddle and Dad's presence 3 nights a week").
  2. Impact and probability reasoning in **Julian's own first-person voice**, short and plain (e.g. "Medium impact as not preferable but manageable. She's mature, loves granny." / "High probability based on the jobs analysis as hybrid has best prospects"). Each on its own line beginning "- ".
- **Response Description** - simple, actionable, semicolon-separated. For threat "Reduce Impact & Probability" rows, prefix each block: "Probability: [text]" then "Impact: [text]" on separate lines. For opportunity rows, plain description of the action to realise or enhance. Long sentences overcomplicate.
- **Assumptions vs supporting evidence** - cite the artefact or source that grounds the assessment (e.g. "Adzuna pull 11 Jul: ~40% of London roles explicitly hybrid"), and flag where it is still an assumption pending due diligence.

## Impact and Probability Assessment

**Impact** (High / Medium / Low) - How severe is the harm if the risk occurs? Consider: financial loss, relationship/wellbeing cost, delay to critical path, or degree of disruption.

**Probability** (High / Medium / Low) - How likely is the risk event to occur? Consider: historical frequency, control strength, external factors, and your confidence level.

**Risk Score** - Calculated as the average of Impact and Probability. If no obvious midpoint, take the higher value:
- High + High = High
- High + Medium = High (take higher)
- High + Low = Medium (average)
- Medium + Medium = Medium
- Medium + Low = Medium (take higher)
- Low + Low = Low

## Residual Risk (Post-Mitigation)

After mitigations are in place, reassess:

**Residual Impact (IMPR)** - The severity of the effect *after* mitigation is applied.

**Residual Probability (ProbR)** - The likelihood of the event *after* mitigation is applied.

**Residual Risk (RiskR)** - Recalculated using the same average logic as pre-mitigation Risk.

## Financial Exposure (for Money-Related Risks Only)

For risks with direct financial impact:

**Residual Impact HK$** - The monetary impact post-mitigation (in HK dollars or applicable currency). Example: cost of moving to Malvern instead of London.

**Residual Probability %** - The percentage likelihood of the risk occurring post-mitigation. Example: 60% chance of running out of cash.

**Exposure(R) HK$** - Calculated as: `Residual Impact HK$ * Residual Probability %`. This quantifies your financial risk exposure and helps prioritise which risks warrant most effort.

## RAG Status (Red / Amber / Green)

A judgment call on residual urgency, based on the residual score and your risk appetite:

**For threats (RISK):**
- **Red** - Residual risk is unacceptable; requires immediate escalation or a new response
- **Amber** - Residual risk is elevated but managed; monitor closely, execute responses as planned
- **Green** - Residual risk is acceptable; monitor as part of standard operations

**For opportunities (OPP):**
- **Green** - Opportunity well-secured and likely to be realised; no blocking dependencies
- **Amber** - Opportunity dependent on something not yet secured; execute realisation action
- **Red** - Opportunity speculative, blocked, or at serious risk of being missed

## Decision Impact

**The most important column in a decision-support register.** With many risks, the operative question is NOT "how urgent is the residual risk" but "does this risk materially affect WHICH option is chosen?" A risk moves the decision only if it is (a) materially worse under one option than the others, AND (b) severe enough that it could tip the choice. A risk that is common to all options, or too small to matter, does not help decide - it is noise for the decision even if it is a real risk to manage.

Scale:
- **Material** - could change the chosen option; must be weighed directly in the decision.
- **Marginal** - informs but does not decide; worth noting, not load-bearing. (E.g. a risk that differentiates "move vs stay" but not the live question of "London vs Malvern".)
- **Immaterial** - common to all options or too small; log and monitor, but it does not help choose.

Keep any acceptance judgement or conditions (e.g. "accepted as real but low-probability now; managed by a paid-carer contingency") in the RAG column or the residual columns; Decision Impact answers only the "does it change the choice?" question.

## Supporting Evidence and Due Diligence

Record the facts, research, and due diligence that informed your Impact, Probability, and Residual assessments. This separates assumptions from validated facts and makes it clear which risks need more investigation.

Examples:
- "Adzuna job-market pull: 80 count-queries; 375 real-salary listings"
- "Cecil Road council tax band confirmed Band E from local authority"
- "Sophia's school transition: assumptions on resilience, not yet tested"

## Workflow

1. **Identify risks and opportunities** from project analysis, prior experience, and stakeholder interviews. Record cause, event, effect and RISK/OPP type for each.
2. **Assess impact and probability** pre-response. Make your judgment explicit with reasoning.
3. **Calculate score** (Impact x Probability, 1-25). For threats: high score = bad. For opportunities: high score = desirable (well-secured, high-value upside).
4. **Identify responses** - one row per effect. For threats: Reduce Impact / Reduce Probability / Reduce Impact & Probability. For opportunities: Exploit / Enhance / Accept.
5. **Reassess residual** (IMPR, ProbR, RiskR, financial exposure if applicable).
6. **Assess Decision Impact** (Material / Marginal / Immaterial) - does this row change which option is chosen? Keep acceptance judgement/conditions in RAG or residual columns.
7. **Record evidence** - facts that support your assessments, gaps that need more due diligence.
8. **Monitor and revisit** - update the register as responses are executed and new facts emerge.

---

# Operations Log

- After every compile, refactor, maintenance, or lint operation, append one row
  to the current quarter's log file. No exceptions, no manual input needed.
- Current log file: **wiki/ai-os/logs/log-2026-Q3.md** (covers July-September 2026)
- At the start of a new quarter, create a new log file (e.g. wiki/ai-os/logs/log-2026-Q3.md)
  and update this entry to point to it.
- Log format, one table row per operation:
  | Date | Type | Detail |
  Use these operation types:
  - **Setup** - new folders, indexes, or structural files created
  - **Compile** - raw files ingested and turned into wiki articles
  - **Refactor** - existing wiki structure or articles reorganised
  - **Maintenance** - deletions, deduplication, link fixes, file moves
  - **Lint** - audit or consistency review run
- Keep Detail brief (one sentence). No narrative.
