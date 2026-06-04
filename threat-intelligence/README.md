### 🐀 DesckVB RAT
Malspam campaign delivering a .NET RAT via HTML redirect → ZIP → JS loader → PowerShell dropper → process hollowing.

| Rule | Platform | Severity | MITRE |
|---|---|---|---|
| DesckVB C2 DDNS Communication | Sentinel / MDE | 🔴 Critical | T1095 |
| DesckVB NVIDEO Run Key Persistence | Sentinel / MDE | 🔴 High | T1547.001 |
| DesckVB Defender Exclusion Registry | Sentinel / MDE | 🔴 High | T1562.001 |
| DesckVB InstallUtil/MSBuild Proxy Execution | Sentinel / MDE | 🔴 High | T1218.004, T1127.001 |
| DesckVB WScript JS Execution from Public | Sentinel / MDE | 🔴 High | T1204.002 |
| DesckVB Scheduled Task via XML | Sentinel / MDE | 🟠 Medium | T1053.005 |

### 🏭 Supply Chain
Detection rules targeting software supply chain attacks across npm, PyPI, and other package ecosystems.

| Rule | Platform | Severity | MITRE |
|---|---|---|---|
| Shai-Hulud C2 Exfiltration | Sentinel / MDE | 🔴 High | T1041 |
| Shai-Hulud NPM Package Execution | Sentinel / MDE | 🔴 High | T1195.002 |
| Shai-Hulud CI/CD Secret Harvesting | Sentinel / MDE | 🔴 High | T1552.001 |
| Shai-Hulud GitHub Repo Creation | Sentinel / MDE | 🟠 Medium | T1537 |
| Shai-Hulud VS Code/Claude Code Backdoor | Sentinel / MDE | 🔴 High | T1176 |
| Shai-Hulud Obfuscated index.js Drop | Sentinel / MDE | 🟠 Medium | T1027 |
| Shai-Hulud GitHub API Abuse | Sentinel / MDE | 🟠 Medium | T1537 |

### 🔗 Generic Supply Chain Coverage
Broad detection rules applicable to any supply chain attack, not campaign-specific.

| Rule | Platform | Severity | MITRE |
|---|---|---|---|
| Package Manager Outbound C2 | Sentinel / MDE | 🔴 High | T1041 |
| Suspicious Lifecycle Hook Execution | Sentinel / MDE | 🔴 High | T1059.007 |
| Package Manager Credential File Access | Sentinel / MDE | 🔴 High | T1552.001 |
| Obfuscated Script via Package Manager | Sentinel / MDE | 🟠 Medium | T1027 |
| Package Manager Spawning Child Process | Sentinel / MDE | 🔴 High | T1059 |
| Automated GitHub Repository Creation | Sentinel / MDE | 🟠 Medium | T1537 |
| Mass Package Version Republish | Sentinel / MDE | 🔴 High | T1195.002 |
