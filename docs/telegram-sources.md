# Telegram Sources

Last reviewed: 2026-05-16

Telegram is useful for field intelligence, but noisy. The KB should use it as a signal source, not as direct operational truth.

## Source Accounts And Channels

| Source | Type | Priority | Notes |
| --- | --- | --- | --- |
| redacted account context | Telegram account / source lead | High for channels, low for groups | Use the channels available through this account as signal sources. Groups on the account are too noisy unless a specific post/thread is supplied. |
| `Project XHTTP` | Telegram channel/group export | High | Strong signal source for XHTTP, Netlify/Vercel, DNS bootstrap, SNI/fronting, and current field reports. |
| `INTERNETFORIRAN` | Telegram channel | High | Useful curated field updates for Shir-o-Khorshid, Psiphon helper configs, Akamai/Fastly scan state, and current breakage. |
| `xsfilterrnet` | Telegram channel | Medium | Useful for config drops and emerging tricks, but must be architecture-classified before being trusted. |
| `White DNS` | Telegram channel | Medium | Useful for DNS bootstrap and resolver behavior signals. |
| `Duck it / DuckitVPN` | Telegram channel | Low-medium | Keep as background signal unless posts are directly relevant. |

## Channel-First Rule

When mining Telegram through the redacted Telegram account:

- Include channels by default.
- Exclude groups by default.
- Include groups only when the user names a specific group, message link, or date range.
- Downrank raw config-only posts unless they reveal a method family, failure mode, provider dependency, or field-status change.

## Extraction Rules

Capture:

- Date and channel name.
- Method family: DNS, XHTTP, CDN fronting, Google collateral, Psiphon, REALITY, Hysteria/TUIC, etc.
- Provider dependencies.
- ISP/operator context when mentioned.
- Status language: working, unstable, requires DNS bootstrap, blocked, burned, throttled.
- Evidence level.

Do not publish:

- Raw VLESS/VMess/Trojan/SS/WireGuard configs.
- UUIDs, private hosts, subscription URLs, active IP lists, or private relay paths.
- Usernames/passwords or account-specific Telegram metadata.

## Scoring Heuristic

| Signal | Weight |
| --- | --- |
| Channel post explaining a method or provider change | High |
| Channel post reporting broad breakage or recovery | High |
| Multiple independent channel reports for same method | High |
| Group chatter with no reproducible detail | Low |
| Raw config dump without context | Low |
| Config dump plus comments about ISP, DNS, SNI, provider, or failure text | Medium |

