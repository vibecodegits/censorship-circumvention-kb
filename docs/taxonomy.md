# Taxonomy

This taxonomy organizes circumvention by role in the system, not by brand name. A single project may appear in multiple families.

## Layers

### Discovery And Control

How clients learn about working paths, parameters, or updates.

Examples: DNS-based signaling, signed config manifests, Telegram/GitHub/Pastebin distribution, covert control channels.

Common failure modes:

- Resolver blocking or DNS poisoning
- Distribution channel takedown
- Config feeds becoming a blocklist oracle
- Freshness and authenticity problems

### Transport Substrate

The network path that carries user traffic or tunnel traffic.

Examples: Google infrastructure, CDN fronting, DNS tunnels, direct fragmented TLS, Psiphon meek, Cloudflare/Netlify/Workers style relays.

Common failure modes:

- Provider policy changes
- SNI, ALPN, TLS fingerprint, or HTTP behavior mismatch
- Collateral target becomes blocked
- ISP-specific filtering differences

### Camouflage And DPI Evasion

How traffic avoids classification by middleboxes.

Examples: TLS ClientHello fragmentation, SNI spoofing, browser TLS fingerprints, domain-fronting style host/SNI mismatch, protocol mimicry.

Common failure modes:

- TCP/TLS reassembly by the censor
- Fingerprint mismatch
- Active probing
- Unusual timing or packet-size signatures

### Relay And Egress

Where traffic exits to the public Internet.

Examples: VPS egress, Google Apps Script relay, Cloudflare Worker, private Node worker, Psiphon server network, no-server direct egress.

Common failure modes:

- Provider abuse controls
- Cost and rate limits
- Server IP blocking
- Account suspension
- Scaling bottlenecks

### Client Integration

How the method reaches normal apps on the user device.

Examples: Android VPN service, tun2socks, SOCKS/HTTP local proxy, NekoBox, v2rayNG, Psiphon/Shir-o-Khorshid client.

Common failure modes:

- Two VPN apps cannot both own the tunnel path cleanly
- Certificate/MITM trust requirements are too risky
- Battery and reliability problems
- UX complexity causes misconfiguration

### Broker And Reverse Relay

How a hidden origin reaches users without exposing inbound ports directly.

Examples: Twoman public-host broker, Cloudflare Tunnel, reverse agents, managed shared-host brokers.

Common failure modes:

- Broker host blocks, rate limits, or suspends traffic
- Hidden origin loses outbound connectivity
- Public host becomes the bottleneck
- Authentication mistakes expose private services

## Method Families

| Family | Core Idea | Strength | Weakness |
| --- | --- | --- | --- |
| DNS tunnels | Encode data through DNS queries/responses | Hard to fully kill without collateral DNS damage | Low bandwidth, noisy at scale |
| DNS bootstrap | Use DNS for discovery/control, not full traffic | Durable and cheap | Needs a real transport after bootstrap |
| Google collateral transport | Make traffic look dependent on Google infrastructure | High blocking cost for censor | Requires careful behavior match; provider-dependent |
| Google Apps Script relays | Use GAS as relay/control surface | Easy distribution, high collateral value | Quotas, policy risk, latency |
| CDN fronting | Separate visible front domain from backend routing path | Strong when provider behavior permits it | Often closed by CDN policy or burned edge sets |
| Psiphon/fronted meek | Use Psiphon tunnel protocols with fronting/meek | Mature ecosystem and server network | Needs working fronting parameters |
| TLS fragmentation | Split ClientHello or records to confuse DPI | Simple helper, no server required | Breaks when censor reassembles correctly |
| SNI spoofing | Show a permitted SNI or confusing SNI behavior | Can bypass simple SNI filters | Fragile under deeper TLS validation |
| Worker/serverless relays | Cloudflare, Netlify, VPS workers as relay layer | Easy to deploy and rotate | Provider limits and blockability |
| Edge XHTTP relays | Netlify/Vercel/Fastly-style XHTTP forwarding to Xray | Hides origin behind large provider | HTTP platform limits and throttling |
| Reverse broker relays | Public shared host brokers traffic to hidden origin | No inbound ports needed on origin | Broker bottleneck and complexity |
| Scanner tooling | Find reachable CDN/provider edges | Useful telemetry | Reachable does not mean tunnel-compatible |

## Classification Checklist

For every method, capture:

- What is the minimum trust assumption?
- Does it need a remote server or account?
- Does it require user-installed certificates?
- What visible domains, providers, or fingerprints does it depend on?
- What changes would kill it?
- Is the method stable architecture or only a working config snapshot?
