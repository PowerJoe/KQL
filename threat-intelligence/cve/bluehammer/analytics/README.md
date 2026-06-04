# BlueHammer — Analytics Rules

Scheduled detection rules for CVE-2026-33825 (BlueHammer). Deploy these in Microsoft Sentinel or as MDE Custom Detection Rules for automated alerting.

## Rules

| Rule | Severity | MITRE | Description |
|---|---|---|---|
| `bluehammer-rstrtmgr-oplock.kql` | 🔴 High | T1003.002 | Non-system process loads RstrtMgr.dll — highest fidelity signal, start here |
| `bluehammer-vss-sam-access.kql` | 🔴 High | T1003.002 | Low/medium integrity process reads SAM/SYSTEM/SECURITY from a VSS snapshot |
| `bluehammer-suspicious-services-exec.kql` | 🟠 Medium | T1543.003 | services.exe spawned by a non-SYSTEM low/medium integrity process |
| `bluehammer-vss-enumeration.kql` | 🟠 Medium | T1003.002 | Low/medium integrity process enumerates Volume Shadow Copy snapshots |

## Deployment order

1. Run `../hunting/bluehammer-rstrtmgr-baseline.kql` (7-day lookback) first to identify legitimate RstrtMgr.dll loaders in your environment.
2. Extend the allow-list in `bluehammer-rstrtmgr-oplock.kql` based on baseline output.
3. Enable `bluehammer-rstrtmgr-oplock.kql` — lowest false-positive risk.
4. Enable the VSS and services rules as supporting signals.

## Requirements

- `bluehammer-rstrtmgr-oplock.kql` requires **MDE Advanced Features → DLL load monitoring** to be enabled, otherwise `DeviceImageLoadEvents` will be empty.
