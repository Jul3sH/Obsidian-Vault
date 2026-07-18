# LinkedIn Enrichment — Architecture

tags: [technical, skills, linkedin, architecture]

---

## Pipeline Flow

```
Google Sheets (pending rows)
        │
        ▼
run_enrichment.py          ← orchestrator; reads args, calls components
        │
        ├─── credentials.py ────► ~/.leadgen/credentials.json
        │    (CredentialManager.load)       (RAPIDAPI_KEY, ANTHROPIC_API_KEY,
        │                                    GOOGLE_SERVICE_ACCOUNT_JSON)
        │
        ├─── gsheets_store.py ──► sheets.googleapis.com (HTTPS · direct)
        │    (GSheetsLeadStore)             reads pending rows by checking
        │                                   empty columns (e.g. about_linkedin_profile)
        │
        └─── linkedin_enricher.py
                │
                ├─► RapidAPI (HTTPS · direct · bypasses VPN)
                │   fresh-linkedin-scraper-api.p.rapidapi.com
                │   GET /api/v1/user/profile   param: username  (1 request)
                │   GET /api/v1/user/experience param: urn      (1 request)
                │   GET /api/v1/user/educations param: urn      (1 request)
                │   GET /api/v1/user/posts      param: urn      (1 request)
                │                                               ──────────
                │                                               4 requests/lead
                │
                │   Note: urn is extracted from the /profile response.
                │   /profile must be called first. All costs confirmed
                │   via "cost": 1 in API response body (2026-05-07).
                │
                └─► Anthropic API (HTTPS · via VPN · 160.79.104.0/21)
                    api.anthropic.com/v1/messages
                    POST (profile summary prompt)   claude-haiku-4-5
                    POST (posts summary prompt)     claude-haiku-4-5

        │
        ▼
gsheets_store.py ──────────► sheets.googleapis.com (HTTPS · direct)
(update_batch)                writes: about_linkedin_profile,
                              recent_posts_summary, education_history,
                              profile_summary_scrape, posts_scrape_status
```

---

## Component Responsibilities

| Component | Responsibility | Credentials used |
|-----------|---------------|-----------------|
| `run_enrichment.py` | Orchestration — CLI args, calls all components in sequence | None directly |
| `credentials.py` | Load `~/.leadgen/credentials.json` into `os.environ` at startup | Reads the file |
| `gsheets_store.py` | Read pending rows; write enriched results back | `GOOGLE_SERVICE_ACCOUNT_JSON` |
| `linkedin_enricher.py` | Fetch LinkedIn data; call LLM; return structured results | `RAPIDAPI_KEY`, `ANTHROPIC_API_KEY` |

---

## Data Flow — Columns

**Input columns read from sheet:**
- `linkedin_url` — source for all API lookups; username extracted internally via regex
- `name` — used in log output only

**Output columns written to sheet:**
| Column | Source | Values |
|--------|--------|--------|
| `about_linkedin_profile` | LLM (Haiku) | 2-3 paragraph profile summary |
| `profile_summary_scrape` | linkedin_enricher.py | `completed` / `failed` |
| `education_history` | RapidAPI /educations | JSON array of school/degree/years |
| `recent_posts_summary` | LLM (Haiku) | 2-paragraph posts narrative |
| `posts_scrape_status` | linkedin_enricher.py | `scraped` / `failed` |

> Note: `linkedin_username` and `extract_username_status` columns are not used. Username is extracted from `linkedin_url` inside `run_enrichment.py` — no sheet column or separate conversion step needed.

---

## VPN Routing

| API call | Route | Reason |
|----------|-------|--------|
| RapidAPI (LinkedIn data) | Direct — bypasses VPN | VPN exit node IPs blocked by RapidAPI |
| Anthropic API (Haiku) | Through VPN | Anthropic IP range blocked in Hong Kong |
| Google Sheets API | Direct — bypasses VPN | Google tolerates direct HK traffic |

ExpressVPN configured with reverse bypass rule: all traffic routes through VPN *except* IPs outside `160.79.104.0/21`. Only Anthropic traffic goes through the tunnel.

---

## Run Modes

| Mode | What it does |
|------|-------------|
| `both` (default) | Profile enrichment then posts enrichment |
| `profile` | Profile, experience, education + LLM summary only |
| `posts` | Posts fetch + LLM summary only |
| `stats` | Print status counts per status column |
| `reset-failed` | Reset `failed` rows back to pending for retry |

---

## Error Handling

| Scenario | Behaviour |
|----------|-----------|
| `linkedin_url` missing or unparseable | Row skipped with warning |
| RapidAPI 429 (rate limit) | Sleep 30s, retry once |
| Profile not in Fresh LinkedIn Scraper index | 400/403 error → status `failed` |
| Empty posts array | `posts_scrape_status = failed` (user doesn't post) |
| LLM timeout or API error | Status set to `failed`; retry with `--mode reset-failed` |
| Missing sheet columns | Auto-added on first run |

---

## See Also

- [[technology/linkedin-enrichment/TESTING|Testing Log]] — isolation tests and blockers from initial build
- [[technology/api-skill-troubleshooting|API Skill Troubleshooting]] — environment gotchas and pre-flight checklist
