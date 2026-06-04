# CVE Detection Rules

Detection and hunting rules for specific CVEs, each in its own subdirectory.

## Coverage

| CVE | Name | Type | Severity |
|---|---|---|---|
| CVE-2026-33825 | [BlueHammer](cve-2026-33825-bluehammer/) | Windows LPE | 🔴 High |
| CVE-2026-39987 | [Marimo RCE](cve-2026-39987-marimo-rce/) | Pre-auth RCE (Python notebook) | 🔴 Critical |
| CVE-2026-31431 | [Copyfail](cve-2026-31431-copyfail/) | Linux LPE — splice()+AF_ALG SUID overwrite | 🔴 Critical |
| CVE-2026-21858 + CVE-2025-68613 | [n8n Full Chain](cve-2026-21858-n8n-fullchain/) | LFI → Token Forge → Sandbox Bypass → RCE | 🔴 Critical |
| CVE-2026-41089 | [Netlogon CLDAP](cve-2026-41089-netlogon-cldap/) | Pre-auth DC stack overflow via CLDAP — DoS/potential RCE | 🔴 Critical |

## Structure

Each CVE subdirectory contains:
- `analytics/` — scheduled detection rules for automated alerting
- `hunting/` — proactive hunting queries
- `README.md` — vulnerability description and deployment guidance
