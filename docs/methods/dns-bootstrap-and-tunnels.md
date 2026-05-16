# Method: DNS Bootstrap And DNS Tunnels

Status: `observed`
Evidence level: `L2-L3`
Last reviewed: 2026-05-16

## Summary

DNS appears in two different roles: bootstrap/control and full data tunneling. The KB should keep these separate.

## Related Repos And Sources

- [patterniha/slipstream](https://github.com/patterniha/slipstream)
- [patterniha/dnstt](https://github.com/patterniha/dnstt)
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

## Failure Modes

- Resolver block/poisoning.
- Low throughput.
- Query pattern detection.
- Captive DNS or ISP DNS interception.

## Strategic Value

Excellent for bootstrap and last-resort channels. Usually not the best primary data plane.

