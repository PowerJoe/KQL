# 🛡️ KQL Detection Rules

> A curated collection of KQL detection and hunting rules for Microsoft Sentinel and Microsoft Defender XDR, built from real-world incidents, threat intelligence, and hands-on SOC experience.

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

> These rules are provided **as-is** for educational and defensive purposes. Always test in a non-production environment before deploying. Rules may generate false positives depending on your environment, tuning is recommended before enabling automated alerting.
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

## 📄 License

MIT License — free to use, modify, and distribute. Attribution appreciated.

---
