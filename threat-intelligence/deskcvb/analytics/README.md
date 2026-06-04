# DesckVB RAT — Analytics Rules

Scheduled detection rules covering the DesckVB RAT attack chain. Deploy in Microsoft Sentinel or as MDE Custom Detection Rules.

## Rules

| Rule | Severity | MITRE | Description |
|---|---|---|---|
| `deskcvb-c2-ddns-communication.kql` | 🔴 Critical | T1095 | Outbound connection to known C2 DDNS domains — confirmed compromise |
| `deskcvb-nvideo-run-key-persistence.kql` | 🔴 High | T1547.001 | HKCU Run key named "Update Drivers NVIDEO_*" |
| `deskcvb-defender-exclusion-registry.kql` | 🔴 High | T1562.001 | Registry write adding a Windows Defender exclusion |
| `deskcvb-installutil-msbuild-proxy.kql` | 🔴 High | T1218.004, T1127.001 | installutil.exe or MSBuild.exe spawned by powershell.exe |
| `deskcvb-wscript-js-execution.kql` | 🔴 High | T1204.002 | wscript.exe executing a JS file from C:\Users\Public\ |
| `deskcvb-scheduled-task-xml.kql` | 🟠 Medium | T1053.005 | schtasks /Create /XML targeting a Temp path |

## Tuning notes

- `deskcvb-installutil-msbuild-proxy.kql` may fire on legitimate CI/CD pipelines. Add known build agent hostnames or service accounts to an exclusion list before enabling automated alerting.
- `deskcvb-scheduled-task-xml.kql` — narrow the scope with `| where InitiatingProcessFileName !in~ ("msiexec.exe", "setup.exe")` if noisy in your environment.
