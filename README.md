# NTS-M365-Guard-Allowlist

Configuration files for NTS-M365-Guard:

- **allowlist.json** – URL allowlist for the **Allowlist URL** feature
- **nts_rules.json** – Additional phishing indicator rules (merged with base CyberDrain/Check rules)

## allowlist.json

### Deploy

To use a remote allowlist, copy `allowlist.json` to this repository:

1. Clone or fork https://github.com/networkthinking/NTS-M365-Guard-Allowlist
2. Add `allowlist.json` to the root (or any path)
3. Use the raw URL in NTS-M365-Guard settings, e.g.:
   - `https://raw.githubusercontent.com/networkthinking/NTS-M365-Guard-Allowlist/refs/heads/main/allowlist.json`

### Schema

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

## nts_rules.json

Additional phishing indicator rules that merge with the base rules (CyberDrain/Check). Host this file and set **Additional Rules URL** in NTS-M365-Guard Options.

### Deploy

1. Add `nts_rules.json` to this repository
2. Use the raw URL in NTS-M365-Guard Options → Additional Rules URL, e.g.:
   - `https://raw.githubusercontent.com/networkthinking/NTS-M365-Guard-Allowlist/refs/heads/main/nts_rules.json`

### Schema

Each rule in `phishing_indicators` supports:

- **id** (required): Unique identifier
- **pattern** (required): Regex pattern to match (supports `flags` for case-insensitivity)
- **severity**: `high`, `medium`, `low`
- **description**: Human-readable description
- **action**: `block` or `warn`
- **category**: e.g. `credential_harvesting`
- **confidence**: 0–1 score
