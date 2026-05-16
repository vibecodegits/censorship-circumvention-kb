# Findings: Relay Experiments, 2026-04-25

Evidence level: `L2-L4`

Source session: `Deploy MoaV on Google Cloud`

## Scope

This session tested and compared multiple relay substrates around MoaV, Xray/XHTTP, Netlify, Vercel, Fastly, Cloud Run, Apps Script, and related local Xray configs.

Repos and projects encountered:

- [shayanb/MoaV](https://github.com/shayanb/MoaV)
- [Kianmhz/GooseRelayVPN](https://github.com/Kianmhz/GooseRelayVPN)
- [amirshaker000/netlify-relay](https://github.com/amirshaker000/netlify-relay)
- [avaco-cloud/Vercel-XHTTP](https://github.com/avaco-cloud/Vercel-XHTTP)
- [powerofp/vercelmasterhttp](https://github.com/powerofp/vercelmasterhttp)
- [g3ntrix/Shade](https://github.com/g3ntrix/Shade)
- [denuitt1/mhr-cfw](https://github.com/denuitt1/mhr-cfw)
- [serverless-dns/serverless-dns](https://github.com/serverless-dns/serverless-dns)
- [ImpostorKeanu/front_brute](https://github.com/ImpostorKeanu/front_brute)

## Important Technical Findings

### Netlify XHTTP

The Netlify XHTTP lane could work for browsing/download-heavy traffic, but sustained upstream hit platform limits. A 100 MiB bidirectional test showed download completed quickly, while sustained upload failed around the one-minute window.

Interpretation:

- Downstream can survive better than upstream.
- Video calls and upload-heavy traffic are poor fits.
- Netlify should be treated as disposable relay infrastructure, not a stable core transport.

### Edge Worker Relays

Vercel, Netlify, Fastly Compute, and Cloud Run were explored as ways to hide or relay XHTTP/HTTP-like traffic to an Xray backend.

Durable pattern:

```text
client -> public edge/serverless endpoint -> controlled Xray/MoaV/3x-ui origin -> Internet
```

Main tradeoff:

- The client path looks like normal HTTPS to a popular provider.
- The provider sees relay-like traffic and may throttle, bill, pause, or suspend.

### MoaV

MoaV is broader than one relay trick. Its README frames it as a multi-protocol system with Reality, Trojan, Hysteria2, XHTTP, DNS tunnels, WireGuard/wstunnel, TrustTunnel, CDN, MTProxy, and other fallback lanes.

KB classification:

- Family: multi-protocol orchestration and deployment toolkit.
- Value: a mental model for layered fallbacks.
- Risk: wide scope can hide operational complexity.

## Strategic Lesson

Provider-hosted relays are attractive because they buy collateral value and easy deployment. They fail on limits, policy, traffic shape, and upstream duration. Any serious deployment should rotate lanes and treat serverless/edge relays as one layer, not the whole system.

