# Method: Google-Collateral Direct Fragmentation

Status: `observed`
Evidence level: `L2`
Last reviewed: 2026-05-16

## Summary

The `xsfilterrnet/3425` Telegram post showed a "serverless" NekoBox plus v2rayNG chain. The config evidence points to DNS/fakeIP Google-domain remapping plus TLS ClientHello fragmentation, not a private VPS relay.

## Family

- Discovery/control: DNS/fakeIP and local rule sets.
- Transport: direct outbound over normal TLS-looking traffic.
- Camouflage: Google/YouTube destination override plus TLS fragmentation.
- Relay/egress: no private relay in the inspected config.
- Client integration: NekoBox plus v2rayNG.

## Findings

- v2rayNG side was named `ServLess frag tlshello`.
- Active non-DNS traffic went to Xray `freedom` outbound with TLS ClientHello fragmentation.
- NekoBox side used sing-box style fakeIP DNS, a local mixed inbound, direct outbound, and a large Google/YouTube-oriented domain rule set.
- The method is closer to the Google-collateral route family than to CDN fronting.

## Failure Modes

- Middlebox starts reassembling ClientHello correctly.
- Google-domain exceptions tighten.
- Two-client VPN chaining behaves inconsistently on Android.
- Config becomes stale quickly if it depends on a specific DPI weakness.

## Strategic Value

Interesting as a "no private server" helper lane. Less reliable than a real Google-backed relay or owned transport because it depends on local evasion behavior rather than a controlled egress path.

