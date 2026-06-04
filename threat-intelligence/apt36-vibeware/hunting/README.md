# APT36 VibeWare — Hunting Queries

Proactive hunting queries for the APT36 VibeWare DeskRAT campaign on Linux endpoints. Run manually or schedule in Advanced Hunting.

## Queries

| Query | Description |
|---|---|
| `apt36-full-chain-hunting.kql` | Correlates curl pipeline, autostart drop, and crontab activity per device. Two or more signals is a high-confidence hit. |
| `apt36-hidden-binary-config-dir.kql` | Detects ELF binaries executing with `--hidden` from `.config` directories, and new binaries/scripts written into `.config` subdirs. |
| `apt36-payload-delivery-domains.kql` | Hunts for connections to `bossmaya.xyz`, `chuchuchacha.xyz`, and the hardcoded fallback IP, with detection type labeling per hit. |

## Usage

Start with `apt36-payload-delivery-domains.kql` to surface any historical connections to campaign infrastructure. Follow with `apt36-full-chain-hunting.kql` to identify devices showing multi-stage compromise. Use `apt36-hidden-binary-config-dir.kql` to find implanted binaries on devices that may have been hit before MDE enrollment.
