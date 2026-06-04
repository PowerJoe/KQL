# Shai-Hulud Campaign

Detection and hunting rules for the **Shai-Hulud** software supply chain campaign, targeting npm, PyPI, and other package ecosystems.

## Rules

| Rule | Type | Severity | MITRE |
|---|---|---|---|
| `shai-hulud-c2-exfiltration.kql` | Analytics | 🔴 High | T1041 |
| `shai-hulud-npm-execution.kql` | Analytics | 🔴 High | T1195.002 |
| `shai-hulud-cicd-harvesting.kql` | Analytics | 🔴 High | T1552.001 |
| `shai-hulud-github-repo.kql` | Analytics | 🟠 Medium | T1537 |
| `shai-hulud-vscode-backdoor.kql` | Analytics | 🔴 High | T1176 |
| `shai-hulud-index-js-drop.kql` | Analytics | 🟠 Medium | T1027 |
| `shai-hulud-github-api.kql` | Analytics | 🟠 Medium | T1537 |
| `shai-hulud-antv-packages.kql` | Hunting | 🔴 High | T1195.002 |
| `shai-hulud-non-antv-packages.kql` | Hunting | 🔴 High | T1195.002 |
| `shai-hulud-pypi-packages.kql` | Hunting | 🔴 High | T1195.002 |
| `shai-hulud-c2-indicators.kql` | Hunting | 🔴 High | T1041, T1552 |
| `shai-hulud-github-repo-creation.kql` | Hunting | 🟠 Medium | T1537 |
