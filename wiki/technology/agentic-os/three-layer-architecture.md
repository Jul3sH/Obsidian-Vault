---
type: reference
updated: 2026-07-28
---

# Three-Layer Architecture

Agentic OS is built on three interdependent layers that work together to turn Claude Code into a team member instead of a chatbot.

## Overview

```
Layer 1: Agent Identity
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
• SOUL.md (who you are, core truths)
• USER.md (who you're helping)
• Semantic memory (sessions, learnings)
• Persistent context across sessions

Layer 2: Skills System
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
• Modular, self-improving capabilities
• Core skills (always installed)
• Optional skills (add/remove as needed)
• Skill dependencies auto-resolved
• Each skill has tested methodology

Layer 3: Brand Context
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
• Voice profile (tone, values, language)
• Positioning (unique angles, value props)
• ICP (ideal customer profile, messaging)
• Visual identity (typography, colors, tone)
• Skills load only what they need
• Output stays on-brand automatically
```

## Layer 1: Agent Identity

**Purpose:** Makes the agent feel like a team member who knows your business and learns from you over time.

### SOUL.md — Who You Are

Core truths and behaviour rules that define the agent's personality:

- **Be genuinely helpful, not performatively helpful** — no "great question!" filler
- **Have opinions** — recommend with reasoning, not menus
- **Be resourceful** — check context first, ask if stuck
- **Anticipate needs** — flag gaps and opportunities
- **Own mistakes** — say so and fix it, don't hedge
- **Work across domains** — not limited to one skill area

**File location:** `context/SOUL.md`

### USER.md — Who You're Helping

Profile of the person/business being served:

- Name, business, role, website, location
- Communication style, preferred output format
- Working style preferences
- Notes and preferences

**File location:** `context/USER.md` (auto-populated by `/start-here` on first run)

### Semantic Memory

Persistent long-term memory across sessions:

- **Session capture** — end-of-session summaries automatically indexed
- **Learnings** — `context/learnings.md` tracks what the agent has learned
- **Decision log** — `context/MEMORY.md` (top-level decisions, locked choices)
- **Searchable recall** — `npm run memory:recall` retrieves past sessions, decisions, learnings

**See:** [[agentic-os/memory-system-architecture|Memory System Architecture]]

## Layer 2: Skills System

**Purpose:** Modular, self-improving capabilities that follow tested methodologies and improve as the user gives feedback.

### Core Skills (Always Installed)

| Skill | Purpose |
|-------|---------|
| **meta-skill-creator** | Build custom skills for your business |
| **meta-wrap-up** | End-of-session capture and memory indexing |
| **mkt-brand-voice** | Extract or build your brand voice |
| **mkt-positioning** | Find angles that differentiate your offer |
| **mkt-icp** | Define ideal customer and messaging |

### Optional Skills (Add/Remove as Needed)

**Content & Marketing:**
- `mkt-copywriting` — sales copy with 7-dimension scoring
- `mkt-content-repurposing` — turn one piece into 8 platforms
- `str-ai-seo` — optimize for AI search engines

**Visual & Design:**
- `viz-excalidraw-diagram` — architecture and workflow diagrams
- `viz-image-gen` — interactive visual direction + image generation
- `viz-interface-design` — design dashboards and SaaS UIs

**Tools & Utilities:**
- `tool-humanizer` — strip AI patterns from output
- `tool-firecrawl-scraper` — scrape JS-heavy websites
- `ops-cron` — schedule recurring Claude Code tasks

### How Skills Work

**Structure:** Each skill is in `.claude/skills/{skill-name}/`
- `SKILL.md` — methodology documentation, triggers, use cases
- `SKILL.local.md` — personal customizations (auto-preserved during updates)
- `scripts/` — helper scripts if needed

**Installation:**
```bash
bash scripts/add-skill.sh mkt-copywriting    # skill + dependencies
bash scripts/remove-skill.sh viz-image-gen   # remove
bash scripts/list-skills.sh                  # see installed & available
```

**Self-improvement:** Corrections go directly into the skill, not a note. Over time, skills get sharper with feedback.

## Layer 3: Brand Context

**Purpose:** Ensures every output stays on-brand without extra prompt engineering.

### Brand Context Files

- **Voice Profile** — Tone, language, key phrases, examples
- **Positioning** — Unique angles, value propositions, messaging pillars
- **ICP** — Ideal customer profile, pain points, language they use
- **Visual Identity** — Typography, color palette, layout patterns, brand assets

### How Skills Use Brand Context

Skills load only what they need:
- Copy skill loads voice + positioning + ICP
- Design skill loads visual identity + voice
- SEO skill loads positioning + messaging

This keeps the prompt focused. The `/start-here` onboarding populates brand context on first run.

## How Layers Integrate

1. **Identity** → Agent personality learned from SOUL.md and USER.md
2. **Session memory** → Agent recalls past decisions and learnings
3. **Skills** → Methods to accomplish work (each skill is a tested approach)
4. **Brand context** → Skills automatically output on-brand

**Example flow:**
```
User asks: "Write a product description for our new tool"
  ↓
Skill: mkt-copywriting activates
  ↓
Loads: voice profile + positioning + ICP
  ↓
Uses: tested 7-dimension scoring methodology
  ↓
Output: on-brand, tailored to ideal customer, structured for scoring
```

## Session Continuity

Each session:

1. **Wake up fresh** — no built-in memory; you are what's in `context/`
2. **Read identity files** — SOUL.md, USER.md, learnings.md
3. **Search memory if needed** — `npm run memory:recall` for past sessions
4. **Improve with feedback** — corrections go into skill files or learnings.md

The more sessions run, the sharper the agent gets.

## Related Documentation

- [[agentic-os/memory-system-architecture|Memory System Architecture]] — how session memory works
- [[agentic-os/multi-client-architecture|Multi-Client Architecture]] — running multiple clients with different identities
