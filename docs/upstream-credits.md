# Upstream Credits And Appreciation

Last reviewed: 2026-05-28

Names first. VibeCodeGit VPN 2.0 and this knowledge base stand on public work from builders who made hard censorship-resistance ideas visible, testable, and reusable. We applaud these projects and keep their names at the front so the credit does not get buried behind our own notes.

This page credits both kinds of upstream work:

- Projects directly used or modeled in the VibeCodeGit VPN 2.0 app architecture.
- Projects studied by the broader censorship-circumvention KB because they shaped method cards, comparison models, or implementation choices.

## Core VibeCodeGit VPN 2.0 Stack

| Project | Credit |
| --- | --- |
| [XTLS/Xray-core](https://github.com/XTLS/Xray-core) | Core proxy engine behind Xray/VLESS/Reality/XHTTP-style client paths. |
| [dima-u/SwiftyXrayKit](https://github.com/dima-u/SwiftyXrayKit) | iOS/macOS bridge that lets the PacketTunnel run Xray/tun2socks as a real device tunnel. |
| [dima-u/SwiftyXrayCore](https://github.com/dima-u/SwiftyXrayCore) | Packaged Xray core used by the Swift PacketTunnel stack. |
| [Kianmhz/GooseRelayVPN](https://github.com/Kianmhz/GooseRelayVPN) | Main inspiration for the encrypted batch/frame relay through Apps Script and a controlled exit. |
| [masterking32/MasterDnsVPN](https://github.com/masterking32/MasterDnsVPN) | DNS tunnel rescue-transport lead, especially resolver balancing and lossy-link behavior. |
| [patterniha/dnstt](https://github.com/patterniha/dnstt) | DNS tunnel baseline using DNS queries/responses as the constrained transport. |
| [patterniha/slipstream](https://github.com/patterniha/slipstream) | DNS covert-channel performance experiment with QUIC-style stream ideas. |
| [shirokhorshid/psiphon-tunnel-core](https://github.com/shirokhorshid/psiphon-tunnel-core) | Psiphon/fronted-meek core lineage and CDN candidate-scanning model. |
| [shirokhorshid/shirokhorshid-android](https://github.com/shirokhorshid/shirokhorshid-android) | Productized Psiphon/CDN-fronting client reference. |
| [MHSanaei/3x-ui](https://github.com/MHSanaei/3x-ui) | Self-managed Xray panel/user manager and mixed/SOCKS helper surface. |
| [shayanb/MoaV](https://github.com/shayanb/MoaV) | Multi-protocol orchestration and XDNS reference point. |
| [hiddify/Hiddify-Manager](https://github.com/hiddify/Hiddify-Manager) and [hiddify/hiddify-app](https://github.com/hiddify/hiddify-app) | Mature anti-filtering management and client UX references. |
| [SagerNet/sing-box](https://github.com/SagerNet/sing-box) | Modern multi-protocol client/core reference, especially for native TLS spoofing research. |
| [cloudflare/cloudflared](https://github.com/cloudflare/cloudflared), Cloudflare Workers, and Cloudflare Tunnel | Operational relay, Worker, and origin-exposure substrate studied by the KB. |
| Google Apps Script | High-collateral HTTPS forwarder used as a public-cloud relay carrier. |
| Apple SwiftUI and NetworkExtension | App and PacketTunnel platform surface for the iOS product. |

## Google, Apps Script, And Relay Lineage

| Project | Credit |
| --- | --- |
| [masterking32/MasterHttpRelayVPN](https://github.com/masterking32/MasterHttpRelayVPN) | Original MHR-style Google Apps Script relay family. |
| [therealaleph/MasterHttpRelayVPN-RUST](https://github.com/therealaleph/MasterHttpRelayVPN-RUST) | Rust MHR client lineage with resilience and packaging improvements. |
| [denuitt1/mhr-cfw](https://github.com/denuitt1/mhr-cfw) | Apps Script plus Cloudflare Worker relay variant. |
| [aliasoblomov/mhr-vps-worker](https://github.com/aliasoblomov/mhr-vps-worker) | Private VPS worker variant compatible with MHR-style request shapes. |
| [g3ntrix/Shade](https://github.com/g3ntrix/Shade) | Apps Script macOS client lineage and SwiftUI wrapper reference. |
| [powerofp/vercelmasterhttp](https://github.com/powerofp/vercelmasterhttp) | Vercel-oriented MHR-style relay project. |
| [ajavadinezhad/zyrln](https://github.com/ajavadinezhad/zyrln) | Google-infrastructure relay lead. |
| [avaco-cloud/Vercel-XHTTP](https://github.com/avaco-cloud/Vercel-XHTTP) | Vercel XHTTP edge-relay pattern. |
| [amirshaker000/netlify-relay](https://github.com/amirshaker000/netlify-relay) | Netlify XHTTP relay pattern and provider-limit evidence. |
| [ShahabSL/twoman](https://github.com/ShahabSL/twoman) | Host-preserving public-host/hidden-agent relay model. |

## DNS, DPI, Fronting, And Scanner Research

| Project | Credit |
| --- | --- |
| [serverless-dns/serverless-dns](https://github.com/serverless-dns/serverless-dns) | Serverless DNS resolver reference from provider research. |
| [patterniha/MITM-DomainFronting](https://github.com/patterniha/MITM-DomainFronting) | Local MITM/domain-fronting helper architecture. |
| [patterniha/MMDF](https://github.com/patterniha/MMDF) | DPI/fronting method lead. |
| [patterniha/SNI-Spoofing](https://github.com/patterniha/SNI-Spoofing) | Original fake ClientHello/SNI spoofing lead. |
| [therealaleph/sni-spoofing-rust](https://github.com/therealaleph/sni-spoofing-rust) | Rust port with clearer platform and integration notes. |
| [aleskxyz/SNI-Spoofing-Go](https://github.com/aleskxyz/SNI-Spoofing-Go) | Go implementation in the SNI spoofing family. |
| [selfishblackberry177/sni-spoof](https://github.com/selfishblackberry177/sni-spoof) | Go port/fork linked to Patterniha SNI-spoofing ideas. |
| [hossein8360/cdn-ip-finder](https://github.com/hossein8360/cdn-ip-finder) | CDN scanner tooling reference. |
| [seramo/sni-scanner](https://github.com/seramo/sni-scanner) | SNI/CDN scanner tooling reference. |
| [patterniha/cf-scanner](https://github.com/patterniha/cf-scanner) | Cloudflare scanner tooling reference. |
| [ImpostorKeanu/front_brute](https://github.com/ImpostorKeanu/front_brute) | Fronting/scanner tool seen during relay experiments. |
| [hanselime/paqet](https://github.com/hanselime/paqet) and [patterniha/paqet](https://github.com/patterniha/paqet) | Packet-ferry/tunnel research leads. |
| [patterniha/gfw_resist_tcp_proxy](https://github.com/patterniha/gfw_resist_tcp_proxy) | TCP/DPI resistance proxy lead. |
| [patterniha/QQ-Tunnel](https://github.com/patterniha/QQ-Tunnel) and [patterniha/QS-Tunnel](https://github.com/patterniha/QS-Tunnel) | DNS-query tunnel leads. |
| [patterniha/tun2socks-helps](https://github.com/patterniha/tun2socks-helps) | Client-helper and integration material. |

## Panels, Clients, And Orchestration

| Project | Credit |
| --- | --- |
| [throneproj/Throne](https://github.com/throneproj/Throne) | sing-box GUI client reference. |
| [g3ntrix/Cloak](https://github.com/g3ntrix/Cloak) | macOS CDN profile client reference. |
| [iampedii/WhiteDNS](https://github.com/iampedii/WhiteDNS) | Android DNS tunnel client reference. |
| [ztmwtf/bia-pain-bache-BPB-Worker-Panel](https://github.com/ztmwtf/bia-pain-bache-BPB-Worker-Panel), [vahitoo/bia-pain-bache-BPB-Worker-Panel](https://github.com/vahitoo/bia-pain-bache-BPB-Worker-Panel), and [NiREvil/bia-pain-bache](https://github.com/NiREvil/bia-pain-bache) | BPB Worker/Pages panel family and Cloudflare profile-generation reference. |
| [patterniha/Serverless-for-Iran](https://github.com/patterniha/Serverless-for-Iran) | Serverless/Xray config surface reference. |
| [libertyir/AzadrahPy](https://github.com/libertyir/AzadrahPy) | Review-backlog lead from the public star refresh. |
| [theermia/BaleTunnel](https://github.com/theermia/BaleTunnel) and [kookoo1sabzy/BaleVPN](https://github.com/kookoo1sabzy/BaleVPN) | Messaging-app collateral tunnel leads. |

## Credit Rule

When a new method card, finding, or app note borrows from a public project, add the project to this file before or alongside the new KB entry. If a project directly changes VibeCodeGit VPN 2.0 architecture, also mention it in the VibeCodeGit VPN 2.0 KB credits section.
