# credentials.py — Shared Credential Manager

tags: [technical, skills, python, credentials, security]

> *Shared across all pipeline skills. Loads API keys from `~/.leadgen/credentials.json` into `os.environ` at script startup. Prompts interactively on first run; silent on all subsequent runs.*

---

## Responsibilities

- Read `~/.leadgen/credentials.json` (chmod 600)
- For each required key: check `os.environ` first, then the JSON file, then prompt the user
- Inject missing keys into `os.environ`
- Save newly entered keys back to the JSON file
- Support key rotation via `update()` and `rotate()` methods

---

## Usage Pattern

Every script in the pipeline calls this at the top:

```python
from credentials import CredentialManager

CredentialManager.load(required=[
    "RAPIDAPI_KEY",
    "ANTHROPIC_API_KEY",
    "SHEETS_AUTH_METHOD",
])
```

After `load()` returns, all required keys are guaranteed to be in `os.environ`.

---

## Credentials File

```
~/.leadgen/credentials.json   (chmod 600 — owner read/write only)
```

Current contents:
```json
{
  "SHEETS_AUTH_METHOD": "service_account",
  "RAPIDAPI_KEY": "...",
  "ANTHROPIC_API_KEY": "...",
  "GOOGLE_SERVICE_ACCOUNT_JSON": "/Users/julianhart/Downloads/lead-enrichment-494612-b952d1eb408f.json"
}
```

**Never commit this file to git. Never paste values into chat.**  
To rotate a key: `python -c "from credentials import CredentialManager; CredentialManager.rotate('RAPIDAPI_KEY')"`

---

## Source

