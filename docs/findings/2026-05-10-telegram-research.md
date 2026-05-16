# Findings: Telegram Research And Netlify XHTTP, 2026-05-10

Evidence level: `L1-L4`

Source artifacts:

- `reports/telegram_evasion_report.md`
- `reports/netlify_xhttp_working_path.md`

## Signal Report

The Telegram export produced these strong signal families:

- DNS bootstrap
- Cloudflare/CDN/XHTTP discussion
- Fragmentation and SNI tuning
- VLESS/REALITY
- Hysteria2/TUIC/QUIC, conditional on UDP reachability
- Success/failure reports with high ISP variance

The most important interpretation is that public chat data is noisy. It is useful for finding candidate patterns, but it must be separated from actual reproducible test results.

## Netlify XHTTP

The May 10 report concluded that the user’s existing Netlify fronting path matched a common working pattern:

```text
client -> front/SNI candidate -> Netlify Edge relay -> external Xray/3x-ui VLESS XHTTP inbound
```

Useful conclusions:

- Netlify XHTTP can be a real lane.
- It is not durable as one static config.
- DNS bootstrap, such as Shecan/StormDNS-like resolver behavior, can be the difference between a front domain resolving/usefully dialing or failing.
- The target origin should be the XHTTP inbound, not the 3x-ui panel.
- UUIDs live at the Xray backend layer; the Netlify relay does not need to know or pin them.

## Shecan/V2Box Placement

The Shecan discussion clarified an important client-integration point:

- DNS bootstrap belongs at system DNS profile level on iOS when possible.
- App-level DNS settings are second best.
- DNS values should not be confused with VLESS server fields.

## KB Interpretation

This belongs across three method cards:

- Netlify XHTTP relay
- DNS bootstrap
- Self-hosted origin plus panel hygiene

