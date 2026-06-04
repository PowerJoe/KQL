### 🇵🇰 APT36 VibeWare (DeskRAT)
Pakistan-linked APT36 campaign targeting Indian military on Linux via weaponized .desktop files and a Golang RAT.

| Rule | Platform | Severity | MITRE |
|---|---|---|---|
| APT36 C2 WebSocket Connection | MDE (Linux) | 🔴 Critical | T1071.001, T1571 |
| APT36 XDG Autostart Persistence | MDE (Linux) | 🔴 High | T1547.013 |
| APT36 Crontab @reboot Persistence | MDE (Linux) | 🔴 High | T1053.003 |
| APT36 .bashrc Startup Injection | MDE (Linux) | 🔴 High | T1546.004 |
| APT36 Curl Decode Pipeline | MDE (Linux) | 🔴 High | T1059.004, T1105 |
| APT36 IP Recon from Script Engine | MDE (Linux) | 🟠 Medium | T1016 |

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

### 🏭 Shai-Hulud Supply Chain Campaign
Detection rules targeting the Shai-Hulud software supply chain campaign across npm and PyPI.

| Rule | Type | Platform | Severity | MITRE |
|---|---|---|---|---|
| Shai-Hulud C2 Exfiltration | Analytics | Sentinel / MDE | 🔴 High | T1041 |
| Shai-Hulud NPM Package Execution | Analytics | Sentinel / MDE | 🔴 High | T1195.002 |
| Shai-Hulud CI/CD Secret Harvesting | Analytics | Sentinel / MDE | 🔴 High | T1552.001 |
| Shai-Hulud GitHub Repo Creation | Analytics | Sentinel / MDE | 🟠 Medium | T1537 |
| Shai-Hulud VS Code Backdoor | Analytics | Sentinel / MDE | 🔴 High | T1176 |
| Shai-Hulud Obfuscated index.js Drop | Analytics | Sentinel / MDE | 🟠 Medium | T1027 |
| Shai-Hulud GitHub API Abuse | Analytics | Sentinel / MDE | 🟠 Medium | T1537 |
| Shai-Hulud @antv Package Execution | Hunting | Sentinel / MDE | 🔴 High | T1195.002 |
| Shai-Hulud Non-@antv Package Execution | Hunting | Sentinel / MDE | 🔴 High | T1195.002 |
| Shai-Hulud Compromised PyPI Packages | Hunting | Sentinel / MDE | 🔴 High | T1195.002 |
| Shai-Hulud C2 and Campaign Indicators | Hunting | Sentinel / MDE | 🔴 High | T1041, T1552 |
| Shai-Hulud GitHub Repository Creation | Hunting | Sentinel / MDE | 🟠 Medium | T1537 |

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
