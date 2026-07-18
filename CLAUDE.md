# CLAUDE.md - Claude Code Wrapper

This is Claude Code's thin agent adapter. The canonical, agent-agnostic rules
(writing style, knowledge base rules, wiki index structure, index doctrine,
folder/linking conventions, Cold Email TCO rules, operations log) live in
`AGENTS.md` and are imported below. Only Claude-specific mechanics that depend on
Claude's loading model, memory system, or skill infrastructure live in this file.

When editing operating rules: if the rule is universal (true regardless of which
agent runs), put it in `AGENTS.md`. If it exists only because of Claude Code's
memory, skills, or hidden-path mirroring, keep it here.

@AGENTS.md

---

# Memory

## What gets loaded at session start
- At the start of every session, read `user.md` from
  `~/.claude/projects/-Users-julianhart-Obsidian-Vault/memory/` before
  responding to the first message. This holds the user profile.
- Load other memory files **on demand only**: when their topic becomes
  relevant to the current conversation (e.g. load `project-dad-inheritance.md`
  when a conversation touches that topic).
- The `MEMORY.md` index in that folder lists all memory files and their topics.
- **Important:** this memory folder is a hidden path outside the Obsidian
  vault. It is not visible in Obsidian or in the wiki. The wiki article at
  `wiki/ai-os/system-design/claude/memory/_index.md` documents the convention only: the actual
  runtime files are at the hidden path above.

## What belongs in memory
Memory is for three things only. Everything else belongs in the wiki.
1. **Personal profile** - who Julian is, how he works, preferences that apply
   universally across all sessions. Lives in `user.md`.
2. **Behavioural corrections** - when Julian corrects an approach that should
   not be repeated in any future session. Lives in `feedback-[slug].md`.
3. **Hard rules with serious consequences** - where getting it wrong could cause
   real harm (legal, financial, relational). Justify briefly why memory is the
   right store rather than the wiki.

Do not save to memory: project context, research, task state, wiki content,
conversation summaries, anything that will only be relevant for the current
session. The wiki already holds most of this: read from it instead.

## Writing memory
- **Confirm before writing** any new memory file. State what you are proposing
  to save and which type, and wait for agreement before writing.
- The exception: correcting a clearly wrong behavioural pattern the user has
  just flagged. Still say what you are saving, but proceed without waiting.
- Memory types: **user**, **feedback**. (Project states live in the wiki.)
  See `wiki/ai-os/system-design/claude/memory/_index.md` for the full convention.
- After writing, create or update the wiki mirror at
  `wiki/ai-os/system-design/claude/memory/[filename].md`.

## Format for feedback memory
Create `~/.claude/projects/-Users-julianhart-Obsidian-Vault/memory/feedback-[short-slug].md`
with frontmatter (`name`, `description`, `type: feedback`, `created`) and a
brief body covering: what the correction was, why it matters, how to apply it.
Then append a row to `MEMORY.md`.

- Do not duplicate `AGENTS.md` or `CLAUDE.md` rules in memory files. Memory is for
  session-learned content; `AGENTS.md` and `CLAUDE.md` are the permanent rulebook.

---

# AI OS - Skills Rule

**All Claude Code skills are documented in `wiki/ai-os/skills/`, no exceptions.**

This applies even if a skill is tightly coupled to a single domain (e.g. a
finance skill, a career skill). The skill documentation always lives in AI OS.
Workstream indexes (career, finance, etc.) cross-link to relevant skills under
a "Tools" section but do not host skill documentation.

Why: skills are infrastructure, not content. A single canonical location makes
them auditable and mirrors the operational reality at `~/.claude/skills/`.

## Skill Wiki Convention
- Every skill has a subfolder: `wiki/ai-os/skills/[skill-name]/`
- Each subfolder contains `SKILL.md`, an **exact copy** of the operational skill file at `~/.claude/skills/[skill-name]/SKILL.md`
- Every other file and subfolder inside `~/.claude/skills/[name]/` is also mirrored at the same relative path under `wiki/ai-os/skills/[name]/`. This includes `references/`, `evals/`, `TESTING.md`, and any other files a skill may contain: mirror the full folder structure, not just SKILL.md.

## Hidden File Mirroring Rule

This is Claude's instance of the universal **Hidden File Visibility** rule in
`AGENTS.md` (which all agents follow). The general principle, exact-copy, update
immediately, confirm to the user, never mirror secrets, lives there. Below are
Claude's specific source paths and mappings.

Skill files (`~/.claude/skills/`) and memory files
(`~/.claude/projects/.../memory/`) live at hidden paths outside Obsidian.
The user cannot see them. **Every hidden file must have an exact mirror
in the wiki:**

