# gsheets_store.py — Google Sheets Read/Write Layer

tags: [technical, skills, linkedin, python, google-sheets]

> *Shared Google Sheets integration used by all pipeline skills. Handles authentication, column management, batch writes, and status tracking.*

---

## Responsibilities

- Authenticate to Google Sheets via service account JWT or OAuth
- Read all rows, return as list of dicts with `_row_index` metadata
- Find pending rows (where a given column is empty)
- Write enriched results back in batch
- Auto-create missing columns on first write
- Handle Google Sheets API 429 rate limits with exponential backoff

---

## Key Design Decisions

- **Shared across skills** — identical copy used by both `linkedin-enrichment` and `apollo-person-match`. If updated, update both.
- **`_row_index` injected** into each row dict so callers can write back to the correct row without re-reading the sheet.
- **`_ensure_columns()`** auto-adds missing columns — skills don't need to pre-create the sheet structure.
- **`ENRICHMENT_COLS` set** documents which columns this skill owns (used for filtering/awareness, not enforced).

---

## Source

```python
"""Google Sheets lead store — read/write for enrichment pipeline."""
import os, json, time, sys
from typing import Optional

try:
    import gspread
    from gspread.exceptions import APIError
except ImportError:
    print("gspread not installed. Run: pip install gspread", file=sys.stderr)
    raise

ENRICHMENT_COLS = {
    "linkedin_username", "about_linkedin_profile", "recent_posts_summary",
    "education_history", "profile_summary_scrape", "posts_scrape_status",
    "extract_username_status", "contacts_scrape_status", "apollo_match_status",
}

def _auth_client():
    """Return authenticated gspread client using stored auth method."""
    method = os.environ.get("SHEETS_AUTH_METHOD", "service_account")
    if method == "service_account":
        sa_path = os.environ.get("GOOGLE_SERVICE_ACCOUNT_JSON", "")
        if not sa_path or not os.path.exists(sa_path):
            raise ValueError(
                f"Service account file not found: {sa_path}\n"
                "Run the script again to re-enter credentials."
            )
        return gspread.service_account(filename=sa_path)
    return gspread.oauth()  # OAuth — gspread handles browser flow + token caching


class GSheetsLeadStore:
    def __init__(self, sheet_id: str, worksheet_name: str = "Sheet1"):
        self.sheet_id = sheet_id
        self.ws_name  = worksheet_name
        self._gc      = _auth_client()
        self._sh      = self._gc.open_by_key(sheet_id)
        self._ws      = self._sh.worksheet(worksheet_name)
        self._headers: list[str] = []
        self._refresh_headers()

    def _refresh_headers(self):
        row1          = self._ws.row_values(1)
        self._headers = [h.strip() for h in row1]

    def _ensure_columns(self, cols: list[str]):
        """Auto-add any missing columns to the sheet header row."""
        added = []
        for col in cols:
            if col not in self._headers:
                next_col = len(self._headers) + 1
                self._ws.update_cell(1, next_col, col)
                self._headers.append(col)
                added.append(col)
                time.sleep(0.5)
        if added:
            print(f"Added columns: {added}", file=sys.stderr)

    def _col_index(self, col_name: str) -> Optional[int]:
        try:
            return self._headers.index(col_name) + 1
        except ValueError:
            return None

    def get_all_rows(self) -> list[dict]:
        records = self._ws.get_all_records(default_blank="")
        for i, r in enumerate(records):
            r["_row_index"] = i + 2  # 1-indexed, row 1 is header
        return records

    def get_pending(self, empty_col: str, value: str = "",
                    limit: int = 10) -> list[dict]:
        """Return rows where empty_col is blank and linkedin_username or linkedin_url exists."""
        self._ensure_columns([empty_col])
        all_rows = self.get_all_rows()
        pending  = []
        for row in all_rows:
            val = str(row.get(empty_col, "")).strip()
            if val:
                continue
            username = str(row.get("linkedin_username", "")).strip()
            url      = str(row.get("linkedin_url", "")).strip()
            if not username and not url and empty_col not in ("apollo_match_status",):
                print(f"Row {row['_row_index']}: no linkedin_username or linkedin_url — skipping",
                      file=sys.stderr)
                continue
            pending.append(row)
            if len(pending) >= limit:
                break
        print(f"Found {len(pending)} pending rows (limit={limit})", file=sys.stderr)
        return pending

    def update_row(self, row_index: int, data: dict, retry: int = 3):
        """Write a dict of {column_name: value} to the given row."""
        self._ensure_columns(list(data.keys()))
        cells = []
        for col_name, value in data.items():
            col_idx = self._col_index(col_name)
            if col_idx is None:
                continue
            cells.append(gspread.Cell(
                row=row_index, col=col_idx,
                value=str(value) if value else ""
            ))
        if not cells:
            return
        for attempt in range(retry):
            try:
                self._ws.update_cells(cells, value_input_option="RAW")
                return
            except APIError as e:
                if "429" in str(e) and attempt < retry - 1:
                    wait = 2 ** attempt * 10
                    print(f"Rate limited. Waiting {wait}s...", file=sys.stderr)
                    time.sleep(wait)
                else:
                    raise

    def update_batch(self, updates: list[dict], sleep_between: float = 1.0):
        for i, upd in enumerate(updates):
            self.update_row(upd["row_index"], upd["data"])
            print(f"  [{i+1}/{len(updates)}] Updated row {upd['row_index']}", file=sys.stderr)
            if i < len(updates) - 1:
                time.sleep(sleep_between)

    def reset_failed(self, field: str, from_val: str = "failed",
                     to_val: str = "pending") -> int:
        all_rows = self.get_all_rows()
        resets   = [{"row_index": row["_row_index"], "data": {field: to_val}}
                    for row in all_rows
                    if str(row.get(field, "")).strip() == from_val]
        if not resets:
            print(f"No rows with {field}={from_val}", file=sys.stderr)
            return 0
        print(f"Resetting {len(resets)} rows: {field} {from_val}→{to_val}", file=sys.stderr)
        self.update_batch(resets)
        return len(resets)

    def stats(self) -> dict:
        from collections import Counter
        all_rows = self.get_all_rows()
        result   = {"total_rows": len(all_rows)}
        for col in ["apollo_match_status", "profile_summary_scrape",
                    "posts_scrape_status", "extract_username_status"]:
            counts = Counter(
                str(r.get(col, "(empty)")).strip() or "(empty)"
                for r in all_rows
            )
            result[col] = dict(counts)
        return result
```

---

## Notes

- **Shared file** — this same file exists in both `apollo-person-match/scripts/` and `linkedin-enrichment/scripts/`. Keep them in sync when making changes.
- **Rate limit handling** — exponential backoff: 10s, 20s, 40s on Google Sheets 429 errors.
- **`get_pending()` skip logic** — rows without `linkedin_username` or `linkedin_url` are skipped unless the empty column is `apollo_match_status` (Apollo skill can work with name+email alone).
