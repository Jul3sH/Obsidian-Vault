Strictly speaking, I don't think it's actually a skill. # Skill Conventions — API-Based Skills

tags: [technical, skills, conventions, architecture]

> *Standard structure and documentation conventions for all API-based Claude skills. Load this as context whenever building or documenting a new skill.*

---

## Key Takeaways

- Every skill has a matching wiki article under `wiki/ai-os/skills/[skill-name]/`
- Python scripts are documented as Markdown files with embedded code blocks — not stored as `.py` in the wiki
- All skills share the same `credentials.py` and `gsheets_store.py` — copy, don't import across skills
- The LLM model must be hardcoded in the script — never rely on a default
- Run the pre-flight checklist before any debugging session

---

## Skill Directory Structure (Runtime)

Skills live in Claude's local agent session storage. The canonical location is:

```
~/Library/Application Support/Claude/local-agent-mode-sessions/skills-plugin/
  [session-id]/[agent-id]/skills/
    [skill-name]/
      SKILL.md              ← Claude-facing description and trigger phrases
      references/
        column-mapping.md   ← Google Sheet column reference
        TESTING.md          ← testing log for this skill (what/why)
        gcloud-setup.md     ← Google Sheets auth setup (if needed)
        llm-providers.md    ← LLM options and costs (if LLM used)
      scripts/
        run_[skill].py      ← entry point / orchestrator
        [skill]_[action].py ← core logic (API calls, LLM)
        gsheets_store.py    ← Google Sheets I/O (shared copy)
        credentials.py      ← credential manager (shared copy)
```

---

## Wiki Documentation Structure

Every skill has a matching entry in `wiki/ai-os/skills/`. The wiki mirrors the full folder structure of the source skill — not just SKILL.md. Every file and subfolder under `~/.claude/skills/[name]/` is reproduced at the same relative path under `wiki/ai-os/skills/[name]/`.

```
~/.claude/skills/[skill-name]/     →    wiki/ai-os/skills/[skill-name]/
  SKILL.md                               SKILL.md  (exact copy)
  references/                            references/
    section0-mapping.md                    section0-mapping.md  (exact copy)
    ...                                    ...
  evals/                                 evals/
    ...                                    ...
  TESTING.md                             TESTING.md  (exact copy)
  scripts/                               scripts/
    run_[skill].py                         run_[skill].md  (code in fenced block + notes)
    ...                                    ...
```

Mirror rules:
- **Exact copy** for all Markdown files — copy full content, add a mirror header at the top (source path + "do not edit here").
- **Python scripts** are documented as `.md` files with the source embedded in a fenced code block plus annotations — never stored as `.py` in the wiki.
- Mirror filenames must match the source exactly (case-sensitive).
- When a new file or subfolder is added to a skill, mirror it immediately in the same operation.
- Update `wiki/ai-os/system-design/hidden-file-sync.md` for every file added or changed.

### Why this structure?
- The runtime location is tied to a Claude session ID and may not persist
- The wiki is a stable, searchable reference that survives session changes
- Full folder mirroring means nothing is invisible — the user can audit the complete skill from Obsidian
- Embedding code in Markdown (with code blocks) allows annotation alongside the code

---

## Shared Files — Handle With Care

These two files are identical copies in every skill's `scripts/` directory:

| File | Purpose | Rule |
|------|---------|------|
| `credentials.py` | Load `~/.leadgen/credentials.json` into `os.environ` | If you update one copy, update all copies |
| `gsheets_store.py` | Google Sheets read/write | If you update one copy, update all copies |

Skills are intentionally self-contained (no cross-skill imports). This is a deliberate trade-off: duplication over coupling.

---

## Credential Conventions

- All API keys stored in `~/.leadgen/credentials.json` (chmod 600)
- Every script calls `CredentialManager.load(required=[...])` as its first action
- Keys required per skill:

| Skill | Keys required |
|-------|--------------|
| apollo-person-match | `APOLLO_API_KEY`, `SHEETS_AUTH_METHOD` |
| linkedin-enrichment | `RAPIDAPI_KEY`, `ANTHROPIC_API_KEY`, `SHEETS_AUTH_METHOD` |

- **Never log, print, or paste API key values.** If exposed, rotate immediately.

---

## LLM Model Convention

- **Always hardcode the model name** in the script — never rely on a provider default
- Current standard: `claude-haiku-4-5-20251001` for data orchestration tasks (no reasoning needed)
- Use Sonnet only if the task requires genuine reasoning, analysis, or complex decision-making
- The model name goes in the `_call_anthropic()` function, not in the calling code

```python
payload = json.dumps({
    "model": "claude-haiku-4-5-20251001",  # hardcoded — do not change without testing cost
    "max_tokens": 512,
    ...
})
```

---

## Testing Convention

Every skill must have a `TESTING.md` in its `references/` folder documenting:
- **What** each test isolated
- **Why** that test was needed
- **What** it revealed
- The pre-flight checklist for future debugging

The generic isolation testing methodology lives in [[../service-design/api-skill-troubleshooting|API Skill Troubleshooting]]. The skill-level `TESTING.md` is skill-specific.

### Pre-Flight Checklist (run before any debugging)

| # | Check | Catches |
|---|-------|---------|
| 1 | `~/.leadgen/credentials.json` has all required keys | Missing keys |
| 2 | Billing/quota checked on every paid API | Zero credits, quota exceeded |
| 3 | curl each external API independently | Auth failures, network blocks |
| 4 | Test with known-good data | Data coverage gaps |
| 5 | VPN routing confirmed for each API | VPN IP blocks |
| 6 | Full end-to-end run | Integration failures |

---

## VPN Routing (Julian's Environment — Hong Kong)

| API | Route | Reason |
|-----|-------|--------|
| Anthropic API | Through VPN | HK network block on 160.79.104.0/21 |
| RapidAPI | Direct | VPN exit IPs blocked by RapidAPI |
| Google Sheets | Direct | Google tolerates HK direct |
| Apollo API | Direct (assumed) | Verify on first use |

ExpressVPN bypass rule: all traffic through VPN *except* IPs outside `160.79.104.0/21`.

---

## CLAUDE.md Entry for New Skills

When creating a new skill, add a matching section to the Obsidian `CLAUDE.md` so future sessions know where the documentation lives. See the `# Skill Documentation` section in the root `CLAUDE.md`.
