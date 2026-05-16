# Method: Twoman Host-Preserving Relay

Status: `observed`
Evidence level: `L2-L3`
Last reviewed: 2026-05-16

## Summary

Twoman is a host-preserving relay model for shared cPanel/managed hosting. A public host acts as a broker, while a hidden server dials outward and provides the actual egress path.

## Related Repo

- [ShahabSL/twoman](https://github.com/ShahabSL/twoman)

## Family

- Transport: normal HTTPS to public shared host.
- Relay/egress: hidden server connected through broker.
- Client integration: local HTTP/SOCKS proxy or tunnel mode.

## Architecture

Public-safe shape:

```text
family client -> public cPanel/managed host -> hidden reverse agent -> private origin/egress
```

This is attractive when the hidden origin has strong bandwidth but cannot or should not expose inbound ports.

## Local Session Interpretation

Twoman made sense for a home-lab/fiber setup because the Canadian home server can be the hidden egress while the public shared host is only the reachable broker. The bottleneck is likely the public host and Iran-to-host route, not the home fiber.

## Failure Modes

- Shared hosting resource limits.
- Public broker gets blocked or suspended.
- Latency through broker.
- More moving parts than a direct VPS relay.

## Strategic Value

Potentially valuable for private/family deployments where a strong home connection exists but inbound reachability is hard.

