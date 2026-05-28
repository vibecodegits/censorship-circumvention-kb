# Method: Google Apps Script Relay Family

Status: `implemented`
Evidence level: `L3-L4`
Last reviewed: 2026-05-27

## Summary

Google Apps Script relay methods use HTTPS traffic to Google as the visible path, then relay or forward requests through Apps Script and sometimes an additional Worker/VPS/backend layer. The family includes pure HTTP relays, MHR variants, GooseRelayVPN, Shade, and app-specific client wrappers.

## Related Repos

- [masterking32/MasterHttpRelayVPN](https://github.com/masterking32/MasterHttpRelayVPN)
- [therealaleph/MasterHttpRelayVPN-RUST](https://github.com/therealaleph/MasterHttpRelayVPN-RUST)
- [denuitt1/mhr-cfw](https://github.com/denuitt1/mhr-cfw)
- [aliasoblomov/mhr-vps-worker](https://github.com/aliasoblomov/mhr-vps-worker)
- [Kianmhz/GooseRelayVPN](https://github.com/Kianmhz/GooseRelayVPN)
- [g3ntrix/Shade](https://github.com/g3ntrix/Shade)
- [powerofp/vercelmasterhttp](https://github.com/powerofp/vercelmasterhttp)
- [ajavadinezhad/zyrln](https://github.com/ajavadinezhad/zyrln)

## Family

- Discovery/control: Apps Script deployment IDs, config files, client UI.
- Transport: HTTPS to Google / Apps Script.
- Camouflage: Google SNI/edge behavior, normal HTTPS request surface.
- Relay/egress: Apps Script alone, Cloudflare Worker, Vercel endpoint, or private VPS worker.
- Client integration: local HTTP/SOCKS proxy, native app, or helper.

## Variants

### MasterHttpRelayVPN / mhrv-rs

Local client exposes an HTTP/SOCKS-like proxy and sends relay requests to a user-deployed Apps Script. The Rust version improved local-client packaging and performance compared with the original Python style.

Useful distinction from the Codex sessions:

- `upstream_socks5` means "where the relay client sends egress after it receives traffic locally."
- A local Xray SOCKS inbound can be used as the upstream, but that is a client-side chain, not the remote server.

### MHR-CFW

Adds Cloudflare Worker as an intermediate fetch/relay layer:

```text
local proxy -> Google Apps Script -> Cloudflare Worker -> target
```

Value: shifts egress away from Apps Script alone.

Weakness: depends on both Google and Cloudflare availability, and Cloudflare may be blocked or noisy in the target region.

### mhr-vps-worker

Replaces Cloudflare Worker with a private Node worker on a VPS. The compatibility session found that the request/response shape matched the Rust MHR client path closely enough for the Apps Script path.

Value: more control, fewer Cloudflare free-tier constraints.

Weakness: introduces VPS IP reputation and operational maintenance.

### GooseRelayVPN

Uses Apps Script as a forwarder for encrypted frames to a private VPS exit server. It is closer to a raw TCP-over-SOCKS tunnel than pure web fetch relays.

Value: can carry arbitrary TCP from SOCKS-aware apps.

Weakness: needs a real exit server and does not solve UDP/WireGuard cleanly.

The VibeCodeGit VPN 2.0 work reinforced a key design point: Apps Script should be a forwarder/carrier for opaque encrypted batches, not the place that holds tunnel keys or sees plaintext targets. The phone/client must also avoid turning every DNS lookup into a slow blocking relay event; DNS needs caching, bypass, or a purpose-built DNS transport.

### Shade / VibeCodeGit VPN

Client wrapper around Google/Apps-Script-oriented relay behavior. The main KB lesson is client safety and lifecycle management: proxy cleanup, TLS verification, secret redaction, and crash recovery matter.

### zyrln

Android VPN plus desktop proxy framed around Google-infrastructure domain-fronting relay behavior. Track as part of the Google-collateral family, but verify the exact transport and threat model before treating it as compatible with MHR/Goose/VibeCodeGit shapes.

## Current Upstream Signals

- `Kianmhz/GooseRelayVPN` latest public release checked here was `v1.7.1` on 2026-05-23, with fixes around Apps Script forwarder error handling and installer dependency order.
- `therealaleph/MasterHttpRelayVPN-RUST` latest public release checked here was `v1.9.35` on 2026-05-25, emphasizing large-download resilience, separate stream timeouts, and safer fallback from slow exit-node paths.
- `masterking32/MasterHttpRelayVPN` remains active on its `python_testing` branch, with a 2026-05-18 push timestamp in GitHub metadata.

## Failure Modes

- Apps Script daily/runtime quotas.
- Google account/platform enforcement.
- Latency and request-size limitations.
- Poor fit for sustained upload or real-time media.
- Client UX complexity.
- Egress worker or VPS blockability.

## Strategic Value

This family remains important because Google collateral value is high. But the best architecture is probably not "Apps Script as the whole VPN"; it is Apps Script as a bootstrap, relay, or emergency lane alongside stronger transports.
