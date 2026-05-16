# Method: MITM Domain Fronting / Local Helper Fronting

Status: `observed`
Evidence level: `L2-L3`
Last reviewed: 2026-05-16

## Summary

MITM Domain Fronting and related local helper tools manipulate local HTTP/TLS behavior to make traffic appear to target an allowed front while carrying requests elsewhere. Patterniha-style work and GUI-DF/MMDF discussions belong here.

## Related Repos

- [patterniha/MITM-DomainFronting](https://github.com/patterniha/MITM-DomainFronting)
- [patterniha/MMDF](https://github.com/patterniha/MMDF)
- [selfishblackberry177/sni-spoof](https://github.com/selfishblackberry177/sni-spoof)

## Family

- Transport: HTTPS/TLS to collateral front.
- Camouflage: Host/SNI/front mismatch, local TLS interception, helper behavior.
- Client integration: browser proxy, local SOCKS/HTTP proxy, VPN helper, or app wrapper.

## Local Session Findings

- Works more naturally on a desktop where the system/browser can use the local helper directly.
- Phone-wide routing is harder without a VPN/tun2socks-level client.
- Installing or trusting local certificates is a major safety/UX boundary.
- V2Ray/VLESS "ping" tests do not necessarily prove whether this method works, because the helper is not a standard proxy node.

## Failure Modes

- Certificate trust requirements.
- Browser/client compatibility.
- Provider closing fronting behavior.
- DPI validating TLS/HTTP consistency.
- User misconfiguration.

## Strategic Value

Best treated as a research primitive or helper tactic. A public KB should document architecture and risks, not hand out copy-paste MITM configs.

