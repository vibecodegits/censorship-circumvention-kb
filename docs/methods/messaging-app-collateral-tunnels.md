# Method: Messaging-App Collateral Tunnels

Status: `observed`
Evidence level: `L2-L3`
Last reviewed: 2026-05-27

## Summary

Messaging-app collateral tunnels carry proxy or VPN traffic over infrastructure that a censor may hesitate to block completely, such as voice-call or WebRTC infrastructure inside a locally important messenger. The current starred sources focus on Bale Messenger and use call-like WebRTC paths as the carrier.

## Related Repos

- [theermia/BaleTunnel](https://github.com/theermia/BaleTunnel)
- [kookoo1sabzy/BaleVPN](https://github.com/kookoo1sabzy/BaleVPN)

## Family

- Discovery/control: messenger account login, contact discovery, signaling channel, peer acceptance.
- Transport: WebRTC/DataChannel or RTP/SRTP-like media carrier over the messenger call infrastructure.
- Camouflage: traffic resembles a long voice or media call between messenger contacts.
- Relay/egress: the peer acting as server shares its own Internet connection.
- Client integration: local SOCKS5 proxy, Android `VpnService`, desktop TUN/SOCKS modes depending on implementation.

## Why It Matters

This family is different from CDN or Google collateral. The collateral target is local social/voice infrastructure. If calls through the messenger remain allowed during partial shutdowns, a tunnel can sometimes ride that path without external VPS discovery or public CDN fronts.

## Privacy And Trust

This is an IP reachability technique, not anonymity.

- The messenger operator can generally observe account-level metadata: which accounts call each other, when, and for how long.
- Depending on the implementation and active relay position, the operator or SFU/TURN path may see destination metadata and plaintext from non-end-to-end-encrypted protocols.
- Users still need application-level encryption such as HTTPS. Treat the relay peer and platform as visible infrastructure, not as a privacy provider.

## Failure Modes

- The messenger blocks, rate-limits, or changes voice/WebRTC behavior.
- Account registration, phone-number verification, or contact graph requirements make onboarding risky.
- Long high-bandwidth sessions stand out as abnormal calls.
- Carrier loss/latency makes generic TCP over media paths fragile.
- Social-graph metadata can expose the relay relationship.

## Strategic Value

Messaging-app tunnels are valuable as emergency peer-assisted lanes, especially where one person has a good connection and another does not. They should sit beside DNS and Google/CDN fallback methods, not replace them.
