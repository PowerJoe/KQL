# Marimo RCE — Hunting Queries (CVE-2026-39987)

Proactive hunting queries for CVE-2026-39987. Run manually or schedule in Advanced Hunting — not for automated alerting.

## Queries

| Query | Description |
|---|---|
| `marimo-rce-exploit-chain-hunting.kql` | Correlates shell spawn from Python, credential file access, and outbound C2 connection per device. Two or more signals is high-confidence exploitation. |
| `marimo-rce-post-exploit-discovery.kql` | Detects system discovery commands (`id`, `whoami`, `uname`, `cat /etc/passwd`, etc.) executed in a shell that traces back to a Python/Marimo parent — hands-on-keyboard indicator. |

## Usage

Start with `marimo-rce-exploit-chain-hunting.kql` over a 7-day window to identify devices with multi-stage compromise signals. Use `marimo-rce-post-exploit-discovery.kql` to identify interactive attacker activity and establish a timeline for incident response scoping.