| Source | Wiki mirror |
|--------|------------|
| `~/.claude/skills/[name]/**/*` (all files, all subfolders) | `wiki/ai-os/skills/[name]/` (same relative path) |
| `~/.claude/skills/skill-conventions.md` | `wiki/ai-os/system-design/claude/skill-conventions.md` |
| `~/.claude/projects/.../memory/*.md` | `wiki/ai-os/system-design/claude/memory/[filename].md` |

**Enforcement:**
- After modifying ANY hidden file, immediately update its wiki mirror.
  Copy the full content, do not summarise or adapt.
- Mirror filenames must exactly match the source filename (e.g.
  `SKILL.md` stays uppercase, `user.md` stays lowercase).
- After creating a new skill or memory file, create the wiki mirror in
  the same operation.
- After completing any skill or memory modification, check the sync
  checklist at `wiki/ai-os/system-design/claude/hidden-file-sync.md` and update
  the "Last synced" date for each file touched.
- **Confirm to the user explicitly.** After updating any wiki mirror,
  send a message confirming which wiki file was updated and which
  hidden source file it mirrors. The user cannot see the hidden files:
  this confirmation is how they know the change is visible.
- This is non-negotiable. If you modify a hidden file and do not update
  its mirror, the user loses visibility of a file they cannot access.
- Python scripts are documented as `.md` files with embedded code blocks, never stored as `.py` in the wiki
- Full conventions: `~/.claude/skills/skill-conventions.md`, read this before creating a new skill

## Skills Documented
- **wiki/ai-os/skills/project-planner/** - Project definition via structured interview; WSJF scoring at project level; writes to wiki/projects/
- **wiki/ai-os/skills/define-user-story/** - User story definition; story statement, acceptance criteria, DoD, sizing; writes to wiki/deliverables/
- **wiki/ai-os/skills/define-enabler/** - Enabler definition (Exploration/Architecture/Infrastructure/Compliance); success criteria, sizing; writes to wiki/deliverables/
- **wiki/ai-os/skills/define-task/** - Generic deliverable definition (anything that isn't a story or enabler); completion criteria, sizing; same admission gates; writes to wiki/deliverables/
- **wiki/ai-os/skills/linkedin-enrichment/** - Step 2 of the lead enrichment pipeline. RapidAPI Fresh LinkedIn Scraper + Claude Haiku summarisation to Google Sheets.
- **wiki/ai-os/skills/apollo-person-match/** - Step 1 of the lead enrichment pipeline. Name + email to LinkedIn URL via Apollo.
- **wiki/ai-os/skills/llm-council/** - Multi-advisor decision council. 5 parallel sub-agents (Contrarian, First Principles, Expansionist, Outsider, Executor) + peer review + chairman synthesis. Triggers: "council this", "pressure-test this", "war room this", "stress-test this".
- **wiki/ai-os/skills/notebooklm-py/** - Automate Google NotebookLM via the unofficial `notebooklm-py` Python package. Creates notebooks, ingests wiki content as sources, generates flashcards, quizzes, podcasts, mind maps, and reports. Primary use case: Personal MBA wiki topic to flashcard deck. Triggers: `/notebooklm`, "make flashcards from [topic]", "create a notebook about [topic]", "quiz me on [topic]".
- **wiki/ai-os/skills/commitment-guard/** - Instruction-only (no scripts). Defends decisions Julian has LOCKED against emotional U-turns and enforces the lock checklist at commit. Triggers on *reopening* a committed decision (not the word "decision"). Implements the F-N-M-T reopen test + 48h stand-down from `wiki/performance/decisions/commitment-lock-protocol.md`. Paired with the `feedback-decision-reopening` memory.
- **wiki/ai-os/skills/decision-visualisation-check/** - Instruction-only (no scripts). Fires when Julian evaluates life, career, or relationship decision options by feel ("I like the idea of...", "I'm warming to..."). Asks for both the pleasant AND bad-day mental image before an incomplete frame biases the decision. Paired with the `feedback-visual-representation-bias` memory and [[visual-representation-bias]] article.

## Shared Infrastructure
- `credentials.py` - shared credential manager, copied into every skill's `scripts/` directory
- `gsheets_store.py` - shared Google Sheets layer, copied into every skill's `scripts/` directory
- `~/.leadgen/credentials.json` - API keys store (chmod 600). Keys: `RAPIDAPI_KEY`, `ANTHROPIC_API_KEY`, `APOLLO_API_KEY`, `GOOGLE_SERVICE_ACCOUNT_JSON`, `SHEETS_AUTH_METHOD`

## Environment Notes (Hong Kong)
- Anthropic API (160.79.104.0/21) requires VPN, blocked in HK
- RapidAPI must bypass VPN, VPN exit IPs are blocked by RapidAPI
- ExpressVPN configured with reverse bypass: all traffic through VPN except IPs outside 160.79.104.0/21
