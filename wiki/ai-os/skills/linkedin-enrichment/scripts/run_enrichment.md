# run_enrichment.py — Orchestration Script

tags: [technical, skills, linkedin, python]

> *Entry point for the LinkedIn enrichment pipeline. Reads CLI args, loads credentials, initialises components, and dispatches work to `linkedin_enricher.py` and `gsheets_store.py`.*

---

## Responsibilities

- Parse CLI arguments (`--sheet-id`, `--mode`, `--batch-size`, `--provider`)
- Call `CredentialManager.load()` to inject credentials into `os.environ`
- Initialise `GSheetsLeadStore` and `LinkedInEnricher`
- Dispatch to profile enrichment, posts enrichment, stats, or reset-failed modes
- Extract LinkedIn username from `linkedin_url` internally via regex — no separate column or conversion step needed

---

## Usage

```bash
# Enrich both profiles and posts (most common)
python scripts/run_enrichment.py \
  --sheet-id "YOUR_SHEET_ID" \
  --worksheet "Sheet1" \
  --batch-size 2 \
  --provider anthropic \
  --mode both

# Profile summaries only
python scripts/run_enrichment.py --sheet-id "YOUR_SHEET_ID" --mode profile

# Posts summaries only
python scripts/run_enrichment.py --sheet-id "YOUR_SHEET_ID" --mode posts

# Check pipeline progress
python scripts/run_enrichment.py --sheet-id "YOUR_SHEET_ID" --mode stats

# Reset failed rows for retry
python scripts/run_enrichment.py --sheet-id "YOUR_SHEET_ID" --mode reset-failed
```

---

## Source

```python
"""LinkedIn enrichment pipeline — end-to-end orchestration script.

Reads pending rows from a Google Sheet, enriches each lead via the LinkedIn
Data API and an LLM summarizer, and writes results back to the same sheet.

All dependencies are local to this skill's scripts/ directory.

Usage:
  python scripts/run_enrichment.py \
    --sheet-id "YOUR_SHEET_ID" \
    --worksheet "Sheet1" \
    --batch-size 2 \
    --provider anthropic \
    --mode both

Modes:
  profile       — enrich LinkedIn profiles only
  posts         — enrich LinkedIn posts only
  both          — profile then posts (default)
  stats         — print status counts per column
  reset-failed  — reset failed rows back to pending for retry
"""
import os, sys, re, time, argparse

# Local imports — all files live in the same scripts/ directory
sys.path.insert(0, os.path.dirname(os.path.abspath(__file__)))
from credentials import CredentialManager
from gsheets_store import GSheetsLeadStore
from linkedin_enricher import LinkedInEnricher

# Ensure all required keys are present — prompts on first run, silent thereafter
CredentialManager.load(required=[
    "RAPIDAPI_KEY",
    "ANTHROPIC_API_KEY",
    "SHEETS_AUTH_METHOD",
])


def extract_username(url: str) -> str:
    """Extract LinkedIn username from URL — regex, no LLM needed."""
    if not url:
        return ""
    match = re.search(r'linkedin\.com/in/([^/?#]+)', url)
    return match.group(1).strip('/') if match else ""


def enrich_profiles(store: GSheetsLeadStore, provider: str, batch_size: int):
    """Enrich LinkedIn profiles for rows where about_linkedin_profile is empty."""
    enricher = LinkedInEnricher(llm_provider=provider)
    pending  = store.get_pending(empty_col="about_linkedin_profile", limit=batch_size)

    if not pending:
        print("No rows pending profile enrichment.")
        return

    updates = []
    for row in pending:
        url      = str(row.get("linkedin_url", "")).strip()
        username = extract_username(url)
        if not username:
            print(f"  Row {row['_row_index']}: linkedin_url missing or "
                  f"unparseable — skipping", file=sys.stderr)
            continue

        print(f"  Enriching profile: {username} ({row.get('name', '')})",
              file=sys.stderr)
        result = enricher.enrich_profile(username)
        updates.append({"row_index": row["_row_index"], "data": result})
        time.sleep(2)

    if updates:
        print(f"\nWriting {len(updates)} profile enrichments to sheet...")
        store.update_batch(updates)
    print("Profile enrichment done.")


def enrich_posts(store: GSheetsLeadStore, provider: str, batch_size: int):
    """Enrich LinkedIn posts for rows where recent_posts_summary is empty."""
    enricher = LinkedInEnricher(llm_provider=provider)
    pending  = store.get_pending(empty_col="recent_posts_summary", limit=batch_size)

    if not pending:
        print("No rows pending posts enrichment.")
        return

    updates = []
    for row in pending:
        url      = str(row.get("linkedin_url", "")).strip()
        username = extract_username(url)
        if not username:
            print(f"  Row {row['_row_index']}: linkedin_url missing or "
                  f"unparseable — skipping posts", file=sys.stderr)
            continue

        print(f"  Fetching posts: {username} ({row.get('name', '')})",
              file=sys.stderr)
        result = enricher.enrich_posts(username)
        updates.append({"row_index": row["_row_index"], "data": result})
        time.sleep(2)

    if updates:
        print(f"\nWriting {len(updates)} post enrichments to sheet...")
        store.update_batch(updates)
    print("Posts enrichment done.")


if __name__ == "__main__":
    parser = argparse.ArgumentParser(
        description="LinkedIn enrichment pipeline"
    )
    parser.add_argument("--sheet-id",   required=True,
                        help="Google Sheet ID from the URL")
    parser.add_argument("--worksheet",  default="Sheet1",
                        help="Tab/worksheet name")
    parser.add_argument("--batch-size", type=int, default=2,
                        help="Rows per run — keep low to respect API rate limits")
    parser.add_argument("--provider",   default="anthropic",
                        choices=["anthropic", "openai", "ollama"],
                        help="LLM provider for summarization")
    parser.add_argument("--mode",       default="both",
                        choices=["profile", "posts", "both",
                                 "reset-failed", "stats"],
                        help="Which step to run")
    args = parser.parse_args()

    store = GSheetsLeadStore(
        sheet_id=args.sheet_id,
        worksheet_name=args.worksheet
    )

    if args.mode == "stats":
        import pprint
        pprint.pprint(store.stats())

    elif args.mode == "reset-failed":
        store.reset_failed("profile_summary_scrape", "failed",    "pending")
        store.reset_failed("posts_scrape_status",    "failed",    "unscraped")
        store.reset_failed("posts_scrape_status",    "unscraped", "pending")
        print("Reset complete.")

    elif args.mode == "profile":
        enrich_profiles(store, args.provider, args.batch_size)

    elif args.mode == "posts":
        enrich_posts(store, args.provider, args.batch_size)

    elif args.mode == "both":
        enrich_profiles(store, args.provider, args.batch_size)
        enrich_posts(store, args.provider, args.batch_size)
```

---

## Notes

- `batch-size` should be kept low (2–5). Each row costs 4 RapidAPI credits and 2 LLM calls.
- Username is always extracted from `linkedin_url` via regex — no `linkedin_username` column needed in the sheet.
- `time.sleep(2)` between rows respects RapidAPI rate limits.
- Partial progress is saved to the sheet after each row — safe to interrupt and resume.
