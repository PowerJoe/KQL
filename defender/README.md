# Microsoft Defender XDR

KQL rules for Microsoft Defender XDR, covering Advanced Hunting queries and Custom Detection Rules.

## Structure

```
defender/
├── custom-detections/   # MDE Custom Detection Rules (automated alerting)
└── hunting/             # Advanced Hunting queries (proactive threat hunting)
```

## Subdirectories

### custom-detections/
Scheduled Custom Detection Rules for Microsoft Defender XDR. These run automatically and generate alerts/incidents when triggered.

### hunting/
Proactive hunting queries for Advanced Hunting. Currently focused on the **Shai-Hulud** supply chain campaign.

| Rule | Severity | MITRE | Description |
|---|---|---|---|
| Hunting - @antv Package Execution | 🔴 High | T1195.002 | Detects execution of any of the 323 compromised @antv packages |
| Hunting - Non-@antv Package Execution | 🔴 High | T1195.002 | Covers compromised packages outside @antv (@tanstack, @uipath, @mistralai, etc.) |
| Hunting - Compromised PyPI Packages | 🔴 High | T1195.002 | Detects installation of specific compromised PyPI versions |
| Hunting - C2 and Campaign Indicators | 🔴 High | T1041, T1552 | Combines C2 network IOCs, credential access, and GitHub campaign markers |
| Hunting - GitHub Repository Creation | 🟠 Medium | T1537 | Detects automated GitHub repo creation used for fallback exfiltration |
