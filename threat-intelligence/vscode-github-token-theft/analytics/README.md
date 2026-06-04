# VSCode GitHub Token Theft — Analytics Rules

Scheduled detection rules for the VSCode webview sandbox escape / GitHub token theft attack.

## Rules

| Rule | Severity | MITRE | Description |
|---|---|---|---|
| `vscode-token-theft-external-exfil.kql` | 🔴 Critical | T1041, T1552.007 | VSCode/Node connecting to a non-GitHub/non-Microsoft external domain |
| `vscode-token-theft-github-api-enum.kql` | 🔴 High | T1087, T1083 | High-frequency /user/repos calls from VSCode/Node — token in use |
| `vscode-token-theft-workspace-ext-install.kql` | 🔴 High | T1059.007, T1204.001 | New extension package.json written to the VSCode extensions directory |
| `vscode-token-theft-extensions-json-drop.kql` | 🟠 Medium | T1204.001, T1566.002 | .vscode/extensions.json created outside the user config path |

## Tuning notes

- `vscode-token-theft-external-exfil.kql` — extend `TrustedDomains` with any internal npm/extension registries or approved third-party services your developers use. This rule may be noisy without tuning in environments with many VSCode extensions that call external APIs.
- `vscode-token-theft-github-api-enum.kql` — the 3-request threshold within 5 minutes is conservative. Lower to 1 for high-security environments; raise if CI tooling runs in VSCode context.
