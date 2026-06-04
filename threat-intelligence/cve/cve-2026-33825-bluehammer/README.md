# BlueHammer — CVE-2026-33825

Detection and hunting rules for **BlueHammer** (CVE-2026-33825), a Windows Defender local privilege escalation vulnerability.

The exploit chain abuses a race condition: a batch oplock on `RstrtMgr.dll` freezes Windows Defender mid-remediation, forcing it to create a Volume Shadow Copy snapshot. The exploit then enumerates VSS and reads the `SAM`/`SYSTEM`/`SECURITY` hives from the snapshot to dump credentials and escalate privileges. NTFS junction/symlink redirection is used along the way.

These rules are **defensive (blue team)** only — they detect the attack, they do not perform it.

## Layout

```
bluehammer/
├── analytics/                          # Scheduled detection rules
│   ├── bluehammer-rstrtmgr-oplock.kql       # Highest fidelity — start here
│   ├── bluehammer-vss-sam-access.kql        # SAM hive read from VSS snapshot
│   ├── bluehammer-suspicious-services-exec.kql
│   └── bluehammer-vss-enumeration.kql
└── hunting/                            # Proactive hunting (not for alerting)
    ├── bluehammer-all-ttps-combined.kql     # Correlates all 3 TTPs per device
    └── bluehammer-rstrtmgr-baseline.kql     # Run first to tune the allow-list
```

## Deployment order

1. Run `hunting/bluehammer-rstrtmgr-baseline.kql` (7-day lookback) to see what legitimately loads `RstrtMgr.dll` and extend the allow-list in the oplock rule.
2. Enable `analytics/bluehammer-rstrtmgr-oplock.kql` — highest fidelity, lowest false-positive risk.
3. Enable the VSS / services analytics rules as supporting signals.
4. Schedule `hunting/bluehammer-all-ttps-combined.kql` to run daily.

## Notes

- `bluehammer-rstrtmgr-oplock.kql` requires **MDE Advanced Features → DLL load monitoring** to be enabled, otherwise `DeviceImageLoadEvents` will be empty.
- Tune the integrity-level and process allow-lists to your environment before enabling automated alerting.
