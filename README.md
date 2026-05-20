# 🛡️ KQL Detection Rules

> A curated collection of KQL detection and hunting rules for Microsoft Sentinel and Microsoft Defender XDR — built from real-world incidents, threat intelligence, and hands-on SOC experience.

---

## 📁 Repository Structure

```
kql-detection-rules/
├── sentinel/
│   ├── analytics/          # Scheduled Analytics Rules
│   ├── hunting/            # Hunting Queries
│   └── workbooks/          # Workbook queries
├── defender/
│   ├── custom-detections/  # MDE Custom Detection Rules
│   └── hunting/            # Advanced Hunting Queries
├── threat-intelligence/
│   └── supply-chain/       # Supply chain campaign rules
│       └── shai-hulud/     # Shai-Hulud campaign IOCs & rules
└── README.md
```

---

## 🔍 Rule Categories

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

---

## 🚀 Getting Started

### Microsoft Sentinel
1. Navigate to **Microsoft Sentinel → Analytics → Create → Scheduled query rule**
2. Copy the KQL from the rule file
3. Configure the frequency and lookback period as specified in the rule header
4. Map entities as documented
5. Set severity and MITRE tags

### Microsoft Defender XDR
1. Navigate to **security.microsoft.com → Hunting → Custom detection rules**
2. Paste the KQL query
3. Set the rule frequency and alert title
4. Configure impacted entities
5. Save and enable

---

## 📋 Rule Header Format

Every rule in this repository follows this header format:

```
// ============================================================
// Rule Name    : <name>
// Platform     : Sentinel | MDE | Both
// Severity     : Low | Medium | High | Critical
// Frequency    : Every Xh
// Lookback     : Xh
// MITRE Tactic : <tactic>
// MITRE Tech   : <technique>
// Author       : PJ131
// Last Updated : YYYY-MM-DD
// Description  : <description>
// ============================================================
```

---

## 🎯 Hunting Queries

Hunting queries are designed for **proactive threat hunting** rather than automated alerting. They are located in the `hunting/` directories and are optimized for:

- Broad coverage over longer timeframes
- Lower false positive rates in manual analysis
- Pivoting on known IOCs from threat intelligence

---

## ⚠️ Disclaimer

> These rules are provided **as-is** for educational and defensive purposes. Always test in a non-production environment before deploying. Rules may generate false positives depending on your environment — tuning is recommended before enabling automated alerting.
>
> IOCs and rule logic are based on publicly available threat intelligence. Always validate against the latest sources before deployment.

---

## 📚 Sources & References

- [Socket Research — Shai-Hulud Campaign](https://socket.dev)
- [Endor Labs](https://www.endorlabs.com)
- [Aikido Security](https://www.aikido.dev)
- [Microsoft MITRE ATT&CK mapping](https://attack.mitre.org)
- [KQL Reference](https://learn.microsoft.com/en-us/azure/data-explorer/kusto/query/)

---

## 📺 YouTube

Rules from this repository are featured on **[Hackin' with PJ131](https://youtube.com/@hackinwithpj131)** — covering red team, blue team, detection engineering, and HackTheBox walkthroughs.

---

## 📄 License

MIT License — free to use, modify, and distribute. Attribution appreciated.

---

*Built by a security consultant with OSCP, CISSP & SC-200 — from the SOC to the lab.*
