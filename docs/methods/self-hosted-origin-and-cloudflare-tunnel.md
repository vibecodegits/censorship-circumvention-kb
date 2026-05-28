# Method: Self-Managed Origins, Panels, And Tunnel Infrastructure

Status: `implemented`
Evidence level: `L3-L4`
Last reviewed: 2026-05-28

## Summary

This card is about user-controlled operational infrastructure: the origin, panel, tunnel, WARP egress, and helper services that other methods depend on. It is not a separate circumvention transport.

MoaV, Hiddify Manager, and 3x-ui belong in the same broad category: self-managed orchestration/panel layers that generate, manage, or expose multiple proxy transports. Cloudflare Tunnel, WARP, systemd services, and private VPS/home-lab hosts are supporting infrastructure under that category.

## Related Repos

- [shayanb/MoaV](https://github.com/shayanb/MoaV)
- [hiddify/Hiddify-Manager](https://github.com/hiddify/Hiddify-Manager)
- [MHSanaei/3x-ui](https://github.com/MHSanaei/3x-ui)
- [cloudflare/cloudflared](https://github.com/cloudflare/cloudflared)
- [XTLS/Xray-core](https://github.com/XTLS/Xray-core)
- [SagerNet/sing-box](https://github.com/SagerNet/sing-box)

## Key Lessons

- Treat MoaV, Hiddify, and 3x-ui as orchestration/panel surfaces, not as individual bypass methods.
- Track the actual transport separately: XHTTP, Reality, Hysteria2, DNS tunnel, Worker relay, Apps Script relay, etc.
- Keep the panel separate from proxy inbound paths.
- Do not expose a no-auth SOCKS proxy publicly.
- Cloudflare Tunnel cannot publish arbitrary SOCKS on a URL path; raw TCP requires hostname-level Cloudflare Access flow.
- For XHTTP relays, the edge relay should target the XHTTP inbound, not the admin panel.
- Patch cadence matters: Xray, sing-box, MoaV, Hiddify, 3x-ui, cloudflared, WARP, and kernel/module mitigations are part of reliability.

## Failure Modes

- Panel exposed by mistake.
- Origin IP or Cloudflare path blocked.
- No-auth proxy exposure.
- User/profile drift when transports are added, removed, or regenerated.
- Dependency drift and security vulnerabilities.
- WARP or tunnel service failures.

## Strategic Value

Useful as the controlled origin and management plane for Netlify/Vercel/Fastly/MHR/Twoman/Goose/DNS experiments. It should be treated as private infrastructure, not documented with live addresses or credentials.

For taxonomy, this card is subordinate to [Multi-protocol orchestration and panels](multi-protocol-orchestration.md). It exists only to preserve the operational lessons from the local 3x-ui/home-lab/Cloudflare Tunnel sessions.
