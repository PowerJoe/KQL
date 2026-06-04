# Marimo RCE — CVE-2026-39987

Detection and hunting rules for **CVE-2026-39987**, a critical pre-authentication remote code execution vulnerability in [Marimo](https://github.com/marimo-team/marimo), a Python reactive notebook framework.

**CVSS v4.0: 9.3 (Critical) — Exploit observed in-the-wild within 9h 41m of disclosure.**

## Vulnerability

Marimo's `/terminal/ws` WebSocket endpoint allocates a PTY and spawns a shell without performing any authentication checks, while other WebSocket routes are protected. A single unauthenticated WebSocket handshake grants full shell access as the Marimo process user — frequently `root` in container deployments.

- **Affected:** marimo < 0.23.0 (edit mode only)
- **Fixed:** marimo 0.23.0+
- **Exposure condition:** Instance running in edit mode (`marimo edit`) — read-only/static deployments are not affected

## Attack chain

1. Attacker sends WebSocket upgrade to `ws://<host>:<port>/terminal/ws`
2. Server accepts handshake with no credential verification
3. PTY allocated, shell forked as Marimo process user
4. Attacker has full interactive shell — credential theft completed in under 3 minutes in observed incidents

## Layout

```
marimo-rce/
├── analytics/                                    # Scheduled detection rules
│   ├── marimo-rce-shell-spawn.kql                    # Shell spawned by Python — highest fidelity
│   ├── marimo-rce-terminal-ws-access.kql             # WebSocket upgrade to /terminal/ws (WAF/proxy logs)
│   ├── marimo-rce-credential-file-access.kql         # SSH keys / cloud tokens read post-exploit
│   └── marimo-rce-outbound-connection.kql            # Unexpected outbound from Python/shell
└── hunting/
    ├── marimo-rce-exploit-chain-hunting.kql          # Correlates all 3 TTPs per device
    └── marimo-rce-post-exploit-discovery.kql         # Discovery commands run under Marimo PTY
```

## Deployment order

1. **Patch first:** Upgrade to marimo 0.23.0+. If immediate patching is not possible, block external access to the Marimo port at the network layer.
2. Enable `marimo-rce-shell-spawn.kql` — no false positives expected in normal Marimo operation.
3. Enable `marimo-rce-terminal-ws-access.kql` if WAF or reverse proxy logs are ingested into Sentinel.
4. Enable `marimo-rce-credential-file-access.kql` and `marimo-rce-outbound-connection.kql`.
5. Run hunting queries daily to surface historical exploitation.

## Platform notes

- `marimo-rce-shell-spawn.kql`, `marimo-rce-credential-file-access.kql`, `marimo-rce-outbound-connection.kql`: require **MDE on Linux** (endpoint enrolled in Defender for Endpoint).
- `marimo-rce-terminal-ws-access.kql`: requires WAF/proxy logs in `CommonSecurityLog` or web server logs in `Syslog`.
- Hunting rules require MDE Linux with process and file event telemetry.

## References

- [Endor Labs — Root in One Request: Marimo's Critical Pre-Auth RCE](https://www.endorlabs.com/learn/root-in-one-request-marimos-critical-pre-auth-rce-cve-2026-39987)
