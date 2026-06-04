# APT36 VibeWare — DeskRAT Campaign

Detection and hunting rules for **APT36 (Transparent Tribe)** campaign **VibeWare**, targeting Indian military and defense personnel on Linux endpoints. The campaign delivers a Golang-based RAT ("DeskRAT") via weaponized `.desktop` files distributed over WhatsApp and email, using Indian military procurement lures (T-72/T-90 tank modernization).

> **Platform note:** These rules target Linux endpoints enrolled in Microsoft Defender for Endpoint (MDE). Rules use `DeviceProcessEvents`, `DeviceFileEvents`, and `DeviceNetworkEvents` — there are no registry events on Linux.

## Attack chain

1. **Lure delivery** — `.desktop` file masquerading as a PDF (Exec field hides bash payload, `Icon=application-pdf`). Delivered via WhatsApp/email.
2. **Initial execution** — desktop environment launches the file; `bash -c` runs a fractional sleep (`sleep 0.18`) then a nested Base64/bzip2 decode pipeline via `curl`.
3. **Staged download** — `bossmaya.xyz/download.php?file=client.txt` delivers `stage3.txt` (Golang ELF, DeskRAT).
4. **Decoy** — Firefox opens a legitimate Indian government press release (pib.gov.in) to distract the victim.
5. **Triple persistence** — XDG autostart (`~/.config/autostart/system-backup.desktop`), crontab `@reboot`, `.bashrc` source injection.
6. **C2 beacon** — DeskRAT calls `api.ipify.org` for external IP, then connects via WebSocket (`ws://chuchuchacha.xyz:8080/ws`) with ChaCha20 encryption. Fallback IP: `85.137.249.243`.
7. **RAT capabilities** — system recon, file browsing/exfiltration in chunks, remote execute (`.desktop`, `.sh`, `.py`, ELF), 30-second heartbeat.

## Layout

```
apt36-vibeware/
├── analytics/                                  # Scheduled detection rules
│   ├── apt36-c2-websocket-connection.kql           # C2 domain/IP hit — highest fidelity
│   ├── apt36-autostart-desktop-persistence.kql     # .desktop in ~/.config/autostart/
│   ├── apt36-crontab-reboot-persistence.kql        # @reboot cron persistence
│   ├── apt36-bashrc-startup-injection.kql          # .bashrc modified to source startup.sh
│   ├── apt36-desktop-file-curl-pipe.kql            # curl decode pipeline from bash
│   └── apt36-ip-recon-from-script-engine.kql       # IP lookup before C2 beacon
└── hunting/
    ├── apt36-full-chain-hunting.kql                # Correlates all TTPs per device
    ├── apt36-hidden-binary-config-dir.kql          # ELF with --hidden from .config dir
    └── apt36-payload-delivery-domains.kql          # Delivery infra and C2 domain hits
```

## Deployment order

1. Enable `apt36-c2-websocket-connection.kql` immediately — any hit is confirmed C2.
2. Enable the three persistence rules (`autostart-desktop`, `crontab-reboot`, `bashrc-injection`) — low false-positive risk.
3. Enable `apt36-desktop-file-curl-pipe.kql` — tune out legitimate CI/CD curl pipelines.
4. Enable `apt36-ip-recon-from-script-engine.kql` — tune out developer tooling that queries ipify.
5. Run hunting queries daily.

## Network IOCs

| Indicator | Type | Purpose |
|---|---|---|
| `chuchuchacha.xyz` | Domain | C2 WebSocket endpoint |
| `85.137.249.243` | IP | C2 hardcoded fallback (AlexHost S.r.l., ASN 200019) |
| `bossmaya.xyz` | Domain | Staged payload delivery |
| `ws://chuchuchacha.xyz:8080/ws` | URL | DeskRAT C2 endpoint |

## Attribution

APT36 / Transparent Tribe — Pakistan-linked threat actor with a history of targeting Indian government, military, and defense sector. Build path artifact (`D:/bossmaya/our/newlinuxblkul/client/main.go`) and domain handle align with prior campaign infrastructure.

## References

- [Medium — Pakistan's APT36 VibeWare Targets Indian Military Infrastructure](https://medium.com/@tarunrd77/pakistans-apt36-vibeware-targets-indian-military-infrastructure-75a853437c03)
