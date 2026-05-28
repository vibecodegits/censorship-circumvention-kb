# Findings: Star And Repository Refresh, 2026-05-27

Evidence level: `L2-L3`

Sources:

- [vibecodegits public stars](https://github.com/vibecodegits?tab=stars)
- GitHub repository metadata and latest-release metadata for starred and previously used repos.

## What Changed Since The Initial KB

The original KB was built from a narrower Anti Mulla Net star-list snapshot and earlier local sessions. The current public star list has 39 repositories and adds several clusters that should now be first-class KB leads:

- DNS tunneling: MasterDnsVPN and WhiteDNS.
- Messaging-app collateral: BaleTunnel and BaleVPN.
- SNI/DPI tooling: SNI-Spoofing-Go, Cloak, sni-scanner.
- Worker/serverless panels: BPB forks and Serverless-for-Iran.
- Client/orchestration: Throne, current MoaV releases, Hiddify/3x-ui/sing-box adjacent tooling.

## Notable Current Releases

| Source | Latest release checked | KB interpretation |
| --- | --- | --- |
| [shayanb/MoaV](https://github.com/shayanb/MoaV) | `v1.7.8`, 2026-05-25 | Orchestration layer is actively evolving around DNS resilience, pinned Xray builds, and restricted-network build reliability. |
| [masterking32/MasterDnsVPN](https://github.com/masterking32/MasterDnsVPN) | `v2026.05.10.180256-27c7e11`, 2026-05-10 | DNS tunnel family now has a newer high-performance branch with ARQ, resolver balancing, and MTU tuning claims. |
| [iampedii/WhiteDNS](https://github.com/iampedii/WhiteDNS) | `1.5.1`, 2026-05-19 | Android client packaging for MasterDNS/StormDNS-style tunnels; source-available, not broadly redistributable. |
| [Kianmhz/GooseRelayVPN](https://github.com/Kianmhz/GooseRelayVPN) | `v1.7.1`, 2026-05-23 | Apps Script forwarder error handling matters; clients should distinguish relay errors from encrypted batch payloads. |
| [therealaleph/MasterHttpRelayVPN-RUST](https://github.com/therealaleph/MasterHttpRelayVPN-RUST) | `v1.9.35`, 2026-05-25 | Large downloads and slow exit nodes need stream-specific timeout behavior and safe fallback. |
| [hiddify/Hiddify-Manager](https://github.com/hiddify/Hiddify-Manager) | `v12.3.1`, 2026-05-26 | Active multi-protocol panel; track as orchestration, not a single transport. |
| [MHSanaei/3x-ui](https://github.com/MHSanaei/3x-ui) | `v3.1.0`, 2026-05-23 | Active Xray panel; useful for controlled origins and users. |
| [SagerNet/sing-box](https://github.com/SagerNet/sing-box) | `v1.13.12`, 2026-05-15 | Important client/core substrate, especially where native TLS spoof knobs exist. |
| [XTLS/Xray-core](https://github.com/XTLS/Xray-core) | `v26.3.27`, 2026-03-27 | Latest release found was older than latest repo pushes; continue tracking repository activity separately from releases. |

## Previously Used Repos Checked

| Source | Current status checked | Notes |
| --- | --- | --- |
| [Kianmhz/GooseRelayVPN](https://github.com/Kianmhz/GooseRelayVPN) | Pushed 2026-05-28 UTC | Still active; central to VibeCodeGit VPN 2.0 relay thinking. |
| [g3ntrix/Shade](https://github.com/g3ntrix/Shade) | Pushed 2026-05-15 UTC | Apps Script macOS client lineage. |
| [shayanb/MoaV](https://github.com/shayanb/MoaV) | Pushed 2026-05-27 UTC | Active; now promoted to method card. |
| `avaco-cloud/Vercel-XHTTP` | GitHub API returned no public repo metadata | Keep local notes, but do not cite as current until a public repo is available. |
| [powerofp/vercelmasterhttp](https://github.com/powerofp/vercelmasterhttp) | Pushed 2026-04-28 UTC | Vercel/MHR variant. |
| [serverless-dns/serverless-dns](https://github.com/serverless-dns/serverless-dns) | Pushed 2026-05-06 UTC | DNS resolver/serverless substrate. |
| [ImpostorKeanu/front_brute](https://github.com/ImpostorKeanu/front_brute) | Pushed 2020-08-17 UTC | Scanner idea remains useful, repo appears old. |
| [dima-u/SwiftyXrayCore](https://github.com/dima-u/SwiftyXrayCore) | Pushed 2026-05-13 UTC | iOS/macOS Xray integration lead. |
| [dima-u/SwiftyXrayKit](https://github.com/dima-u/SwiftyXrayKit) | Pushed 2026-05-13 UTC | PacketTunnel/Xray wrapper lead. |
| [MHSanaei/3x-ui](https://github.com/MHSanaei/3x-ui) | Pushed 2026-05-28 UTC | Origin/user management remains active. |
| [cloudflare/cloudflared](https://github.com/cloudflare/cloudflared) | Pushed 2026-05-27 UTC | Tunnel infrastructure remains active. |
| [SagerNet/sing-box](https://github.com/SagerNet/sing-box) | Pushed 2026-05-26 UTC | Core client substrate remains active. |

## KB Actions Taken

- Added method cards for messaging-app collateral tunnels, multi-protocol orchestration/panels, and native client packaging/PacketTunnel integration.
- Updated DNS, Apps Script, and SNI spoofing method cards with new repos and current upstream signals.
- Updated source inventory with the current all-star snapshot and release table.
- Added VibeCodeGit VPN lessons as a public-safe finding.

## Public-Safe Boundary

Repository metadata and architecture-level summaries are fine for the public KB. Raw working configs, IP/SNI scan results, UUIDs, private relays, account IDs, tokens, and family deployment details stay out.
