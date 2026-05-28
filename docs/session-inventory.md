# Local Codex Session Inventory

Last reviewed: 2026-05-27

Source: local Codex session files under `~/.codex/sessions` and `~/.codex/archived_sessions`, plus generated workspace artifacts under `~/Documents/Codex`.

This inventory is intentionally public-safe. It records the research value of each session without exposing credentials, live hostnames that are not already public, raw configs, UUIDs, or active private infrastructure details.

## Relevant Research Sessions

| Date | Thread | KB Value | Added To |
| --- | --- | --- | --- |
| 2026-04-20 | Build full-fledged app | MITM-DomainFronting, MMDF, local GUI-DF/Mac/iPhone limitations, hardcoded Google edge behavior. | `methods/mitm-domain-fronting.md` |
| 2026-04-21 | Resume app build | VibeCodeGit VPN packaging, pinned Google edge support, Apps Script quick-start packaging. | `findings/2026-04-20-to-21-client-app-build.md` |
| 2026-04-24 | Prepare repo for work | `MasterHttpRelayVPN-RUST`, local Xray upstream SOCKS role, direct SOCKS vs local Xray patterns. | `methods/google-apps-script-relays.md` |
| 2026-04-25 | Deploy MoaV on Google Cloud | MoaV review, Netlify/Vercel/Fastly/Cloud Run relay experiments, 100 MiB transfer testing, upstream reset findings. | `findings/2026-04-25-relay-experiments.md` |
| 2026-04-27 | Clean panel tunnel routes | Cloudflare Tunnel + 3x-ui routing constraints; GooseRelayVPN as separate workaround. | `methods/self-hosted-origin-and-cloudflare-tunnel.md`, `methods/google-apps-script-relays.md` |
| 2026-04-27 | Find Google script daily limit | Google service relay viability and Apps Script quota framing. | `findings/2026-04-28-provider-research.md` |
| 2026-04-28 | Find edge relay service | Edge/CDN relay provider matrix: Gcore, CloudFront, Azure Front Door, Bunny, Fastly, Cloudflare caveats. | `findings/2026-04-28-provider-research.md` |
| 2026-04-28 | Find Fastly worker domain support | Fastly fronting distinction: own Fastly service vs arbitrary third-party Fastly host. | `methods/fastly-compute-xhttp.md` |
| 2026-04-30 | Review GitHub projects | Compared MHR-CFW, MasterHttpRelayVPN-RUST, Shade, GooseRelayVPN; live Worker/GAS/Goose path checks. | `methods/google-apps-script-relays.md` |
| 2026-05-03 | Assess repo compatibility | `MasterHttpRelayVPN-RUST` compatibility with `mhr-vps-worker`; shared request/response shape. | `methods/google-apps-script-relays.md` |
| 2026-05-04 | Find Netlify SNI requirements | Netlify Host/SNI must route through a domain Netlify can terminate/serve. | `methods/netlify-xhttp-relay.md` |
| 2026-05-10 | Review Telegram chats | Telegram evidence report, DNS bootstrap, Netlify XHTTP, Shecan/V2Box placement, fragmentation signals. | `findings/2026-05-10-telegram-research.md` |
| 2026-05-10 | Check mhr-vps-worker conflict | Node worker on VPS as MHR worker replacement; service separation from 3x-ui. | `methods/google-apps-script-relays.md` |
| 2026-05-10 | Review VPN audit | VibeCodeGit VPN security hardening: TLS verification, proxy cleanup, secret redaction, lifecycle cleanup. | `findings/2026-05-10-client-security-audit.md` |
| 2026-05-10 | Review X post | Twoman host-preserving relay and hidden-server/public-host model. | `methods/twoman-host-preserving-relay.md` |
| 2026-05-10 | Find upstream SOCKS | MHR local upstream SOCKS/Xray semantics; warning against publishing no-auth SOCKS. | `methods/self-hosted-origin-and-cloudflare-tunnel.md` |
| 2026-05-12 | Patch Hyper-V and 3X-UI | Operational maintenance for self-managed origin/panel infrastructure: 3x-ui, Xray, cloudflared, WARP, kernel patching. | `methods/self-hosted-origin-and-cloudflare-tunnel.md` |
| 2026-05-15 | Debug Netlify XHTTP fronting | Isolated Netlify 429 throttling vs working backend; upstream relay comparison; disposable relay conclusion. | `findings/2026-05-15-netlify-xhttp-debug.md` |
| 2026-05-15 | Read shared chat | Shir-o-Khorshid/Psiphon CDN fronting, Akamai/Fastly field reports, NekoBox+v2rayNG serverless fragmentation. | `findings/2026-05-current-thread.md` |
| 2026-05-20 to 2026-05-22 | Build/test VibeCodeGit VPN 2.0 | iOS PacketTunnel, Xray/tun2socks, Goose encrypted relay batches, Apps Script forwarder, Worker/VPS relay, DNS and long-polling pitfalls, TestFlight packaging. | `vibecodegit-vpn-2.0-knowledge-base.md`, `vibecodegit-vpn-2.0-architecture-and-codebase.md`, `findings/2026-05-27-vibecodegit-vpn-lessons.md`, `methods/client-packaging-and-packet-tunnel.md`, `methods/google-apps-script-relays.md` |
| 2026-05-26 | Repair MoaV MasterDNS/user-management work | MoaV web UI/user sync risk when adding/removing transports; MasterDNS must touch profiles, subscriptions, and generated users coherently. | `methods/multi-protocol-orchestration.md`, `methods/dns-bootstrap-and-tunnels.md` |
| 2026-05-26 to 2026-05-27 | Inspect BPB/Cloudflare Worker state | BPB panel settings can coexist with unrelated relay Workers; recover/deploy as separate Worker to avoid breaking the VibeCodeGit relay. | `methods/multi-protocol-orchestration.md` |
| 2026-05-27 | Refresh KB from stars and repo metadata | 39 public starred repos, current release/push metadata, new Bale/MasterDNS/WhiteDNS/SNI-Go/BPB/Throne families. | `source-inventory.md`, `findings/2026-05-27-star-and-repo-refresh.md` |

## Non-Research Or Low-Relevance Sessions

These sessions exist locally but are not central to this censorship-circumvention KB:

- 2026-04-26 `Troubleshoot SSH to Ubuntu VM` - mostly local admin and communication style; only minor 3x-ui/Vercel-XHTTP links.
- 2026-04-28 `Move conversation history` - useful only as provenance for local session access and why active Codex DBs should not be iCloud-synced.
- 2026-05-03 `Build secure Markeign website` - company website deployment, not circumvention research.
- 2026-05-03 `Audit Wix site UX and SEO` - unrelated website/SEO work.
- 2026-05-15 `Locate whistler packing list` - unrelated Reminders task.

## Open Follow-Up

- Turn each important repo into a source card with code references.
- Separate live operational deployments from reusable architecture.
- Add an evidence ledger with "verified locally", "reported in Telegram", "source-code confirmed", and "current field status" columns.
- Turn newly added Bale, MasterDNS, WhiteDNS, BPB, Serverless-for-Iran, Cloak, Throne, and scanner leads into source cards as time allows.
