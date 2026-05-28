# Method: Native Client Packaging And Packet Tunnels

Status: `implemented`
Evidence level: `L3-L4`
Last reviewed: 2026-05-27

## Summary

Native client packaging is not a circumvention primitive by itself, but it decides whether a method is usable outside the lab. The VibeCodeGit VPN work showed that once a method reaches real users, lifecycle, DNS, signing, system proxy cleanup, and UI state become as important as the relay protocol.

## Related Repos And Sources

- [dima-u/SwiftyXrayCore](https://github.com/dima-u/SwiftyXrayCore)
- [dima-u/SwiftyXrayKit](https://github.com/dima-u/SwiftyXrayKit)
- [hiddify/hiddify-app](https://github.com/hiddify/hiddify-app)
- [throneproj/Throne](https://github.com/throneproj/Throne)
- [g3ntrix/Cloak](https://github.com/g3ntrix/Cloak)
- [iampedii/WhiteDNS](https://github.com/iampedii/WhiteDNS)
- Local VibeCodeGit VPN and VibeCodeGit VPN 2.0 session notes summarized in `docs/findings/2026-05-27-vibecodegit-vpn-lessons.md`.

## Family

- Discovery/control: profile editor, subscription imports, scanner/candidate feeds, deployment ID fields.
- Transport: supplied by embedded Xray/sing-box/Goose/DNS tunnel/custom relay components.
- Camouflage: inherited from the selected transport.
- Relay/egress: supplied by Google Apps Script, Worker/VPS, Xray origin, DNS server, or another configured lane.
- Client integration: macOS system proxy, Android `VpnService`, iOS `PacketTunnelProvider`, tun2socks, local SOCKS/HTTP listeners.

## Durable Lessons

- A local proxy helper is easier to ship on macOS, but full-device phone routing needs a native VPN extension or a client that owns the tunnel path.
- UI tabs must not silently change the live active route. Viewing a transport config and connecting through it are separate actions.
- For iOS, PacketTunnel plus tun2socks/Xray is a practical base because it lets normal apps use the tunnel without per-app proxy setup.
- DNS is a first-order design problem. If every DNS lookup rides the slow relay path, the VPN can appear connected while traffic stalls.
- Long-poll relay carriers need careful concurrency. Avoid holding carrier/session locks while inspecting or closing per-flow state.
- Setup screens should expose only the input the user can safely provide. VibeCodeGit VPN 2.0 moved toward one Apps Script deployment ID field while fixing secrets and relay parameters internally.
- App Store/TestFlight work is part of the engineering surface: bundle IDs, Network Extension entitlements, icons, export compliance, and provisioning can block distribution even after the tunnel works.

## Safety Checklist

- No raw tokens, UUIDs, tunnel keys, private endpoints, or generated configs in public repos.
- Redact secrets from runtime logs and UI diagnostics.
- Track ownership of system proxy or VPN profile state and recover on launch after crashes.
- Make TLS verification production-default and developer-insecure paths explicit.
- Avoid QR codes or screenshots that expose long-lived auth material.
- Keep scanning/discovery low-volume and separate from the connect button.

## Failure Modes

- Stale system proxy settings break the user machine after crash or force-quit.
- Two VPN-style apps compete for the same OS tunnel route.
- DNS deadlocks or slow relay DNS make the tunnel look alive but unusable.
- App packaging includes old bundle identifiers or stale provisioning profiles.
- Helper binaries are not bundled, signed, or allowed by hardened runtime rules.
- A working repo becomes unusable because the user-facing setup has too many fields or ambiguous mode state.

## Strategic Value

This layer turns volatile circumvention methods into something maintainable. It should be treated as a product architecture family, not as cosmetic polish.
