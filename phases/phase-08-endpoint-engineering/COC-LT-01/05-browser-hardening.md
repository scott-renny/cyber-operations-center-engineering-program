# COC-LT-01 Browser Hardening

## Scope

Firefox is the hardened daily-use browser on COC-LT-01.

## Implemented controls

- Enhanced Tracking Protection configured.
- uBlock Origin installed for content and tracker blocking.
- Cookie AutoDelete installed for session-data reduction.
- Bitwarden installed for managed credential use.
- Browser privacy and security settings reviewed.

## Operating guidance

- Install extensions only from trusted publisher pages.
- Keep the extension set small to reduce browser attack surface.
- Review site exceptions periodically.
- Use private browsing for authentication tests when validating a new factor.
- Treat certificate or authentication warnings as investigation points rather than bypass prompts.
- Keep Firefox and extensions updated.

## Limitations

Browser hardening reduces common tracking, malicious-content, and credential-handling risks but does not replace endpoint protection, secure DNS, VPN policy, or hardware-backed authentication.
