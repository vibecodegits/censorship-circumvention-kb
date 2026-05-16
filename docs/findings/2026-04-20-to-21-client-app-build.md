# Findings: Client App And MITM Fronting, 2026-04-20 To 2026-04-21

Evidence level: `L2-L3`

Source sessions:

- `Build full-fledged app`
- `Resume app build`

## What We Learned

The early client-app work revolved around Patterniha-style domain-fronting/MITM behavior and a packaged macOS app later referred to as VibeCodeGit VPN.

Key findings:

- GUI-DF-style workflows can work on macOS when the Mac itself uses the local proxy directly.
- iPhone integration is harder because the method behaves like a local browser/proxy/MITM workflow, not a normal VMess/VLESS/Trojan node.
- V2Ray-style "ping" checks are not reliable for this style of tool because the local proxy is not a real Xray node.
- A packaged app can reduce UX pain, but it does not remove the architectural problems around local proxying, certificate trust, and platform-specific traffic capture.
- Later packaging included pinned Google-edge support and Google Apps Script quick-start material.

## KB Interpretation

This is not a clean generic tunnel architecture. It belongs in the "client-side helper/MITM fronting" family.

Durable lessons:

- Client UX and lifecycle management matter as much as the bypass primitive.
- Certificate/MITM workflows are risky and should be treated as advanced/last-resort paths.
- A local SOCKS/HTTP helper can be useful, but phone-wide routing needs VPN/tun2socks-level integration or a client that owns the network extension.

## Public-Safe Redactions

- No live pinned edge addresses.
- No app bundle internals that expose private deployments.
- No raw setup recipes for a working family deployment.

