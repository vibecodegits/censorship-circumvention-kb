# Method: Vercel XHTTP Relay

Status: `observed`
Evidence level: `L2-L3`
Last reviewed: 2026-05-16

## Summary

Vercel XHTTP relays use Vercel Edge Functions to forward XHTTP-like traffic from an Xray/V2Ray client to a controlled backend Xray server.

## Related Repos

- [avaco-cloud/Vercel-XHTTP](https://github.com/avaco-cloud/Vercel-XHTTP)
- [powerofp/vercelmasterhttp](https://github.com/powerofp/vercelmasterhttp)

## Family

- Transport: HTTPS/XHTTP through Vercel edge.
- Relay/egress: Vercel Edge Function to Xray origin.
- Client integration: VLESS/XHTTP-capable client.

## Notes From Local Sessions

The Vercel-XHTTP README frames the method as useful only when the operator already controls an Xray backend with XHTTP. It is not a no-server proxy. It also warns that Vercel Hobby traffic accounting can pause accounts when transfer quotas are exhausted, and that Vercel Edge does not support arbitrary TCP, UDP, QUIC, mKCP, gRPC, Reality, or WebSocket as a generic tunnel substrate.

## Failure Modes

- Vercel bandwidth and fast-origin-transfer limits.
- Account pause/suspension.
- Only HTTP-like/XHTTP traffic fits well.
- Backend still needs a stable origin and TLS behavior.

## Strategic Value

Useful as an easy edge layer for XHTTP, especially for testing. Less attractive as a long-term family transport unless account limits and provider policy are managed.

