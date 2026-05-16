# Governance

The knowledge base should be useful, public-readable, and resilient. It should not become a pastebin of working bypass parameters.

## Public Notes

Safe for GitHub:

- Architecture diagrams
- Method comparisons
- Source links
- Code-level summaries
- Failure modes
- Carrier/ISP observations at a high level
- Redacted screenshots
- Historical timelines

Keep out of public GitHub:

- Raw active IP lists
- Working configs copied verbatim
- Credentials, UUIDs, private keys, tokens, or relay URLs
- One-click setup instructions for fragile live paths
- User-specific carrier/operator recipes
- Anything that turns the repo into a blocklist source

## Evidence Levels

| Level | Meaning |
| --- | --- |
| L0 rumor | Unsourced claim, keep as lead only. |
| L1 public post | Telegram/X/blog claim, useful but needs verification. |
| L2 config artifact | Public config or screenshot, can classify architecture. |
| L3 source code | Repository confirms implementation behavior. |
| L4 live test | Reproducible test with date, ISP, and redacted details. |
| L5 multi-operator validation | Same method confirmed across carriers or regions. |

## Method Status

Use these statuses in method cards:

- `concept` - plausible idea, not confirmed.
- `observed` - seen in public posts or configs.
- `implemented` - source code confirms behavior.
- `field-active` - currently reported working somewhere.
- `degrading` - evidence shows shrinking availability.
- `burned` - no longer working in observed environments.
- `unknown` - insufficient recent evidence.

## Review Questions

Before publishing a new note:

- Does this help compare systems, or only help copy a fragile setup?
- Could the note be used as a blocklist directly?
- Are operational details redacted?
- Is the date and evidence level clear?
- Does it distinguish one ISP from general Internet behavior?

