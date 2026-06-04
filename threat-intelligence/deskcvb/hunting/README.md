# DesckVB RAT — Hunting Queries

Proactive hunting queries for the DesckVB RAT campaign. Run manually or schedule in Advanced Hunting — not intended for automated alerting.

## Queries

| Query | Description |
|---|---|
| `deskcvb-full-chain-hunting.kql` | Correlates three TTPs (JS from Public, proxy exec, NVIDEO Run key) per device over 7 days. Two or more signals is a high-confidence hit. |
| `deskcvb-public-folder-staging.kql` | Detects two or more script/staging files dropped into C:\Users\Public\ within one hour by a non-standard process. |
| `deskcvb-payload-delivery-domains.kql` | Hunts for connections to delivery infrastructure and geolocation checks (ipapi.co) made by script engines before payload detonation. |

## Usage

Start with `deskcvb-full-chain-hunting.kql` for a quick triage of already-compromised devices. Follow up with `deskcvb-public-folder-staging.kql` for earlier-stage detections where the RAT may not yet have established persistence. Use `deskcvb-payload-delivery-domains.kql` to identify devices that accessed delivery infrastructure but may not have executed the payload.
