# Findings: Current Thread, May 2026

This note summarizes the working understanding from the current research thread. It intentionally omits raw IP lists and live configs.

## Shared Chat Transcript

The shared ChatGPT transcript started from Siemens PLC/CDN protocol questions and moved into censorship circumvention architecture.

Main conclusion:

- PLC-native protocols are poor general-purpose public bypass transports.
- The more plausible design is a mobile/client-side tunnel that encrypts user traffic, carries opaque chunks over a collateral provider path, and exits through a relay or compatible tunnel network.
- DNS is better as bootstrap/control or low-bandwidth channel than as the default full browsing data plane.

## Shir-o-Khorshid And Psiphon Fronting

The X post and repository review showed that Shir-o-Khorshid is a community Psiphon Android fork with added CDN fronting controls.

Code-level findings from the local review:

- The Android client exposes CDN fronting settings for edge addresses and SNI.
- The custom Psiphon core includes `FRONTED-MEEK-CDN-OSSH`.
- The client has hardcoded verify-name logic for Akamai-like and Fastly-like fronting cases.
- The build workflow pulls the custom tunnel core into the Android app.

Architecture classification:

- Family: Psiphon/fronted meek plus CDN fronting.
- Providers observed: Akamai and Fastly families.
- Stability: powerful but likely high burn rate when small edge/SNI sets are public.

## Telegram Field Reports

The `INTERNETFORIRAN` channel posts described a fast-moving Akamai/Fastly period.

Observed pattern:

- Earlier posts distributed a larger Akamai edge set.
- Later scan summaries suggested the available Akamai set had shrunk sharply, and broad Fastly scans were poor.
- Reports varied by mobile operator, which means "working" needs carrier context.

Interpretation:

- This looked like a method under active pressure, not a stable generic route.
- Reachable CDN edges should not be treated as tunnel-compatible until protocol behavior is tested.

## Psiphon Helper / MitM Domain Fronting

The Patterniha-linked tutorial described using a local helper with Psiphon, where another local client supplies behavior Psiphon does not directly expose.

Architecture classification:

- Family: local MITM/helper plus Psiphon/domain-fronting.
- Risk: certificate/MITM requirements are a user-safety and UX concern.
- Strategic lesson: the durable part is not the exact config; it is the client-side ability to manipulate fronting, TLS, and routing parameters.

## NekoBox + v2rayNG Serverless Post

The `xsfilterrnet/3425` post advertises a serverless NekoBox plus v2rayNG combination.

Config-level findings:

- v2rayNG side is named `ServLess frag tlshello`.
- Active routing sends non-DNS traffic through a local Xray `freedom` outbound with TLS ClientHello fragmentation.
- NekoBox side is sing-box style with fakeIP DNS, local mixed inbound, direct outbound, and a large Google/YouTube-oriented rule set.
- The NekoBox rules use destination override behavior toward a Google destination family.

Architecture classification:

- Family: Google-collateral plus TLS fragmentation, probably no private VPS.
- Stability: potentially better than public CDN edge lists, but fragile if middleboxes improve TLS reassembly or tighten Google exceptions.

## Current Strategic Takeaway

The most promising durable architecture is layered:

- DNS or similar low-friction mechanisms for discovery/control.
- Google-collateral routes as a primary high-collateral transport where behavior can be made normal enough.
- Psiphon/CDN/fronting as fallbacks when working parameters exist.
- DPI/SNI fragmentation as helper tactics, not the whole system.
- A client-side update/control mechanism that can rotate strategies without publishing raw live parameters as the main artifact.

