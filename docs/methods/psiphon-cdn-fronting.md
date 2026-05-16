# Method: Psiphon / Shir-o-Khorshid CDN Fronting

Status: `degrading`
Evidence level: `L3-L4`
Last reviewed: 2026-05-16

## Summary

Shir-o-Khorshid is an unofficial Psiphon Android fork that adds controls for CDN-fronted Psiphon transport behavior. The custom core includes a fronted meek CDN protocol path.

## Related Repos

- [shirokhorshid/shirokhorshid-android](https://github.com/shirokhorshid/shirokhorshid-android)
- [shirokhorshid/psiphon-tunnel-core](https://github.com/shirokhorshid/psiphon-tunnel-core)

## Family

- Transport: Psiphon fronted meek / OSSH.
- Camouflage: CDN fronting, TLS profile and SNI/verify-name controls.
- Relay/egress: Psiphon server network.
- Client integration: Android VPN client.

## Code-Level Findings

Local source review found:

- Android settings for CDN edge addresses and SNI.
- Custom tunnel core protocol `FRONTED-MEEK-CDN-OSSH`.
- Dial override fields for SNI, verify server names, ALPN, TLS profile, and dial addresses.
- Akamai-like and Fastly-like verify-name sets.
- Hardcoded edge candidates in the Android client.

## Field Report Pattern

Telegram reports around May 2026 suggested a sharp reduction in working Akamai edges and mixed Fastly availability, with strong ISP/operator dependence.

## Failure Modes

- Edge IP sets burn quickly once public.
- CDN policy changes.
- ISP-specific blocking.
- Reachable edge does not equal compatible Psiphon fronting path.

## Strategic Value

Strong when alive, but likely high burn rate. Better as a rotating fallback under a client that can update tactics safely.

