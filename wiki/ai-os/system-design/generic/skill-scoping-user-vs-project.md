---
type: reference
created: 2026-07-25
tags: [ai-os, system-design, skills, claude-code, portability]
---

# Skill Scoping: User-Level vs. Project-Level

> *Where a skill lives — the machine's home directory or inside a repo — decides its portability, versioning, and scope. Open this when deciding where to install a new skill, or comparing how ClaudeClaw and agentic-os handle skills.*

Claude Code loads skills from two places. The choice between them is an architecture decision, not a detail. Verified against both repos on 2026-07-25.

---

## The two locations

- **User-level** — `~/.claude/skills/`. Lives in the machine's home directory. Shared across every project and every Claude Code surface (terminal, ClaudeClaw) on that machine.
- **Project-level** — `<repo>/.claude/skills/`. Lives inside a repo. Only active when working within that repo.

---

## How the two systems chose

| | ClaudeClaw | agentic-os |
|---|---|---|
| **Primary scope** | User-level (`~/.claude/skills/`) | Project-level (`<repo>/.claude/skills/`) |
| **Evidence** | Agent config: "All global Claude Code skills (`~/.claude/skills/`) are available"; 25 skills in `~/.claude/skills/` | 27 skills in `agentic-os/.claude/skills/`, domain-prefixed (`fin-`, `mkt-`, `meta-`, `str-`, `tool-`) |
| **Also has** | A thin project-level layer for repo upkeep (`add-migration`) | — |
| **Why** | It's a **thin bridge** — it should expose whatever toolkit the machine already has, so phone = terminal | It's a **self-contained OS** — the repo *is* the system; skills must travel and version with it |

---

## What "travel with the repo, not the machine" means

**Project-level skills are files inside the git repo**, so they inherit git:

- **Versioned** — committed to history; diffable, revertable.
- **Cloneable** — `git clone` on any machine brings them with the code.
- **Team-syncable** — `push`/`pull` distributes them; a teammate cloning the repo gets all skills instantly.
- **Move-with-the-folder** — copy the repo to another box and the skills are already inside it.

The skill set is a property of **the repo**. Wherever the repo goes, the skills go.

**User-level skills live in `~/.claude/skills/`**, a property of **the machine's account**:

- Not in any repo (unless dotfiles are separately versioned).
- A clone of the project on a fresh machine brings **none** of them.
- A teammate cloning the repo gets **zero** of them.
- Available in every project — but only on that one machine, reinstalled per machine.

**Concrete test — new laptop or a colleague joins:**
- *Project-level:* `git clone` → all skills work immediately, zero setup.
- *User-level:* the home-dir skills are invisible until manually reinstalled on the new machine.

---

## Trade-offs

| Dimension | User-level | Project-level |
|---|---|---|
| Availability | Every project on the machine | Only inside the repo |
| Portability | Machine-bound | Travels via git clone |
| Versioning | Not tied to a project's history | Versioned in the repo |
| Team sharing | Manual copy per machine | Automatic via the repo |
| Namespace | Flat/global (collision risk) | Repo-scoped; often domain-prefixed |
| Isolation | None — every project sees the same pile | Natural — a client repo sees only its own |
| Duplication | Write once, use everywhere | May duplicate across repos |

**One line:** project-level = portable and versioned but per-repo; user-level = write-once-use-everywhere but machine-bound and reinstalled per machine.

---

## Practical consequence (this setup)

- Planning/career skills (`define-user-story`, `goal-planner`, `jira-sync`, `morning`, `project-planner`, ...) are **user-level** → identical from Telegram and terminal.
- agentic-os domain skills (`fin-`/`mkt-`/`meta-`) are **repo-scoped** → only fire inside that repo; ClaudeClaw on the phone can't see them unless in that project context.
- To make a repo-scoped skill available everywhere, symlink it into `~/.claude/skills/`, or accept it stays repo-bound.

---

## See Also
- [[pointer-vs-copy|Pointer vs. Copy]] — the same own-it-locally instinct applied to knowledge
- [[skill-conventions|Skill Conventions]] — how skills are structured
- [[claudeclaw-business-os-overview|ClaudeClaw Business OS Overview]]
