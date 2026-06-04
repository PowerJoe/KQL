# 🛡️ KQL Detection Rules

> A curated collection of KQL detection and hunting rules for Microsoft Sentinel and Microsoft Defender XDR, built from real-world incidents, threat intelligence, and hands-on SOC experience.

---

## 📁 Repository Structure

```
kql-detection-rules/
├── threat-intelligence/
│   ├── shai-hulud/         # Shai-Hulud supply chain campaign
│   ├── supply-chain/       # Generic supply chain rules
│   ├── vscode-github-token-theft/ # VSCode webview token theft (VSCode ≤ v1.97)
│   ├── ta4922-atlas-rat/   # TA4922 Atlas RAT campaign (Chinese threat actor)
│   ├── apt36-vibeware/     # APT36 VibeWare DeskRAT campaign (Linux)
│   ├── deskcvb/            # DesckVB RAT malspam campaign
│   └── cve/
│       ├── cve-2026-9082-drupal-jsonapi-sqli/ # Drupal JSON:API error-based SQLi
│       ├── cve-2026-48778-notepadpp/      # Notepad++ config.xml ShellExecute hijack
│       ├── cve-2026-20230-cucm-webdialer/ # Cisco CUCM WebDialer SSRF → root
│       ├── cve-2026-34159-llamacpp-rpc/   # llama.cpp RPC null-buffer bypass RCE
│       ├── cve-2026-34486-tomcat-tribes/  # Tomcat Tribes deserialization RCE
│       ├── cve-2026-41089-netlogon-cldap/ # Netlogon CLDAP stack overflow (DC DoS)
│       ├── cve-2026-21858-n8n-fullchain/ # n8n LFI+RCE full chain
│       ├── cve-2026-31431-copyfail/    # Copyfail Linux LPE (splice+AF_ALG)
│       ├── cve-2026-33825-bluehammer/  # BlueHammer LPE
│       └── cve-2026-39987-marimo-rce/ # Marimo pre-auth RCE
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

## 🔴 CVE Coverage

### BlueHammer — CVE-2026-33825

Windows Defender local privilege escalation via a race condition on `RstrtMgr.dll`. The exploit freezes Defender mid-remediation using a batch oplock, forces a Volume Shadow Copy snapshot, then reads `SAM`/`SYSTEM`/`SECURITY` hives from the snapshot to dump credentials.

Rules: [`threat-intelligence/cve/cve-2026-33825-bluehammer/`](threat-intelligence/cve/cve-2026-33825-bluehammer/)

| File | Type | Description |
|------|------|-------------|
| `analytics/bluehammer-rstrtmgr-oplock.kql` | Analytics | Oplock on RstrtMgr.dll — highest fidelity |
| `analytics/bluehammer-vss-sam-access.kql` | Analytics | SAM hive read from VSS snapshot |
| `analytics/bluehammer-suspicious-services-exec.kql` | Analytics | Suspicious service execution |
| `analytics/bluehammer-vss-enumeration.kql` | Analytics | VSS enumeration activity |
| `hunting/bluehammer-all-ttps-combined.kql` | Hunting | Correlates all 3 TTPs per device |
| `hunting/bluehammer-rstrtmgr-baseline.kql` | Hunting | Baseline for allow-list tuning |

### Marimo RCE — CVE-2026-39987

Pre-authentication remote code execution in Marimo (Python reactive notebook, < 0.23.0). The unauthenticated `/terminal/ws` WebSocket allocates a PTY and spawns a shell with no credential checks. Exploited in-the-wild within 9h 41m of disclosure; credential theft observed in under 3 minutes post-compromise.

Rules: [`threat-intelligence/cve/cve-2026-39987-marimo-rce/`](threat-intelligence/cve/cve-2026-39987-marimo-rce/)

| File | Type | Description |
|------|------|-------------|
| `analytics/marimo-rce-shell-spawn.kql` | Analytics | Shell spawned by Python/Marimo — highest fidelity |
| `analytics/marimo-rce-terminal-ws-access.kql` | Analytics | WebSocket upgrade to `/terminal/ws` in WAF/proxy logs |
| `analytics/marimo-rce-credential-file-access.kql` | Analytics | SSH keys / cloud tokens read post-exploit |
| `analytics/marimo-rce-outbound-connection.kql` | Analytics | Unexpected outbound connection from Python/shell |
| `hunting/marimo-rce-exploit-chain-hunting.kql` | Hunting | Correlates all 3 TTPs per device |
| `hunting/marimo-rce-post-exploit-discovery.kql` | Hunting | Discovery commands run under Marimo PTY |

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
