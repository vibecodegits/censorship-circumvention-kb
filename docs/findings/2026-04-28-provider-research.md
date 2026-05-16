# Findings: Provider And Edge Relay Research, 2026-04-27 To 2026-04-28

Evidence level: `L1-L3`

Source sessions:

- `Find Google script daily limit`
- `Find edge relay service`
- `Find Fastly worker domain support`

## Google Services

The useful question was: which Google products can carry VMess, VLESS, HTTP tunnels, Trojan, Shadowsocks, mixed proxy traffic, or WireGuard-like traffic?

High-level conclusion:

- Raw TCP/UDP or long-lived bidirectional HTTP streaming is required for most VPN/proxy transports.
- Many Google products are ordinary request/response HTTP services and do not make good generic relays.
- Better candidates are infrastructure products that can host real services or long-lived streams, such as GKE, App Engine Flexible in some cases, external load balancing, Cloud Run for supported HTTP/WebSocket-like traffic, or Compute Engine.
- Apps Script is useful because of Google collateral value, but it has quotas and was not designed as a high-throughput relay.

## Edge/CDN Providers

Potential front doors discussed:

- Gcore CDN
- AWS CloudFront
- Azure Front Door
- Bunny CDN
- Fastly
- Cloudflare
- Netlify
- Vercel

The durable recommendation was to keep a controlled origin, then test multiple non-Cloudflare front doors because Cloudflare paths were already known to be weak or blocked in some Iran contexts.

## Fastly Clarification

Important distinction:

- Your own Fastly service/domain can route to your own backend if configured for that behavior.
- Arbitrary third-party Fastly domains, such as public package-hosting domains, should not be treated as a reliable or appropriate front for your private service.

KB classification:

- Fastly Compute belongs in "edge worker relay" if you own the service.
- Public third-party fronting attempts belong in "fragile provider-specific loopholes" and should not be public operational guidance.

