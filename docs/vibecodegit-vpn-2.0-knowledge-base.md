# VibeCodeGit VPN 2.0 Knowledge Base

Last reviewed: 2026-05-28

Credits first: [XTLS/Xray-core](https://github.com/XTLS/Xray-core), [SwiftyXrayKit](https://github.com/dima-u/SwiftyXrayKit), [SwiftyXrayCore](https://github.com/dima-u/SwiftyXrayCore), [GooseRelayVPN](https://github.com/Kianmhz/GooseRelayVPN), [MasterDnsVPN](https://github.com/masterking32/MasterDnsVPN), [dnstt](https://github.com/patterniha/dnstt), [slipstream](https://github.com/patterniha/slipstream), [Shir-o-Khorshid Psiphon core](https://github.com/shirokhorshid/psiphon-tunnel-core), [3x-ui](https://github.com/MHSanaei/3x-ui), [MoaV](https://github.com/shayanb/MoaV), [Hiddify](https://github.com/hiddify/Hiddify-Manager), [sing-box](https://github.com/SagerNet/sing-box), [cloudflared](https://github.com/cloudflare/cloudflared), Cloudflare Workers, Google Apps Script, and Apple NetworkExtension/SwiftUI. We applaud the upstream builders who made the transport, tunnel, relay, and product ideas possible. The longer ledger is in [Upstream Credits And Appreciation](upstream-credits.md).

## Scope

This is a public-safe knowledge base for the VibeCodeGit VPN 2.0 Codex project. It describes architecture, code organization, evidence, and lessons without publishing live deployment URLs, active credentials, generated configs, QR codes, private relay hostnames, account identifiers, or one-click instructions for fragile working paths.

The source project inspected locally is an iOS app and PacketTunnel codebase. The public repo should publish the map, not the private runtime material.

## Current Project Shape

VibeCodeGit VPN 2.0 is an iOS VPN app with five visible transport families:

| Family | Current state | KB handling |
| --- | --- | --- |
| Vibe / Xray Core | Live PacketTunnel path through SwiftyXrayKit, Xray, and tun2socks. Accepts Xray share links or raw Xray JSON. | Track as the default native tunnel route. |
| Google Script Relay | Live PacketTunnel path through local Goose SOCKS and an Apps Script or Worker/VPS relay chain. | Track as an encrypted collateral-carrier route; Apps Script must stay a forwarder, not a plaintext VPN brain. |
| DNS Tunnel | UI/config surface exists. MoaV XDNS can ride the Xray path; MasterDNS, DNSTT, and Slipstream need native PacketTunnel-safe engines before becoming main transports. | Track as rescue/control-plane work and app-side probe work until the native engines are linked. |
| Pure MITM / Domain Fronting | Separated in the UI and model, but the packet transport engine is not linked into the current PacketTunnel build. | Track as a method family, not a live button. |
| Psiphon / Shir-o-Khorshid Fronting | UI/config surface exists; native Psiphon tunnel is disabled in the shipping PacketTunnel build until a lighter iOS-safe core is ready. | Track fronting scans as candidate discovery, not a direct transport tab. |

## Durable Architecture Lesson

The app is strongest when it treats transports as interchangeable lanes behind one native device tunnel:

```text
User apps -> iOS PacketTunnel -> local core or SOCKS bridge -> collateral carrier -> controlled egress
```

That shape avoids teaching users to juggle local proxies, browser settings, or raw configs. It also makes cleanup, DNS behavior, entitlements, and lifecycle state first-order security features.

## Key Knowledge

- The Connect button now starts a real `NETunnelProviderManager` profile and PacketTunnel extension instead of pretending a local proxy is device-wide VPN.
- Xray mode is the cleanest native path today because SwiftyXrayKit handles Xray plus tun2socks inside the PacketTunnel.
- The Apps Script route is safest when the phone encrypts Goose batches locally and the Apps Script only forwards opaque payloads.
- DNS can make the VPN appear connected while traffic stalls. DNS needs caching, bypass routes, or a purpose-built DNS transport rather than blocking every lookup on a slow relay.
- Discovery panels should feed candidate stores. They should not be treated as transport buttons or aggressive phone-side scanners.
- User-facing setup should expose the fewest safe fields. Runtime auth, tunnel keys, route mode, and MTU should be generated, baked into test builds, or managed by a secure provisioning flow.

## Public-Safe Evidence

| Evidence | Value |
| --- | --- |
| `APP_IMPLEMENTATION_NOTES.md` in the app project | Summarizes current architecture, working modes, DNS plan, discovery plan, and verification notes. |
| `RelayProfile.swift` and `ProviderProfile.swift` | Show the transport model, DNS protocol choices, Psiphon config fields, and provider configuration boundary. |
| `TunnelController.swift` | Shows validation, profile installation, start/stop lifecycle, and NetworkExtension manager handling. |
| `PacketTunnelProvider.swift` | Shows PacketTunnel mode routing, network settings, Xray start, Google relay start, DNS start, and Psiphon start boundaries. |
| `GooseRelay.swift` | Shows the local Goose SOCKS bridge, fake-DNS handling, packet-flow bridge, encrypted frame carrier, metrics, and self-tests. |
| `CloudflareWorker/` and `RelayScripts/` | Show the Worker and Apps Script forwarding templates without needing public runtime secrets. |

## Redaction Rules

Keep out of GitHub:

- Live relay hostnames, worker URLs, Apps Script deployment IDs, panel URLs, account IDs, auth tokens, tunnel keys, generated configs, and QR codes.
- Raw CDN candidate IP/SNI lists or scanner output.
- Private provisioning profiles, Apple account details, App Store Connect IDs, and TestFlight build artifacts.
- One-click operational setup for a fragile active route.

Safe to publish:

- Architecture diagrams.
- Codebase maps.
- High-level transport flows.
- Failure modes and safety checks.
- Upstream project credits.
- Evidence levels and dates.

## Backlog

- Turn MasterDNS/DNSTT/Slipstream from configuration surfaces into PacketTunnel-safe native engines.
- Replace disabled Psiphon/fronting stub with a memory-safe iOS bridge or keep it as candidate discovery only.
- Add a shared candidate store for CDN/SNI scan results with cooldown, last-success, and last-failure metadata.
- Keep app-side logs redacted and cap packet/host logging in provider diagnostics.
- Add source cards for each project in [Upstream Credits And Appreciation](upstream-credits.md).
