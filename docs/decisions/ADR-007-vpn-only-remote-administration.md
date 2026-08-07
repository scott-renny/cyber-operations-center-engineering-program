# ADR-007: Require VPN-only remote administration

- **Status:** Accepted
- **Date:** 2026-08-07
- **Owner:** COC Program Owner
- **Related phase(s):** Phase 8
- **Related asset(s):** COC-LT-01

## Context

Public HTTP and HTTPS forwarding exposed management and internal web services directly to Internet-originated traffic. WireGuard was already available as an authenticated, encrypted remote-access boundary.

## Decision

Remove unnecessary public HTTP/HTTPS forwarding and require WireGuard before remote administrative access. Retain only the approved WireGuard UDP entry point for this access path.

## Alternatives Considered

Continue direct publication with application authentication; add further reverse-proxy controls; restrict public web access by source address; require VPN access.

## Rationale

VPN-first access reduces exposed services, centralizes the remote-access boundary, and preserves private management-plane design. It is easier to validate and monitor than multiple directly published administrative services.

## Security Implications

WireGuard availability and key protection become critical. Host firewalls, service authentication, patching, and monitoring remain required because VPN access does not make a client or service inherently trusted.

## Consequences

Remote administration depends on a working VPN profile. Troubleshooting must use an approved local path or a validated recovery procedure rather than temporarily restoring public exposure.

## Validation

Review `ufw status`, confirm public HTTP/HTTPS rules are absent, confirm WireGuard remains reachable, and verify internal services through the VPN.

## Review Date or Trigger

Review after a remote-access architecture change, WireGuard control failure, or introduction of a formally approved alternative access broker.
