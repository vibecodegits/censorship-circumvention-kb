# Method: Multi-Protocol Orchestration And Panels

Status: `implemented`
Evidence level: `L3`
Last reviewed: 2026-05-27

## Summary

Multi-protocol orchestration projects combine many circumvention transports, generated client profiles, user management, routing rules, and operational scripts. They are not one bypass method; they are survival portfolios. The main design challenge is keeping user/profile state synchronized when transports are added, removed, or regenerated.

## Related Repos

- [shayanb/MoaV](https://github.com/shayanb/MoaV)
- [hiddify/Hiddify-Manager](https://github.com/hiddify/Hiddify-Manager)
- [MHSanaei/3x-ui](https://github.com/MHSanaei/3x-ui)
- [NiREvil/bia-pain-bache](https://github.com/NiREvil/bia-pain-bache)
- [ztmwtf/bia-pain-bache-BPB-Worker-Panel](https://github.com/ztmwtf/bia-pain-bache-BPB-Worker-Panel)
- [vahitoo/bia-pain-bache-BPB-Worker-Panel](https://github.com/vahitoo/bia-pain-bache-BPB-Worker-Panel)
- [throneproj/Throne](https://github.com/throneproj/Throne)
- [XTLS/Xray-core](https://github.com/XTLS/Xray-core)
- [SagerNet/sing-box](https://github.com/SagerNet/sing-box)

## Family

- Discovery/control: generated subscriptions, web panels, CLI scripts, app profile import/export.
- Transport: VLESS/REALITY, XHTTP, Hysteria2, TUIC, WireGuard variants, DNS tunnels, Worker/Pages relays, Telegram proxies, Snowflake/Psiphon-style donation lanes.
- Camouflage: inherited from each protocol.
- Relay/egress: VPS, Worker/Pages, Cloudflare Tunnel, WARP, local home lab, donated relay.
- Client integration: subscription links for Xray/sing-box/Clash/Hiddify/Throne/NekoBox/V2Box-style clients.

## Findings From Local Sessions

- MoaV is useful because it keeps many fallback lanes deployable from one stack, but transport changes must be propagated to existing users and generated profiles deliberately.
- Adding MasterDNS-style lanes to an orchestration stack is not just "add one service"; user generation, subscriptions, health checks, profile rendering, and web UI state all need synchronized updates.
- BPB-style Worker panels are useful as Cloudflare Worker/Pages configuration surfaces, especially for VLESS/Trojan/WARP/fragment profiles, but they should be kept separate from unrelated relay workers.
- 3x-ui remains useful for origin/user management, but exposing raw SOCKS/mixed listeners publicly is weaker than using VLESS/Reality/Trojan/XHTTP-style encrypted clients.

## Current Upstream Signals

- `shayanb/MoaV` latest public release checked here was `v1.7.8` on 2026-05-25. Release notes highlighted XDNS multi-resolver fan-out, faster Xray builds from pinned binaries, build resilience for restricted regions, log cleanup, and config-aware update guidance.
- `hiddify/Hiddify-Manager` latest public release checked here was `v12.3.1` on 2026-05-26.
- `MHSanaei/3x-ui` latest public release checked here was `v3.1.0` on 2026-05-23.
- `SagerNet/sing-box` latest public release checked here was `v1.13.12` on 2026-05-15.
- `XTLS/Xray-core` latest public release checked here was `v26.3.27` on 2026-03-27, while the repository had newer pushes through 2026-05-26.

## Failure Modes

- Generated profiles drift from live server state.
- Existing users do not receive newly added transports or lose removed transports cleanly.
- A web UI writes incomplete state after a backend schema changes.
- A panel leaks raw operational material in URLs, QR codes, logs, screenshots, or public docs.
- Too many fallback options make support impossible unless health and provenance are visible.

## Strategic Value

Orchestration is the right shape for a hostile network because no single method stays good forever. The KB should track these projects as integration layers and distinguish "transport works" from "user generation and subscription sync are correct."
