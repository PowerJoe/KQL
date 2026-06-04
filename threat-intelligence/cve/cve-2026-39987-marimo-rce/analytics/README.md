# Marimo RCE — Analytics Rules (CVE-2026-39987)

Scheduled detection rules for CVE-2026-39987. Endpoint rules target Linux endpoints enrolled in MDE; the WebSocket rule targets WAF/proxy log sources in Sentinel.

## Rules

| Rule | Severity | Platform | MITRE | Description |
|---|---|---|---|---|
| `marimo-rce-shell-spawn.kql` | 🔴 Critical | MDE (Linux) | T1059.004, T1190 | Shell spawned by Python/Marimo process — direct exploit indicator |
| `marimo-rce-terminal-ws-access.kql` | 🔴 Critical | Sentinel (WAF/Syslog) | T1190 | WebSocket upgrade to `/terminal/ws` in web layer logs |
| `marimo-rce-credential-file-access.kql` | 🔴 High | MDE (Linux) | T1552.001, T1005 | SSH keys, cloud tokens, `.env` files read by Python/shell |
| `marimo-rce-outbound-connection.kql` | 🔴 High | MDE (Linux) | T1041, T1071.001 | Python/shell initiating outbound connection to public IP on non-standard port |

## Tuning notes

- `marimo-rce-outbound-connection.kql` — the internal range exclusion list covers RFC1918. Extend it with any non-RFC1918 trusted ranges (e.g., VPN egress, cloud metadata) specific to your environment.
- `marimo-rce-shell-spawn.kql` — scope to devices running Marimo by filtering on `DeviceName` or a device group if noise from other Python web servers is a concern.
