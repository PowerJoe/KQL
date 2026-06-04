# CVE Detection Rules

Detection and hunting rules for specific CVEs, each in its own subdirectory.

## Coverage

| CVE | Name | Type | Severity |
|---|---|---|---|
| CVE-2026-33825 | [BlueHammer](bluehammer/) | Windows LPE | 🔴 High |

## Structure

Each CVE subdirectory contains:
- `analytics/` — scheduled detection rules for automated alerting
- `hunting/` — proactive hunting queries
- `README.md` — vulnerability description and deployment guidance
