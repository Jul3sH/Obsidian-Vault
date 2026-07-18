---
type: reference
created: 2026-07-17
tags: [ai-os, system-design, codex, google-drive, google-sheets, connector]
---

# Google Drive Connector

> Hosted Google connector used by Codex for Drive, Docs, Sheets, and Slides.

## Key Takeaways

- The hosted `Google Drive` plugin is installed in Codex.
- This is the preferred route for Google Sheets work because Julian does not want to host a local MCP server.
- The local `google-sheets` streamable HTTP MCP endpoint was removed from Codex config.
- Authentication is working as of 2026-07-17.

## Capability

Once Julian signs in again, the hosted connector exposes Google Sheets tools for:

| Capability | Supported |
|---|---|
| Create a native Google Sheet | Yes |
| Import an `.xlsx` or `.csv` as a native Google Sheet | Yes |
| Read spreadsheet metadata | Yes |
| Read spreadsheet ranges and cells | Yes |
| Apply Google Sheets `batchUpdate` operations | Yes |
| Duplicate an existing sheet into a new spreadsheet | Yes |
| Rename or move Drive files | Yes |
| List Drive folders and shared drives | Yes |

## Current State

Installed plugin:

```text
google-drive@openai-curated-remote
```

Earlier observed auth failure:

```text
HTTP 401: Provided authentication token is expired. Please try signing in again.
```

Resolved by Julian re-authenticating. A read-only root-folder listing then succeeded and returned Google Sheets including `UK Relocation Cashflows`, `UK Relocation savings comparison`, and `UK Relocation RISKS`.

## Next Step

No setup blocker currently. Codex can use the hosted connector to create and edit Google Sheets directly, subject to normal permissions and user approval flow.

## Related

- [[codex-setup]] - Codex hidden-file mirroring and config rules
- [[config.toml]] - Current visible mirror of `~/.codex/config.toml`
