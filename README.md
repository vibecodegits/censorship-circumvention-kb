# Censorship Circumvention Knowledge Base

Last checked: 2026-05-20

This knowledge base is for organizing what we know about censorship circumvention approaches, with enough structure to compare methods without turning the notes into a fragile feed of raw working configs.

The useful unit is not "a config that works today." It is a method family, its assumptions, its dependencies, and the evidence that it is still alive or getting squeezed.

## Goals

- Build a durable map of method families and how they fail.
- Track public projects, posts, and discussions as evidence.
- Separate reusable architecture from short-lived operational details.
- Make it easy to compare DNS, Google, CDN, DPI, relay, and client-level approaches.
- Keep sensitive or fast-burning artifacts out of the public notes.

## Repo Shape

- `docs/taxonomy.md` - method families and where each one fits.
- `docs/architecture-map.md` - bigger-picture model of components and tradeoffs.
- `docs/source-inventory.md` - current public sources and repository list.
- `docs/session-inventory.md` - local Codex session inventory and what each contributed.
- `docs/telegram-sources.md` - Telegram source handling rules and channel-first guidance.
- `docs/methods/` - reusable method cards.
- `docs/governance.md` - publication, redaction, and evidence rules.
- `docs/findings/` - dated research notes from chats, posts, and code review.
- `docs/templates/` - templates for new method cards and source cards.

## Working Rules

- Prefer primary sources: source code, official docs, original posts, reproducible public logs.
- Cite every claim that depends on a source.
- Keep raw IP lists, active configs, private relays, credentials, and user-specific setup details out of public docs.
- Track "works for whom" separately from "works in general"; ISP and mobile operator differences matter.
- Treat reachability as separate from tunnel compatibility. An open CDN IP is not automatically useful.

## Current High-Level Picture

The current evidence points to four durable categories:

- DNS/control-plane methods: resilient for discovery or low-bandwidth channels, weaker for full browsing.
- Google-collateral methods: often more stable because blocking has high collateral cost.
- CDN-fronting methods: powerful when available, but edge IP/SNI combinations burn quickly.
- DPI/SNI evasion methods: useful as helpers, but fragile when middleboxes improve reassembly and fingerprinting.

The likely strategic pattern is a layered system: DNS or other low-friction bootstrap, Google/collateral transport where possible, CDN/Psiphon fallbacks, and a client that can rotate tactics without exposing raw working material as the product.

## Current Method Cards

- [Google Apps Script relay family](docs/methods/google-apps-script-relays.md)
- [Netlify XHTTP relay](docs/methods/netlify-xhttp-relay.md)
- [Vercel XHTTP relay](docs/methods/vercel-xhttp-relay.md)
- [Psiphon / Shir-o-Khorshid CDN fronting](docs/methods/psiphon-cdn-fronting.md)
- [DNS bootstrap and tunnels](docs/methods/dns-bootstrap-and-tunnels.md)
- [MITM domain fronting / local helper fronting](docs/methods/mitm-domain-fronting.md)
- [Twoman host-preserving relay](docs/methods/twoman-host-preserving-relay.md)
- [Google-collateral direct fragmentation](docs/methods/google-collateral-fragmentation.md)
- [Fake ClientHello SNI spoofing](docs/methods/fake-clienthello-sni-spoofing.md)
