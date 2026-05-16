# Method: Netlify XHTTP Relay

Status: `degrading`
Evidence level: `L4`
Last reviewed: 2026-05-16

## Summary

Netlify XHTTP relays use a Netlify site or function as an HTTP/XHTTP forwarding layer to a controlled Xray/3x-ui backend. The client presents a front/SNI address and a Netlify Host, while the relay forwards traffic to the real XHTTP inbound.

## Related Repos

- [amirshaker000/netlify-relay](https://github.com/amirshaker000/netlify-relay)
- [XTLS/Xray-core](https://github.com/XTLS/Xray-core)

## Family

- Discovery/control: distributed VLESS/XHTTP configs and DNS resolver hints.
- Transport: TLS/HTTP/2/XHTTP through Netlify edge.
- Camouflage: front domain/SNI plus Netlify Host behavior.
- Relay/egress: Netlify Edge/serverless relay to Xray backend.
- Client integration: V2Box/v2rayNG/NekoBox/Xray client with XHTTP support.

## Working Shape

Public-safe architecture:

```text
client -> front/SNI candidate -> Netlify relay host/path -> controlled Xray XHTTP inbound -> Internet
```

Important distinction:

- The relay target must be the XHTTP inbound, not the 3x-ui web panel.
- UUID/user validation happens on the Xray backend, not inside the Netlify relay.
- DNS bootstrap can affect whether the front/SNI candidate is reachable.

## Findings From Local Sessions

- On 2026-05-10, the lane shape was coherent and worked from the local test environment.
- On 2026-05-15, the same backend and user worked directly through the backend path but failed through Netlify with HTTP 429.
- The isolated failing layer was Netlify platform behavior, likely throttling or abuse/rate protection.

## Failure Modes

- Netlify HTTP 429 / platform throttling.
- Edge Function limits.
- Account/service suspension.
- ISP-specific front/SNI reachability.
- Old Xray clients without stable XHTTP support.
- Misconfigured `TARGET_DOMAIN`, path, or backend port.

## Strategic Value

Netlify XHTTP is a real lane, but it should be treated as disposable rotating infrastructure. It belongs in a fallback portfolio, not as the single stable transport.

