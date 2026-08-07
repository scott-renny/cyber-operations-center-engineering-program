# COC-LT-01 Firewall and Exposure Changes

## Decision

Remote administration now requires WireGuard. Unnecessary public HTTP and HTTPS forwarding rules were removed, while the WireGuard UDP entry point was retained.

## Architecture change

```text
Before:
Internet -> public HTTP/HTTPS forwarding -> internal services

After:
Internet -> WireGuard VPN -> private management plane -> internal services
         X public HTTP/HTTPS forwarding
```

## Completed validation

- The VPN endpoint firewall state was reviewed with `ufw status`.
- Unnecessary public HTTP/HTTPS allowances were absent.
- The WireGuard path remained available.
- Internal web services remained reachable through the approved private path.

## Security effect

The change reduces the public attack surface and makes VPN authentication and encryption the boundary for remote administrative access. Host firewalls and service authentication remain necessary defense-in-depth controls.

## Rollback principle

If remote access fails, diagnose WireGuard, DNS, routing, and firewall state from an approved local path. Do not restore public web exposure as an undocumented convenience measure.
