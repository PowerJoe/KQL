# DesckVB RAT

Detection and hunting rules for the **DesckVB RAT** delivery chain, a malspam campaign delivering a .NET remote access trojan via HTML redirect → ZIP → JavaScript loader → PowerShell dropper → process hollowing into a signed .NET binary.

## Attack chain

1. **Malspam** — HTML attachment (`Bestellung_2026.html`) with meta-refresh redirect through high-reputation domains (DoubleClick → redirector → delivery kit)
2. **ZIP delivery** — `pengajian.muliastudy.com` delivers an archive containing a JS loader
3. **JS loader** (`wscript.exe //nologo`) — relocates itself to `C:\Users\Public\`, downloads PowerShell stages from staging servers, checks geolocation via `ipapi.co`
4. **PowerShell dropper** — decodes and drops the packed RAT, adds Defender exclusions, creates two XML-based scheduled tasks
5. **Process hollowing** — RAT is injected into `installutil.exe` or `MSBuild.exe` (operator-configurable)
6. **Persistence** — HKCU Run key named `Update Drivers NVIDEO_<random>`, repeating scheduled task (PT8-11M)
7. **C2** — Raw TCP to `xtadts.ddns.net` / `afxwd.ddns.net`, AES-encrypted (PBKDF2 from "P@55w0rd!"), certificate-pinned

## Layout

```
deskcvb/
├── analytics/                              # Scheduled detection rules
│   ├── deskcvb-wscript-js-execution.kql        # JS loader from Public folder
│   ├── deskcvb-installutil-msbuild-proxy.kql   # Process hollowing into signed binary
│   ├── deskcvb-defender-exclusion-registry.kql # Defender exclusion added
│   ├── deskcvb-nvideo-run-key-persistence.kql  # NVIDEO Run key persistence
│   ├── deskcvb-scheduled-task-xml.kql          # XML-based scheduled task creation
│   └── deskcvb-c2-ddns-communication.kql       # C2 DDNS domain hits
└── hunting/                                # Proactive hunting queries
    ├── deskcvb-full-chain-hunting.kql          # Correlates all TTPs per device
    ├── deskcvb-public-folder-staging.kql       # Multi-file drop in Public folder
    └── deskcvb-payload-delivery-domains.kql    # Delivery infra and geolocation check
```

## Deployment order

1. Enable `deskcvb-c2-ddns-communication.kql` immediately — any hit is confirmed C2.
2. Enable `deskcvb-nvideo-run-key-persistence.kql` and `deskcvb-defender-exclusion-registry.kql` — low false-positive risk.
3. Enable `deskcvb-installutil-msbuild-proxy.kql` — review any InstallUtil/MSBuild spawned by PowerShell; tune out legitimate build pipelines.
4. Enable `deskcvb-wscript-js-execution.kql` and `deskcvb-scheduled-task-xml.kql`.
5. Run `deskcvb-full-chain-hunting.kql` and `deskcvb-public-folder-staging.kql` daily as hunting routines.

## Network IOCs

| Domain | Purpose |
|---|---|
| `xtadts.ddns.net` | C2 (primary) |
| `afxwd.ddns.net` | C2 (secondary) |
| `pengajian.muliastudy.com` | ZIP delivery |
| `catalogo.castrouria.com` | Packed RAT payload |
| `startthewave.org` | Redirect stage |

## References

- [Huntress — Malspam to DesckVB RAT Delivery Chain Analysis](https://www.huntress.com/blog/malspam-to-deskcvb-rat-delivery-chain-analysis)
