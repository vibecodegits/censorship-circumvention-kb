# Method: DNS Bootstrap And DNS Tunnels

Status: `observed`
Evidence level: `L2-L3`
Last reviewed: 2026-05-27

## Summary

DNS appears in two different roles: bootstrap/control and full data tunneling. The KB should keep these separate.

## Related Repos And Sources

- [patterniha/slipstream](https://github.com/patterniha/slipstream)
- [patterniha/dnstt](https://github.com/patterniha/dnstt)
- [masterking32/MasterDnsVPN](https://github.com/masterking32/MasterDnsVPN)
- [iampedii/WhiteDNS](https://github.com/iampedii/WhiteDNS)
- [patterniha/QQ-Tunnel](https://github.com/patterniha/QQ-Tunnel)
- [patterniha/QS-Tunnel](https://github.com/patterniha/QS-Tunnel)
- [serverless-dns/serverless-dns](https://github.com/serverless-dns/serverless-dns)
- Shecan / DNS bootstrap observations from Telegram research.

## Family

- Discovery/control: DNS records, DoH/DoT, resolver-specific behavior.
- Transport: DNS tunnel for full data only in the tunnel variants.
- Client integration: system DNS profile, app DNS settings, local resolver/tunnel client.

## Bootstrap Role

DNS bootstrap helps clients resolve or select front domains, SNI candidates, and working route parameters. It can make Netlify/XHTTP or other fronting lanes work where normal resolver behavior fails.

## Tunnel Role

DNS tunnels carry data inside DNS packets. They are resilient under harsh filtering but usually slower and noisier than normal HTTP/TLS transports.

## Findings From Local Sessions

- Telegram research showed strong DNS bootstrap signals.
- Shecan-style resolver placement belongs at system DNS profile level on iOS when possible.
- MoaV treats DNS tunnels like dnstt and SlipStream as fallback lanes, not primary high-speed browsing routes.
- MasterDnsVPN adds a newer DNS-tunnel branch focused on low protocol overhead, resolver balancing, ARQ, packet duplication, and MTU adaptation.
- WhiteDNS is a source-available Android client around MasterDNS/StormDNS with both proxy and Android `VpnService` modes. Treat licensing and redistribution limits carefully.
- QQ-Tunnel and QS-Tunnel are Patterniha DNS-query/IP-spoofing experiments. They belong in research inventory until code review or field reports justify a method card.

## Current Upstream Signals

- `masterking32/MasterDnsVPN` latest public release checked here was `v2026.05.10.180256-27c7e11`; release notes mention smart MTU outlier detection and balancing/log/default-config changes.
- `iampedii/WhiteDNS` latest public release checked here was `1.5.1` on 2026-05-19.
- `shayanb/MoaV` latest public release checked here was `v1.7.8` on 2026-05-25 and added XDNS multi-resolver fan-out for hostile networks.

## Failure Modes

- Resolver block/poisoning.
- Low throughput.
- Query pattern detection.
- Captive DNS or ISP DNS interception.

## Strategic Value

Excellent for bootstrap and last-resort channels. Usually not the best primary data plane.
