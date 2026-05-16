# Findings: Client Security Audit, 2026-05-10

Evidence level: `L2-L3`

Source session: `Review VPN audit`

## Scope

Claude had produced an audit for the VibeCodeGit VPN app, and Codex implemented the high-impact fixes.

## Durable Lessons

For a censorship-circumvention client, security and lifecycle behavior are not polish. They are core product features.

Important items from the audit/fix:

- Track system-proxy ownership so the app does not leave stale proxy settings behind.
- Recover from stale proxy state on launch.
- Remove unsafe TLS-disable paths from production behavior.
- Gate insecure TLS behavior behind explicit developer-only environment variables.
- Redact secrets in logs.
- Clean up helper processes and proxy state on exit.

## KB Interpretation

Any future client should have a "client safety checklist":

- TLS verification default-on.
- No live secret logging.
- Proxy lifecycle cleanup.
- Crash/quit recovery.
- Explicit user-visible status for what traffic is routed.
- No silent certificate/MITM installation.

