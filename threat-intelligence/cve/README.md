# CVE Detection Rules

Detection and hunting rules for specific CVEs, each in its own subdirectory.

## Coverage

| CVE | Name | Type | Severity |
|---|---|---|---|
| CVE-2025-64446 | [FortiWeb RCE](cve-2025-64446-fortiweb-rce/) | Pre-auth auth bypass + path traversal + RCE | 🔴 Critical |
| CVE-2026-33825 | [BlueHammer](cve-2026-33825-bluehammer/) | Windows LPE | 🔴 High |
| CVE-2026-39987 | [Marimo RCE](cve-2026-39987-marimo-rce/) | Pre-auth RCE (Python notebook) | 🔴 Critical |
| CVE-2026-31431 | [Copyfail](cve-2026-31431-copyfail/) | Linux LPE — splice()+AF_ALG SUID overwrite | 🔴 Critical |
| CVE-2026-21858 + CVE-2025-68613 | [n8n Full Chain](cve-2026-21858-n8n-fullchain/) | LFI → Token Forge → Sandbox Bypass → RCE | 🔴 Critical |
| CVE-2026-41089 | [Netlogon CLDAP](cve-2026-41089-netlogon-cldap/) | Pre-auth DC stack overflow via CLDAP — DoS/potential RCE | 🔴 Critical |
| CVE-2026-34486 | [Tomcat Tribes RCE](cve-2026-34486-tomcat-tribes/) | EncryptInterceptor fail-open → Java deserialization RCE | 🔴 Critical |
| CVE-2026-34159 | [llama.cpp RPC RCE](cve-2026-34159-llamacpp-rpc/) | Null buffer bypass → arbitrary R/W → pre-auth RCE | 🔴 Critical |
| CVE-2026-20230 | [Cisco CUCM WebDialer SSRF](cve-2026-20230-cucm-webdialer/) | SSRF → file write → root privilege escalation | 🔴 High |
| CVE-2026-48778 | [Notepad++ Code Execution](cve-2026-48778-notepadpp/) | config.xml poisoning → ShellExecute hijack | 🔴 High |
| CVE-2026-9082 | [Drupal JSON:API SQLi](cve-2026-9082-drupal-jsonapi-sqli/) | Error-based SQL injection via JSON:API filter key (PostgreSQL) | 🔴 Critical |
| CVE-2026-43284 / CVE-2026-43500 / CVE-2026-46300 | [Kukurigu LPE](cve-2026-43284-kukurigu/) | Linux page-cache poisoning via xfrm-ESP/RxRPC/Fragnesia → root | 🔴 Critical |
| CVE-2026-21250 | [HTTP.sys LPE](cve-2026-21250-httpsys-lpe/) | Windows HTTP.sys malformed request → BSOD / EoP | 🔴 Critical |

## Structure

Each CVE subdirectory contains:
- `analytics/` — scheduled detection rules for automated alerting
- `hunting/` — proactive hunting queries
- `README.md` — vulnerability description and deployment guidance
