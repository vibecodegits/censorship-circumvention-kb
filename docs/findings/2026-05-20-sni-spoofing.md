# Findings: SNI Spoofing / Fake ClientHello Injection, May 2026

This note captures the current public lead around SNI spoofing tools without copying live configs, IP addresses, or candidate SNI values.

## Public Lead

User-supplied X lead: [kharabam666/status/2056531696875438464](https://x.com/kharabam666/status/2056531696875438464).

The directly linked X page may require login or fail to render in crawlers. Public mirrors/search results around the same discussion show a claim of a stable connection using SNI spoofing and credit [patterniha/SNI-Spoofing](https://github.com/patterniha/SNI-Spoofing). A related mirrored post also points to the Rust port by `therealaleph` and says the approach is meant to be used with v2ray-style configs that go through Cloudflare/CDN.

## What The Repos Confirm

- [patterniha/SNI-Spoofing](https://github.com/patterniha/SNI-Spoofing) is the original Python implementation lead. The repository frames the method as DPI bypass through IP/TCP header manipulation.
- [therealaleph/sni-spoofing-rust](https://github.com/therealaleph/sni-spoofing-rust) documents the mechanism more explicitly: a local TCP forwarder injects a fake TLS ClientHello with an intentionally wrong TCP sequence number after the TCP handshake, the DPI parses the fake SNI, and the real server drops the invalid segment.
- [sing-box TLS docs](https://sing-box.sagernet.org/configuration/shared/tls/) now document native client-side `spoof` and `spoof_method` fields. The docs describe a forged ClientHello carrying a whitelisted SNI and list several ways to make the receiving server reject the forged segment.

## Client Integration Answer

People generally still need a real proxy config. The spoofing layer is an evasion shim, not the data tunnel.

- With standalone tools, the local Xray/v2ray/sing-box-compatible client connects to the spoofing listener, and the spoofing tool forwards to the upstream endpoint.
- With sing-box 1.14+ style native support, the spoofing behavior can live in the TLS outbound, but the outbound still needs the normal proxy/server settings.
- Xray remains a common underlying proxy engine, but the current public evidence here does not show a native Xray-core `tls.spoof` equivalent. Pairing Xray with a standalone local forwarder is the observed pattern.

## Operational Boundaries

The method requires low-level packet access. Public docs and repos mention root/CAP_NET_RAW and CAP_NET_ADMIN on Linux, root/BPF access on macOS, and Administrator or WinDivert-style interception on Windows.

This is awkward on mobile. Android/iOS clients generally cannot casually inject raw TCP packets from an ordinary app, so mobile use usually needs either a privileged environment, a client core that implements the behavior in a supported way, or a desktop/router doing the spoofing for downstream clients.

## Classification

- Family: Camouflage and DPI evasion.
- Best paired with: existing TLS proxy transports, especially CDN-backed configs.
- Evidence: L3 for implementation behavior from source/docs; L1 for current field report.
- Stability: useful helper tactic, but fragile if middleboxes validate TCP state or wait for the server-accepted ClientHello.

## Redactions

Omitted:

- working fake SNI values
- CDN IPs
- copy-paste configs
- UUIDs, private endpoint domains, or carrier-specific recipes

The new method card is [Fake ClientHello SNI Spoofing](../methods/fake-clienthello-sni-spoofing.md).
