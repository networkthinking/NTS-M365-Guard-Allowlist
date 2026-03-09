# Allowlist for NTS-M365-Guard

This folder contains a sample `allowlist.json` for use with the **Allowlist URL** feature in NTS-M365-Guard.

## Deploy to NTS-M365-Guard-Allowlist

To use a remote allowlist, copy `allowlist.json` to the [NTS-M365-Guard-Allowlist](https://github.com/networkthinking/NTS-M365-Guard-Allowlist) repository:

1. Clone or fork https://github.com/networkthinking/NTS-M365-Guard-Allowlist
2. Add `allowlist.json` to the root (or any path)
3. Use the raw URL in NTS-M365-Guard settings, e.g.:
   - `https://raw.githubusercontent.com/networkthinking/NTS-M365-Guard-Allowlist/refs/heads/main/allowlist.json`

## JSON Schema

```json
{
  "version": "1.0",
  "lastUpdated": "ISO 8601 date",
  "description": "Optional description",
  "patterns": [
    "https://example.com/*",
    "https://*.trusted.com/*",
    "^https://trusted\\.example\\.com/.*"
  ]
}
```

- **patterns** (required): Array of URL patterns. Supports:
  - Simple URLs with `*` wildcards (e.g. `https://*.example.com/*`)
  - Regex patterns (e.g. `^https://trusted\.example\.com/.*`)

Patterns are merged with the user-configured URL Allowlist in the extension. The extension fetches this file every 30 minutes by default.
