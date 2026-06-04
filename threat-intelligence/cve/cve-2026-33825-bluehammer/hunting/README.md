# BlueHammer — Hunting Queries

Proactive hunting queries for CVE-2026-33825 (BlueHammer). These are not intended for automated alerting — run them manually or on a daily schedule in Advanced Hunting.

## Queries

| Query | Description |
|---|---|
| `bluehammer-rstrtmgr-baseline.kql` | 7-day baseline of all processes that load RstrtMgr.dll. Run this **before** enabling the analytics rules to tune the allow-list. |
| `bluehammer-all-ttps-combined.kql` | Correlates all three core BlueHammer TTPs (VSS SAM access, services.exe spawn, VSS enumeration) on the same device. A hit on all three is a strong indicator of an active exploit. |

## Usage

Run `bluehammer-rstrtmgr-baseline.kql` first across a 7-day lookback. Any process/integrity-level combination that appears frequently is likely legitimate and should be added to the allow-list in `../analytics/bluehammer-rstrtmgr-oplock.kql`.

Schedule `bluehammer-all-ttps-combined.kql` to run daily as an ongoing hunting routine.