```python
"""Shared credential manager for the lead enrichment pipeline.

Stores API keys securely in ~/.leadgen/credentials.json (chmod 600).
On first run, prompts the user to enter any missing keys.
On subsequent runs, loads silently with no user interaction required.
"""
import os, json, sys, stat
from pathlib import Path
from getpass import getpass

CREDENTIALS_DIR  = Path.home() / ".leadgen"
CREDENTIALS_FILE = CREDENTIALS_DIR / "credentials.json"

KEY_META = {
    "APOLLO_API_KEY": {
        "label":  "Apollo API key",
        "hint":   "Find it at: https://app.apollo.io/#/settings/integrations/api",
        "secret": True,
    },
    "RAPIDAPI_KEY": {
        "label":  "RapidAPI key",
        "hint":   "Find it at: https://rapidapi.com/developer/apps → your app → Authorization",
        "secret": True,
    },
    "ANTHROPIC_API_KEY": {
        "label":  "Anthropic API key",
        "hint":   "Find it at: https://console.anthropic.com/settings/keys",
        "secret": True,
    },
    "OPENAI_API_KEY": {
        "label":  "OpenAI API key",
        "hint":   "Find it at: https://platform.openai.com/api-keys",
        "secret": True,
    },
    "SHEETS_AUTH_METHOD": {
        "label":   "Google Sheets authentication method",
        "hint":    "Enter 'service_account' or 'oauth'",
        "secret":  False,
        "choices": ["service_account", "oauth"],
    },
    "GOOGLE_SERVICE_ACCOUNT_JSON": {
        "label":  "Path to your Google service account JSON key file",
        "hint":   "e.g. /Users/yourname/secrets/service-account.json",
        "secret": False,
    },
}


class CredentialManager:

    @classmethod
    def load(cls, required: list[str]):
        """Ensure all required keys are in os.environ. Prompt if missing."""
        store   = cls._load_store()
        changed = False

        if "SHEETS_AUTH_METHOD" in required:
            required = cls._expand_sheets_requirements(required, store)

        for key in required:
            if os.environ.get(key):
                continue
            if key in store:
                os.environ[key] = store[key]
                continue
            print(f"\n─── First-time setup ───────────────────────────────")
            value           = cls._prompt_for_key(key)
            store[key]      = value
            os.environ[key] = value
            changed         = True

        if changed:
            cls._save_store(store)
            print("\n  Credentials saved to ~/.leadgen/credentials.json")
            print("  You won't be asked again.\n")

    @classmethod
    def update(cls, key: str, value: str):
        """Update a single credential (e.g. to rotate a key)."""
        store      = cls._load_store()
        store[key] = value
        cls._save_store(store)
        os.environ[key] = value

    @classmethod
    def rotate(cls, key: str):
        """Prompt for a new value for an existing key and overwrite it."""
        store = cls._load_store()
        meta  = KEY_META.get(key, {"label": key, "secret": True})
        if meta.get("secret", True):
            value = getpass(f"  Enter new {meta['label']}: ").strip()
        else:
            value = input(f"  Enter new {meta['label']}: ").strip()
        if value:
            cls.update(key, value)

    @classmethod
    def show(cls):
        """Print which credentials are stored (keys only, never values)."""
        store = cls._load_store()
        if not store:
            print("No credentials stored yet.")
            return
        for key in store:
            print(f"  {key}: {'*' * 8}")

    # ── Private helpers ────────────────────────────────────────────────────────

    @classmethod
    def _load_store(cls) -> dict:
        if CREDENTIALS_FILE.exists():
            try:
                with open(CREDENTIALS_FILE) as f:
                    return json.load(f)
            except (json.JSONDecodeError, OSError):
                return {}
        return {}

    @classmethod
    def _save_store(cls, store: dict):
        CREDENTIALS_DIR.mkdir(parents=True, exist_ok=True)
        with open(CREDENTIALS_FILE, "w") as f:
            json.dump(store, f, indent=2)
        os.chmod(CREDENTIALS_FILE, stat.S_IRUSR | stat.S_IWUSR)  # chmod 600

    @classmethod
    def _prompt_for_key(cls, key: str) -> str:
        meta    = KEY_META.get(key, {"label": key, "hint": "", "secret": True})
        secret  = meta.get("secret", True)
        choices = meta.get("choices")
        print(f"\n  {meta['label']} not found.")
        if meta.get("hint"):
            print(f"  {meta['hint']}")
        while True:
            value = (getpass if secret else input)(f"  Enter {meta['label']}: ").strip()
            if not value:
                print("  Value cannot be empty.")
                continue
            if choices and value not in choices:
                print(f"  Invalid value. Choose from: {', '.join(choices)}")
                continue
            if key == "GOOGLE_SERVICE_ACCOUNT_JSON":
                if not Path(value).expanduser().exists():
                    print(f"  File not found: {value}")
                    continue
                value = str(Path(value).expanduser().resolve())
            return value

    @classmethod
    def _expand_sheets_requirements(cls, required: list[str], store: dict) -> list[str]:
        expanded = [k for k in required if k != "SHEETS_AUTH_METHOD"]
        method   = os.environ.get("SHEETS_AUTH_METHOD") or store.get("SHEETS_AUTH_METHOD")
        if not method:
            method = cls._prompt_for_key("SHEETS_AUTH_METHOD")
            store["SHEETS_AUTH_METHOD"] = method
            os.environ["SHEETS_AUTH_METHOD"] = method
            cls._save_store(store)
        if method == "service_account":
            expanded.append("GOOGLE_SERVICE_ACCOUNT_JSON")
        return expanded
```

---

## Notes

- **Shared across all skills** — identical copy in every skill's `scripts/` directory.
- **Load order priority:** `os.environ` → `credentials.json` → interactive prompt. This means you can override any key temporarily by exporting it in the shell before running.
- **Security:** File is chmod 600. Values are never logged. Secrets use `getpass` (hidden input).
- **Key rotation:** If a key is exposed (e.g. pasted into chat), rotate it immediately using the `rotate()` method or by logging into the provider dashboard and generating a new key, then updating the file.
