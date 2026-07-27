---
type: reference
updated: 2026-07-28
---

# Multi-Client Architecture

Agentic OS supports running multiple isolated clients from a single installation. Each client has its own context, brand data, memory, projects, and preferences — all scoped to prevent cross-client leakage.

## How Multi-Client Works

**Single install, multiple workspaces:**

```
agentic-os/
├── context/              (root/shared)
├── brand_context/        (root/shared)
├── .claude/
│   ├── skills/          (shared across all clients)
│   └── hooks/           (shared)
│
└── clients/
    ├── acme/            (client workspace)
    │   ├── context/     (client-specific)
    │   ├── brand_context/  (client brand)
    │   └── memory/      (client memory, scope='client')
    │
    └── beta-startup/    (another client)
        ├── context/
        ├── brand_context/
        └── memory/
```

## Folder Structure

### Root Workspace (`agentic-os/`)

**Shared across all clients:**
- `context/SOUL.md`, `USER.md` — global personality
- `context/learnings.md` — accumulated knowledge
- `context/memory/` — root-level memory (indexed as `system` scope)
- `brand_context/` — root brand (voice, positioning, ICP, visual identity)
- `.claude/skills/` — all skills (used by all clients)
- `.claude/hooks/` — shared hooks (session capture, wrap-up, etc.)
- `scripts/` — shared update, install, bootstrap scripts

### Client Workspace (`clients/{slug}/`)

**Isolated to that client:**
- `context/` — client-specific identity files (can override root)
- `brand_context/` — client-specific brand
- `projects/` — client-specific projects and deliverables
- `.env` — client-specific API keys and environment
- `memory/` — indexed as `visibility = 'client'`, `client_id = {slug}`

## Client-Scoped Memory

When indexing for a client:

```bash
npm run memory:index -- --visibility client --client acme
```

The indexer:
1. Discovers files under `clients/acme/context/memory/`
2. Re-scopes all rows to `visibility = 'client'`, `client_id = 'acme'`
3. Prevents accidental root-scope indexing

When searching for a client:

```bash
npm run memory:recall -- "what did we learn" --client acme
```

The search:
1. Filters by `(visibility = 'system' OR (visibility = 'client' AND client_id = 'acme'))`
2. Never returns other clients' memory
3. Always includes root `system` baseline (shared learnings)

## Isolation Guarantees

**Scope invariant (enforced in DB + application):**

Every memory row has this CHECK constraint. No-leak tests prove:
- Client A's search cannot return Client B's memory
- Search always includes system baseline (root memory)
- Scope filter is the only leak vector (code-review rule)

## Creating a Client

**Via Claude Code (recommended):**
```
/start-here --client <slug>
```

Creates `clients/{slug}/` and runs onboarding to populate brand context.

## Multi-Client Workflow

**Typical setup:**

1. **Root workspace** — One global SOUL.md (general personality), shared learnings, shared brand templates
2. **Per-client workspace** — Override SOUL.md if different personality, client-specific brand, client-specific projects and memory
3. **Skill customization** — Global skills, client-specific customizations via `SKILL.local.md`
4. **Context inheritance** — Root `context/learnings.md` loaded for all sessions, client-specific learnings loaded only for that client

## Updating with Multiple Clients

```bash
bash scripts/update.sh
```

Update flow:
1. Pulls from upstream
2. Backs up all client folders to `.backup/`
3. Syncs shared files (skills, hooks, scripts) to all clients
4. Preserves client-specific files (env, context, brand, projects)

If update conflicts detected, stops and asks per skill: keep yours or accept upstream.

## Client-Specific Env Vars

Each client can have different API keys:

```bash
# Root .env (shared)
ANTHROPIC_API_KEY=xxx

# Client .env (overrides root)
cat clients/acme/.env
FIRECRAWL_API_KEY=acme-specific-key
OPENAI_API_KEY=acme-specific-key
```

When Claude Code runs for a client, it loads root `.env` first, then client `.env` (overrides).

## Related Documentation

- [[agentic-os/memory-database-schema|Memory Database Schema]] — scope model and no-leak guarantees
- [[agentic-os/memory-system-architecture|Memory System Architecture]] — per-client memory isolation
