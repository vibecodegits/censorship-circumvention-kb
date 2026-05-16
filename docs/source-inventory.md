# Source Inventory

Last checked: 2026-05-16

This file tracks public sources to turn into method cards. It should link to sources without copying sensitive operational details.

## GitHub Star List Snapshot

Source: [vibecodegits / Anti Mulla Net](https://github.com/stars/vibecodegits/lists/anti-mulla-net)

The list showed 20 repositories when checked.

| Source | Initial Category | Notes |
| --- | --- | --- |
| [shirokhorshid/shirokhorshid-android](https://github.com/shirokhorshid/shirokhorshid-android) | Psiphon client / CDN fronting | Community Psiphon Android fork with extra controls. |
| [shirokhorshid/psiphon-tunnel-core](https://github.com/shirokhorshid/psiphon-tunnel-core) | Psiphon core / fronted meek | Custom tunnel core used by the Android client. |
| [hanselime/paqet](https://github.com/hanselime/paqet) | Packet ferry / tunnel | Needs source card and architecture review. |
| [patterniha/MITM-DomainFronting](https://github.com/patterniha/MITM-DomainFronting) | MITM helper / domain fronting | Public notes describe local interception plus fronting. Treat cert/MITM requirements carefully. |
| [ShahabSL/twoman](https://github.com/ShahabSL/twoman) | Unknown / needs review | Needs source card. |
| [ajavadinezhad/zyrln](https://github.com/ajavadinezhad/zyrln) | Google infrastructure route | Description claims Google-backed domain-fronting relay. |
| [masterking32/MasterHttpRelayVPN](https://github.com/masterking32/MasterHttpRelayVPN) | Google Apps Script relay | MHR family, Python implementation. |
| [hiddify/Hiddify-Manager](https://github.com/hiddify/Hiddify-Manager) | Management panel / multi-protocol | Broader anti-filtering panel, not a single method. |
| [aliasoblomov/mhr-vps-worker](https://github.com/aliasoblomov/mhr-vps-worker) | VPS worker / MHR variant | Replaces Cloudflare Worker with private Node worker. |
| [therealaleph/MasterHttpRelayVPN-RUST](https://github.com/therealaleph/MasterHttpRelayVPN-RUST) | Google Apps Script relay | Rust port of MHR. |
| [amirshaker000/netlify-relay](https://github.com/amirshaker000/netlify-relay) | Netlify/serverless relay | Needs source card. |
| [denuitt1/mhr-cfw](https://github.com/denuitt1/mhr-cfw) | GAS + Cloudflare Worker relay | Domain-fronted relay through Apps Script and Workers. |
| [selfishblackberry177/sni-spoof](https://github.com/selfishblackberry177/sni-spoof) | SNI spoofing / DPI bypass | Go port of Patterniha SNI spoofing forwarder. |
| [patterniha/MMDF](https://github.com/patterniha/MMDF) | DPI circumvention | Needs source card. |
| [patterniha/paqet](https://github.com/patterniha/paqet) | Packet ferry / tunnel | Fork/mirror; compare with hanselime upstream. |
| [patterniha/cf-scanner](https://github.com/patterniha/cf-scanner) | Scanner tooling | Cloudflare scanning; keep raw findings out of public notes. |
| [patterniha/gfw_resist_tcp_proxy](https://github.com/patterniha/gfw_resist_tcp_proxy) | TCP proxy / DPI resistance | Needs source card. |
| [patterniha/slipstream](https://github.com/patterniha/slipstream) | DNS covert channel | High-performance multi-path covert channel over DNS. |
| [patterniha/dnstt](https://github.com/patterniha/dnstt) | DNS tunnel | dnstt mirror plus plugin work. |
| [patterniha/tun2socks-helps](https://github.com/patterniha/tun2socks-helps) | Client helper | Helper scripts and integration material. |

## Additional Repos From Local Codex Sessions

These were found in older local Codex session files or local repo checkouts and were not all present in the star list snapshot.

| Source | Initial Category | Notes |
| --- | --- | --- |
| [patterniha/MITM-DomainFronting](https://github.com/patterniha/MITM-DomainFronting) | MITM/fronting helper | Early client-app sessions; local helper/MITM architecture. |
| [patterniha/MMDF](https://github.com/patterniha/MMDF) | Fronting/DPI evasion | Referenced in early GUI-DF/MMDF investigation. |
| [selfishblackberry177/sni-spoof](https://github.com/selfishblackberry177/sni-spoof) | SNI spoofing | Go implementation/fork linked to Patterniha ideas. |
| [masterking32/MasterHttpRelayVPN](https://github.com/masterking32/MasterHttpRelayVPN) | Apps Script relay | Original MHR lineage. |
| [therealaleph/MasterHttpRelayVPN-RUST](https://github.com/therealaleph/MasterHttpRelayVPN-RUST) | Apps Script relay client | Rust MHR client; multiple setup/debug sessions. |
| [Kianmhz/GooseRelayVPN](https://github.com/Kianmhz/GooseRelayVPN) | Apps Script + VPS TCP tunnel | Encrypted frames through Apps Script to private exit. |
| [g3ntrix/Shade](https://github.com/g3ntrix/Shade) | Apps Script macOS client | Google Apps Script relay client with SwiftUI wrapper. |
| [shayanb/MoaV](https://github.com/shayanb/MoaV) | Multi-protocol orchestration | Reality, Hysteria2, XHTTP, DNS tunnels, WireGuard/wstunnel, etc. |
| [avaco-cloud/Vercel-XHTTP](https://github.com/avaco-cloud/Vercel-XHTTP) | Vercel XHTTP relay | Edge Function relay to Xray backend. |
| [powerofp/vercelmasterhttp](https://github.com/powerofp/vercelmasterhttp) | Vercel/MHR relay | Vercel-oriented MHR-style project. |
| [amirshaker000/netlify-relay](https://github.com/amirshaker000/netlify-relay) | Netlify XHTTP relay | Local tests, May 10 working report, May 15 429 debug. |
| [aliasoblomov/mhr-vps-worker](https://github.com/aliasoblomov/mhr-vps-worker) | Private VPS worker | Compatible with MHR Apps Script shape in local review. |
| [ShahabSL/twoman](https://github.com/ShahabSL/twoman) | Host-preserving reverse relay | Public host + hidden reverse agent model. |
| [serverless-dns/serverless-dns](https://github.com/serverless-dns/serverless-dns) | DNS resolver/serverless | Seen in provider exploration. |
| [ImpostorKeanu/front_brute](https://github.com/ImpostorKeanu/front_brute) | Fronting/scanner tool | Seen in relay experiment session. |
| [XTLS/Xray-core](https://github.com/XTLS/Xray-core) | Core proxy engine | XHTTP, freedom fragmentation, VLESS/REALITY substrate. |
| [dima-u/SwiftyXrayCore](https://github.com/dima-u/SwiftyXrayCore) | iOS/macOS client integration | Seen during iOS/client discussion. |
| [dima-u/SwiftyXrayKit](https://github.com/dima-u/SwiftyXrayKit) | iOS/macOS client integration | Seen during iOS/client discussion. |
| [MHSanaei/3x-ui](https://github.com/MHSanaei/3x-ui) | Xray panel/origin management | Home origin and backend management. |
| [cloudflare/cloudflared](https://github.com/cloudflare/cloudflared) | Tunnel infrastructure | Used as origin exposure/control-plane component. |

## Current Thread Sources To Convert

| Source | Category | Status |
| --- | --- | --- |
| Shared ChatGPT transcript on PLC/CDN protocols | Background analysis | Summarized in `findings/2026-05-current-thread.md`. |
| X post by `@PawnToPromotion` about Shir-o-Khorshid CDN fronting | Psiphon/CDN fronting | Summarized; screenshots reviewed locally. |
| `INTERNETFORIRAN` Telegram posts around 964 and latest scan updates | Akamai/Fastly field reports | Summarized without raw IP lists. |
| `projectXhttp` Telegram tutorial around Psiphon + local helper | MITM helper / Psiphon | Summarized at architecture level. |
| `xsfilterrnet/3425` Telegram post | Serverless NekoBox + v2rayNG | Summarized as Google-collateral plus TLS fragmentation. |
