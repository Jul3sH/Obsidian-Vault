> Mirror copy. Source: `~/.claude/projects/-Users-julianhart-Obsidian-Vault/memory/feedback-taxonomy-before-filing.md`

---
name: taxonomy-before-filing
description: Read wiki/ai-os/taxonomy.md and the destination index's filing test BEFORE proposing any file location or structural change; before restructuring, check whether the existing structure is failing or merely forgotten
type: feedback
created: 2026-09-22
---

# Taxonomy Before Filing

**What the correction was:** On 21-22 Sep 2026, Claude proposed homes for a new
ai-os file (first `wiki/performance/`, then `system-design/generic/`) without
reading `wiki/ai-os/taxonomy.md` or the destination `_index` filing tests, both
of which already answered the question (service-design, by the people/process
test and the when-in-doubt default). Julian's own memory of the taxonomy had
faded, so with no backstop from Claude he came close to collapsing the working
service-design/system-design split entirely.

**Why it matters:** The filing rules only protect the structure if they are read
at proposal time. The AGENTS.md rule ("read the destination index's What belongs
here test before proposing a location") already existed and was skipped
silently. When Claude skips it, Julian's fading memory of his own prior design
has no backstop, and an adopted, working system nearly gets restructured because
it was forgotten, not because it failed.

**How to apply:**
- Before proposing a location for any new wiki file, read the destination
  index's filing test (the existing AGENTS.md rule - follow it, every time).
- For anything under `wiki/ai-os/`, read `wiki/ai-os/taxonomy.md` first,
  including Gate 0 (is this AI OS at all?).
- When Julian proposes restructuring folders, categories, or systems, read
  `taxonomy.md` and the [[systems-register]] before engaging with the redesign,
  and ask: is the existing structure failing, or merely forgotten? Restructure
  energy with no failure evidence is [[mm-build-dont-adopt-bias]] firing - raise
  the card.
