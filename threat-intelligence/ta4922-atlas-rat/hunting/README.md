# TA4922 — Hunting Queries

Proactive hunting queries for the TA4922 Atlas RAT campaign. Run manually or schedule in Advanced Hunting — not for automated alerting.

## Queries

| Query | Description |
|---|---|
| `ta4922-full-chain-hunting.kql` | Correlates DLL sideloading, C2 connection, and Chrome credential theft per device. Two or more signals is high-confidence compromise. |
| `ta4922-wechat-injection.kql` | Hunts for WeChat.exe spawning suspicious child processes or being launched by unexpected parents — a known TA4922 injection target. |
| `ta4922-payload-hosting-domains.kql` | Surfaces all connections to TA4922 C2 IPs and distribution infrastructure with per-hit malware family labeling. |

## Usage

Start with `ta4922-payload-hosting-domains.kql` to surface any historical infrastructure hits across all three malware families. Follow with `ta4922-full-chain-hunting.kql` to identify devices showing multi-stage compromise. Use `ta4922-wechat-injection.kql` on environments with a significant WeChat user base.
