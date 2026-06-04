# VSCode GitHub Token Theft

Detection and hunting rules for a **VSCode/github.dev webview sandbox escape** disclosed June 2, 2026, enabling silent GitHub token exfiltration via a malicious Jupyter notebook in an attacker-controlled repository.

> **No CVE assigned at time of writing.** Affects VSCode Desktop ≤ v1.97 and VSCode Web (github.dev). Update to v1.98+.

## Vulnerability

VSCode registers `keydown` event handlers on webview iframes without validating the event source. A Jupyter notebook cell containing `<img src="data:foobar" onerror="...">` can dispatch synthetic keyboard events (`dispatchEvent()`) to the host window:

1. **Ctrl+Shift+A** — accepts the extension recommendation notification (`.vscode/extensions.json` in the repo)
2. **Ctrl+F1** — fires a custom keybinding from the now-installed workspace extension

The workspace extension installs silently with `skipPublisherTrust: true`, accesses the VSCode GitHub session token, calls `api.github.com/user/repos`, and exfiltrates the token to an attacker-controlled endpoint. Full private repository access is obtained in a single browser visit.

## Attack chain

| Step | Timing | Observable |
|---|---|---|
| Victim visits attacker repo on github.dev | T+0 | Network connection to github.dev |
| Notebook renders, JS waits | T+0 to T+10s | No observable |
| Ctrl+Shift+A injected — extension dialog accepted | T+10s | No user interaction logged |
| Ctrl+F1 injected — extension keybinding fires | T+10.5s | No user interaction logged |
| Extension accesses GitHub token | T+10.5s | VSCode calls api.github.com/user/repos |
| Token + repo list exfiltrated | T+11s | VSCode connects to external domain |

## Layout

```
vscode-github-token-theft/
├── analytics/
│   ├── vscode-token-theft-workspace-ext-install.kql  # New extension files in VSCode ext dir
│   ├── vscode-token-theft-github-api-enum.kql        # /user/repos calls from VSCode/Node
│   ├── vscode-token-theft-external-exfil.kql         # VSCode calling non-GitHub domains
│   └── vscode-token-theft-extensions-json-drop.kql   # .vscode/extensions.json outside config dir
└── hunting/
    ├── vscode-token-theft-full-chain-hunting.kql      # Correlates all 3 stages per device
    └── vscode-token-theft-ipynb-followed-by-network.kql  # Notebook open → external call <15m
```

## Deployment order

1. Enable `vscode-token-theft-external-exfil.kql` — catches active token exfiltration. Tune the trusted domain list to match your environment's expected VSCode extension sources.
2. Enable `vscode-token-theft-github-api-enum.kql` — catches the repository enumeration step.
3. Enable `vscode-token-theft-extensions-json-drop.kql` — low noise, catches the delivery artifact.
4. Enable `vscode-token-theft-workspace-ext-install.kql` — tune if VSCode is managed centrally and pushes extensions via automation.
5. Run hunting queries daily.

## Mitigation

- **Patch:** Upgrade to VSCode ≥ v1.98.
- **Immediate:** Clear github.dev browser local storage to force token re-authentication.
- **Policy:** Restrict workspace trust — do not open repositories from unknown sources in VSCode Web.

## Tuning note

> **`vscode-token-theft-external-exfil.kql` requires environment-specific tuning.** In developer-heavy environments, VSCode extensions legitimately call third-party APIs (npm registries, telemetry endpoints, AI services, etc.). Add your approved external domains to the `TrustedDomains` list in that rule before enabling automated alerting, or expect significant noise. The `analytics/README.md` contains guidance on what to add.

## References

- [Ammar Askar — GitHub Token Stealing via VSCode Webview](https://blog.ammaraskar.com/github-token-stealing/)
