# Findings: VibeCodeGit VPN And VibeCodeGit VPN 2.0 Lessons, 2026-05-27

Evidence level: `L3-L4`

Sources:

- Local VibeCodeGit VPN macOS sessions from 2026-04-20 to 2026-05-10.
- Local VibeCodeGit VPN 2.0 iOS sessions from 2026-05-20 to 2026-05-22.
- Local project notes under `VibeCodeGit VPN/HANDOFF.md`, `VibeCodeGit VPN/AUDIT.md`, and `VibeCodeGits VPN 2.0/APP_IMPLEMENTATION_NOTES.md`.

## Public-Safe Summary

VibeCodeGit VPN started as a macOS SwiftUI wrapper around local helper/proxy behavior: Apps Script relay, Google/fronting variants, custom relay, V2Ray/Xray, LAN-facing local proxy, OAuth-assisted Apps Script deploy, and packaging around helper binaries.

VibeCodeGit VPN 2.0 moved the design toward a real iOS PacketTunnel app. Its main path used PacketTunnel plus Xray/tun2socks, then a local Goose SOCKS relay that sent encrypted batch frames through a Google Apps Script or Worker/VPS chain. Apps Script was treated as a forwarder, not as the trusted plaintext endpoint.

## Durable Lessons

- Client lifecycle is core security. A stale macOS system proxy, lingering helper process, or stale VPN profile can break the user's whole device.
- A UI mode tab must not equal active route. Users need an explicit distinction between "viewing a config" and "connecting through it."
- Native phone routing needs the OS VPN stack. SOCKS/HTTP helper apps are useful, but iOS family use needs PacketTunnel/tun2socks-level integration.
- DNS behavior can make or break the route. The iOS relay appeared connected while traffic stalled when DNS rode the same slow or deadlocked relay path.
- Apps Script works better as a forwarder for opaque encrypted batches than as a full VPN brain. It should not hold tunnel keys or see target hosts.
- Relay carriers need lock discipline. Do not hold carrier/session locks while checking or closing per-flow state; it can freeze the PacketTunnel.
- Long-polling can be healthy only when upload/send and receive paths are separated enough that one side does not starve the other.
- A user-facing app should expose the minimum safe input. The 2.0 path moved toward a single Apps Script deployment ID while keeping worker auth, tunnel key, route mode, and MTU fixed or generated internally.
- TestFlight/App Store work is not a clerical afterthought. Bundle identifiers, Network Extension entitlement, icon assets, export compliance, and App Store Connect app records all became real blockers.

## What Belongs In The KB

- The architecture pattern: native app -> PacketTunnel/tun2socks -> local relay core -> collateral carrier -> controlled egress.
- The security checklist: proxy/VPN lifecycle cleanup, TLS verification, no secret logs, clear mode state, redacted diagnostics.
- The DNS checklist: cache where safe, avoid blocking the tunnel on DNS, and separate DNS transport experiments from the main connect path.
- The product lesson: reduce user inputs, keep generated secrets private, and make the app recover from partial setup.

## What Stays Out

- Live deployment URLs, UUIDs, worker auth tokens, tunnel keys, account identifiers, private endpoint names, and generated config files.
- Family-specific working configs or screenshots containing QR codes/secrets.
- Raw install instructions for private infrastructure.
