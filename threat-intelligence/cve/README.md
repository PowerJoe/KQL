# CVE Detection Rules

Detection and hunting rules for specific CVEs, each in its own subdirectory.

## Coverage

| CVE | Name | Type | Severity |
|---|---|---|---|
| CVE-2026-33825 | [BlueHammer](cve-2026-33825-bluehammer/) | Windows LPE | 🔴 High |
| CVE-2026-39987 | [Marimo RCE](cve-2026-39987-marimo-rce/) | Pre-auth RCE (Python notebook) | 🔴 Critical |

## Structure

Each CVE subdirectory contains:
- `analytics/` — scheduled detection rules for automated alerting
- `hunting/` — proactive hunting queries
- `README.md` — vulnerability description and deployment guidance
