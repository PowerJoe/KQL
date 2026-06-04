# TA4922 — Analytics Rules

Scheduled detection rules covering the TA4922 Atlas RAT campaign. All rules target Windows endpoints enrolled in MDE.

## Rules

| Rule | Severity | MITRE | Description |
|---|---|---|---|
| `ta4922-atlas-rat-c2.kql` | 🔴 Critical | T1571, T1573 | Connection to Atlas RAT C2 on port 886 — confirmed compromise |
| `ta4922-romulusloader-c2.kql` | 🔴 Critical | T1071.001, T1571 | Connection to RomulusLoader C2 on port 1234 |
| `ta4922-silentrunloader-c2-exfil.kql` | 🔴 Critical | T1041, T1005 | SilentRunLoader C2 domain and /upload.php exfiltration |
| `ta4922-dll-sideloading.kql` | 🔴 High | T1574.001 | vulkan-1.dll / libcef.dll loaded from user-writable directory |
| `ta4922-process-injection-svchost-dllhost.kql` | 🔴 High | T1055.012 | svchost/dllhost spawned by unexpected parent |
| `ta4922-chrome-credential-theft.kql` | 🔴 High | T1555.003, T1005 | Chrome Login Data / Cookies accessed by non-browser process |
| `ta4922-rmm-tool-deployment.kql` | 🟠 Medium | T1219 | AnyDesk / SyncFuture launched by suspicious parent |

## Tuning notes

- `ta4922-dll-sideloading.kql` — extend the vendor exclusion list (`NVIDIA`, `AMD`, `Intel`) with any custom GPU driver paths in your environment.
- `ta4922-process-injection-svchost-dllhost.kql` — add known-good management tools (e.g., SCCM, WSUS agents) to the exclusion list if they legitimately spawn svchost.
- `ta4922-rmm-tool-deployment.kql` — if AnyDesk is an approved tool in your environment, adjust to alert only on suspicious parent processes.
