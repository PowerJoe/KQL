# APT36 VibeWare — Analytics Rules

Scheduled detection rules for the APT36 VibeWare DeskRAT campaign. All rules target **Linux endpoints** enrolled in MDE.

## Rules

| Rule | Severity | MITRE | Description |
|---|---|---|---|
| `apt36-c2-websocket-connection.kql` | 🔴 Critical | T1071.001, T1571 | Connection to C2 domain/IP — confirmed compromise |
| `apt36-autostart-desktop-persistence.kql` | 🔴 High | T1547.013 | .desktop file created in ~/.config/autostart/ |
| `apt36-crontab-reboot-persistence.kql` | 🔴 High | T1053.003 | crontab invocation or cron spool file write |
| `apt36-bashrc-startup-injection.kql` | 🔴 High | T1546.004 | .bashrc or startup.sh modified in .config |
| `apt36-desktop-file-curl-pipe.kql` | 🔴 High | T1059.004, T1105 | bash running curl with base64/bzip2 decode pipeline |
| `apt36-ip-recon-from-script-engine.kql` | 🟠 Medium | T1016 | curl/script engine querying external IP lookup services |

## Tuning notes

- `apt36-ip-recon-from-script-engine.kql` — developer tooling and cloud-init scripts legitimately call `api.ipify.org`. Tune by adding known service account names or device groups to an exclusion list.
- `apt36-desktop-file-curl-pipe.kql` — CI/CD agents may legitimately use curl pipelines. Limit to interactive user sessions or non-build-agent device groups.
