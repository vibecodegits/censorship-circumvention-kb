# Method: Self-Hosted Origin, 3x-ui, Cloudflare Tunnel, WARP

Status: `implemented`
Evidence level: `L3-L4`
Last reviewed: 2026-05-16

## Summary

Several sessions involved a self-hosted 3x-ui/Xray origin behind Cloudflare Tunnel, with WARP and systemd-managed helper services. This is operational infrastructure rather than a single censorship-bypass method, but it underpins many relay experiments.

## Related Repos

- [MHSanaei/3x-ui](https://github.com/MHSanaei/3x-ui)
- [cloudflare/cloudflared](https://github.com/cloudflare/cloudflared)
- [XTLS/Xray-core](https://github.com/XTLS/Xray-core)

## Key Lessons

- Keep the panel separate from proxy inbound paths.
- Do not expose a no-auth SOCKS proxy publicly.
- Cloudflare Tunnel cannot publish arbitrary SOCKS on a URL path; raw TCP requires hostname-level Cloudflare Access flow.
- For XHTTP relays, the edge relay should target the XHTTP inbound, not the admin panel.
- Patch cadence matters: Xray, 3x-ui, cloudflared, WARP, and kernel/module mitigations are part of reliability.

## Failure Modes

- Panel exposed by mistake.
- Origin IP or Cloudflare path blocked.
- No-auth proxy exposure.
- Dependency drift and security vulnerabilities.
- WARP or tunnel service failures.

## Strategic Value

Useful as the controlled origin for Netlify/Vercel/Fastly/MHR/Twoman experiments. It should be treated as private infrastructure, not documented with live addresses or credentials.

