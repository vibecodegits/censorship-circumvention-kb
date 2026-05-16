# Findings: Netlify XHTTP Debug, 2026-05-15

Evidence level: `L4`

Source artifact: `netlify_xhttp_debug_2026-05-15.md`

## Isolation Result

The important debug result was:

```text
backend Cloudflare Tunnel + same Xray user: works
Netlify relay + same backend + same Xray user: fails with Netlify 429
```

That means the failure was not primarily:

- UUID/user mismatch
- Xray backend failure
- 3x-ui inbound failure
- Kubernetes/Let's Encrypt front-domain failure

The failing layer was Netlify.

## Likely Cause

The pattern matched Netlify platform-level throttling or abuse/rate protection triggered by real XHTTP relay traffic.

## Upstream Comparison

The local/deployed relay was older and simple: it forwarded the incoming path/query to `TARGET_DOMAIN`. The upstream `amirshaker000/netlify-relay` had evolved toward configurable paths, optional serverless function mode, timeout handling, throttling behavior, and stricter header forwarding.

## Practical Conclusion

Netlify is useful as a rotating/disposable relay lane. It should not be the only lane for family connectivity.

Better posture:

- Keep direct backend fallback.
- Rotate fresh Netlify apps and paths.
- Test upstream serverless/proxy modes.
- Keep a separate Google/MHR/Goose emergency lane.
- Log ISP, resolver, front domain, mode, and failure text for each field test.

