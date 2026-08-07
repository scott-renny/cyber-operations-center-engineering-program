# COC-LT-01 — Phase 8 Endpoint Record

> **Asset:** COC-LT-01  
> **Platform:** Windows 11 Home  
> **Status:** Phase 8 baseline complete  
> **Evidence classification:** Sanitized public record

## Role

COC-LT-01 is a roaming administrative and analysis endpoint. Its baseline assumes that the device may operate on trusted home networks and untrusted external networks.

## Control summary

| Domain | Implemented outcome |
|---|---|
| Platform trust | TPM 2.0 and Secure Boot verified |
| Local authentication | Windows Hello PIN configured |
| Endpoint protection | Defender controls reviewed and enabled |
| Network access | Split and full WireGuard profiles validated |
| Untrusted networks | Full tunnel, controlled DNS, and kill switch |
| Monitoring | Wazuh agent and real-time FIM validated |
| Browser | Firefox privacy and security baseline applied |
| Identity | Hardware key enrolled for Microsoft and Bitwarden |
| Exposure | Public HTTP/HTTPS rules removed; remote administration requires VPN |

## Documentation map

1. [Endpoint hardening](01-endpoint-hardening.md)
2. [WireGuard](02-wireguard.md)
3. [Windows security](03-windows-security.md)
4. [Wazuh agent](04-wazuh-agent.md)
5. [Browser hardening](05-browser-hardening.md)
6. [Identity security](06-identity-security.md)
7. [Firewall changes](07-firewall.md)
8. [Validation results](08-validation.md)
9. [Phase completion report](PHASE-08-COMPLETION.md)

## Publication note

Live addresses, keys, endpoints, account identifiers, recovery codes, device identifiers, and raw screenshots are intentionally excluded.
