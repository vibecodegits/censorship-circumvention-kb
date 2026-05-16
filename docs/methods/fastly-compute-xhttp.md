# Method: Fastly Compute / Fastly Fronting

Status: `concept`
Evidence level: `L1-L2`
Last reviewed: 2026-05-16

## Summary

Fastly can host edge compute and route requests for domains/services the operator controls. It should be separated from claims about abusing arbitrary third-party Fastly-hosted domains as fronts.

## Related Sources

- Local `fastly-xhttp-compute` experiment based on Fastly JavaScript Compute starter.
- 2026-04-28 session on Fastly worker/fronting domain support.

## Family

- Transport: HTTPS through Fastly edge.
- Relay/egress: Fastly Compute or Fastly-configured backend.
- Camouflage: provider-collateral edge traffic only when using owned/authorized services.

## Key Distinction

Owned Fastly service:

```text
client -> your Fastly domain/service -> your backend
```

Arbitrary public Fastly domain:

```text
client -> third-party Fastly hostname -> your backend
```

The first is a legitimate relay architecture to evaluate. The second is fragile, provider-specific, and not appropriate as public guidance.

## Failure Modes

- Fastly account/service limits.
- Incorrect Host/SNI/certificate assumptions.
- Provider policy enforcement.
- Confusing reachability of a Fastly edge with permission/routing to a backend.

