# Method: Fake ClientHello SNI Spoofing

Status: `implemented`
Evidence level: `L3`
Last reviewed: 2026-05-20

## Summary

Fake ClientHello SNI spoofing is a packet-level DPI evasion helper. A local tool or proxy core injects a forged TLS ClientHello containing a permitted SNI before the real TLS handshake. The forged segment is made unacceptable to the real server, while a permissive or partially stateful middlebox may still parse it and mark the flow as allowed.

This is not a full VPN or proxy transport by itself. It usually needs an existing TLS proxy path, such as a VLESS/VMess/Trojan/XHTTP-style client configuration, and is most often discussed with CDN-backed configs.

## Related Repos And Docs

- [patterniha/SNI-Spoofing](https://github.com/patterniha/SNI-Spoofing)
- [therealaleph/sni-spoofing-rust](https://github.com/therealaleph/sni-spoofing-rust)
- [selfishblackberry177/sni-spoof](https://github.com/selfishblackberry177/sni-spoof)
- [sing-box TLS `spoof` and `spoof_method`](https://sing-box.sagernet.org/configuration/shared/tls/)
- [XTLS/Xray-core](https://github.com/XTLS/Xray-core) as a common underlying client/server substrate, not currently tracked here as a native implementation of this specific packet injection feature.

## Family

- Discovery/control: none by itself.
- Transport: existing TLS-over-TCP proxy transport, often through a CDN-backed endpoint.
- Camouflage: forged first ClientHello with a whitelisted SNI; the real ClientHello follows normally.
- Relay/egress: supplied by the underlying proxy server, CDN route, or relay, not by the spoofing layer.
- Client integration: standalone local forwarder in front of Xray/v2ray/sing-box-compatible configs, or native sing-box outbound TLS spoofing in versions that support it.

## Dependencies

- Providers: a reachable underlying TLS endpoint and, for common public examples, a CDN edge/origin path.
- Client software: an existing proxy client/config for the real tunnel, unless the proxy core implements spoofing natively.
- Remote infrastructure: an origin/relay that accepts the real TLS/proxy handshake after the spoofed segment is ignored.
- OS privileges: raw packet access. Linux needs elevated capabilities, macOS needs root/BPF access, and Windows needs Administrator/WinDivert-style interception.
- Candidate SNI values: should be treated as short-lived operational details and omitted from public notes.

## Why It Works

The method relies on a gap between what the censoring middlebox sees and what the real server accepts. The middlebox may parse the first plausible ClientHello in the TCP flow and make an allow/block decision from its SNI. The forged packet is then rejected by the real server because of an intentionally invalid TCP property, such as a wrong sequence number or checksum. The real TLS handshake can proceed afterward on the same connection.

sing-box documents this as copying the real ClientHello, replacing only the SNI value, and using a rejection method so the receiving server drops the forged segment while the middlebox treats it as legitimate.

## When A Proxy Config Is Still Needed

- Standalone tools such as `patterniha/SNI-Spoofing` and `therealaleph/sni-spoofing-rust` sit between the local proxy client and the upstream endpoint. Users still need a real Xray/v2ray/sing-box-compatible config for the tunnel.
- Native sing-box support can put the spoofing behavior inside the TLS outbound, but the outbound still needs normal proxy settings.
- Xray is useful as the underlying proxy substrate. The current public evidence here does not show Xray-core itself exposing the same native packet-injection knob, so Xray configs are typically paired with a standalone local forwarder for this method.

## Failure Modes

- DPI validates TCP state more strictly and ignores out-of-window, bad-checksum, or otherwise invalid forged segments.
- DPI waits for the server-accepted TLS handshake instead of trusting the first apparent ClientHello.
- The fake SNI or provider family becomes blocked or loses special treatment.
- TLS fingerprint, ALPN, timing, packet-size, or CDN routing behavior looks inconsistent.
- Mobile OSes and app stores make raw packet injection difficult outside privileged or VPN-extension contexts.
- Users mistake the spoofing helper for a complete proxy and run it without a compatible tunnel path.

## Evidence

| Date | Source | Evidence Level | Notes |
| --- | --- | --- | --- |
| 2026-05-20 | [patterniha/SNI-Spoofing](https://github.com/patterniha/SNI-Spoofing) | L3 | Python implementation describes DPI bypass with IP/TCP header manipulation and includes a local listener plus fake ClientHello injection logic. |
| 2026-05-20 | [therealaleph/sni-spoofing-rust](https://github.com/therealaleph/sni-spoofing-rust) | L3 | Rust port documents wrong-sequence fake ClientHello injection, supported platforms, privilege requirements, and use with CDN-backed VLESS/VMess configs. |
| 2026-05-20 | [sing-box TLS docs](https://sing-box.sagernet.org/configuration/shared/tls/) | L3 | Official docs include client-side `spoof` and `spoof_method` fields, supported rejection methods, and privilege requirements. |
| 2026-05-20 | [kharabam666 X lead](https://x.com/kharabam666/status/2056531696875438464) | L1 | Public lead reports stable use of SNI spoofing and points to Patterniha's implementation; direct X access may require login. |

## Public-Safe Notes

Do not publish raw working configs, Cloudflare/CDN IPs, candidate fake SNI lists, UUIDs, private endpoint domains, or carrier-specific recipes. The durable knowledge is the role of the spoofing layer, its dependency on an underlying tunnel, and the middlebox assumption it exploits.
