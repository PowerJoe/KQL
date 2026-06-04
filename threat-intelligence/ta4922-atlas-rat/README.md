# TA4922 — Atlas RAT Campaign

Detection and hunting rules for **TA4922** (overlaps: Silver Fox, Void Arachne), a Chinese-speaking financially motivated threat actor targeting European and Asian organisations with a multi-malware arsenal delivered via localized phishing lures.

## Malware families

| Malware | Type | C2 |
|---|---|---|
| **Atlas RAT** | Modular backdoor (keylog, screenshot, webcam, audio, file theft, plugin download) | 206.238.115.58:886, 154.211.86.110:886 |
| **RomulusLoader** | PE loader — process hollowing into svchost/dllhost, deploys AnyDesk/SyncFuture | 43.156.77.97:1234, 103.214.172.33 |
| **SilentRunLoader** | Compiled Python stealer — Chrome credentials, cookies, history | ws.ztts88.cyou (18.139.83.110) |
| **Winos4.0/ValleyRAT** | Full RAT — DDoS, webcam, mic, remote shell | RC4-encrypted config |

## Attack chain

1. **Lure delivery** — Localized phishing (HR, payroll, tax authority, invoicing) via email, WhatsApp, LINE, or Teams. Archive names in Japanese, German, and English.
2. **DLL sideloading** — ZIP unpacks a legitimate executable paired with a malicious DLL (`vulkan-1.dll`, `libcef.dll`, `teamspeak_control.dll`) loaded from `%APPDATA%` or `%TEMP%`.
3. **RomulusLoader** — Injects into `svchost.exe` / `dllhost.exe` via process hollowing, fetches next-stage payloads, deploys AnyDesk/SyncFuture for persistent access.
4. **Atlas RAT** — Modular backdoor beacons to port 886 with `SFuck\x00\x00\x00` check-in, ChaCha-encrypted comms.
5. **SilentRunLoader** — Python stealer harvests Chrome credentials, exfiltrates to `/upload.php`.
6. **Persistence** — Drops to `C:\Program Files\Common Files`, Atlas RAT config stored in User Documents.

## Evasion techniques

- Direct syscalls via SysWhispers
- WDAGUtilityAccount username check (WDAG sandbox detection)
- CExecSvc service / `mshome` DNS suffix / `vmsmb` device checks
- Code bloat injection (Winos4.0 variant 71× larger than baseline)
- Legitimate RMM tools (AnyDesk, SyncFuture) as cover

## Layout

```
ta4922-atlas-rat/
├── analytics/
│   ├── ta4922-atlas-rat-c2.kql                   # Atlas RAT C2 — port 886, known IPs
│   ├── ta4922-romulusloader-c2.kql               # RomulusLoader C2 — port 1234
│   ├── ta4922-silentrunloader-c2-exfil.kql       # SilentRunLoader C2 + /upload.php exfil
│   ├── ta4922-dll-sideloading.kql                # vulkan-1.dll / libcef.dll from user dirs
│   ├── ta4922-process-injection-svchost-dllhost.kql  # Anomalous svchost/dllhost parent
│   ├── ta4922-chrome-credential-theft.kql        # Chrome Login Data from non-browser process
│   └── ta4922-rmm-tool-deployment.kql            # AnyDesk/SyncFuture via suspicious parent
└── hunting/
    ├── ta4922-full-chain-hunting.kql             # Correlates all TTPs per device
    ├── ta4922-wechat-injection.kql               # WeChat injection/abnormal spawn
    └── ta4922-payload-hosting-domains.kql        # All C2 + delivery infra hits
```

## Deployment order

1. Enable the three C2 rules immediately — any IOC hit is confirmed compromise.
2. Enable `ta4922-dll-sideloading.kql` — tune GPU driver paths if needed.
3. Enable `ta4922-process-injection-svchost-dllhost.kql` — tune known-good parent processes in your environment.
4. Enable `ta4922-chrome-credential-theft.kql` and `ta4922-rmm-tool-deployment.kql`.
5. Run hunting queries daily.

## Network IOCs

| Indicator | Port | Malware | Purpose |
|---|---|---|---|
| 206.238.115.58 | 886 | Atlas RAT | C2 |
| 154.211.86.110 | 886 | Atlas RAT | C2 |
| 43.156.77.97 | 1234 | RomulusLoader | C2 |
| 103.214.172.33 | — | RomulusLoader | Payload hosting |
| ws.ztts88.cyou / 18.139.83.110 | 443 | SilentRunLoader | C2 + exfil |
| nwphotoblog.com | — | — | Landing page |

## References

- [BleepingComputer — Chinese Hackers Use New Atlas RAT in European Cyberattacks](https://www.bleepingcomputer.com/news/security/chinese-hackers-use-new-atlas-rat-malware-in-european-cyberattacks/)
- [Proofpoint — TA4922: Suspected Chinese Crime Group Going Global](https://www.proofpoint.com/us/blog/threat-insight/ta4922-suspected-chinese-crime-group-going-global)
