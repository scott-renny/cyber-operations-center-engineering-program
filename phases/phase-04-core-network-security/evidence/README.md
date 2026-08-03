# Phase 4 Validation Evidence

**Status:** Complete  
**Evidence classification:** Public, sanitized  
**Validation date:** 2026-07-31  
**Asset:** Atlas (`coc-srv-01`)

## Publication decision

This record contains outcome-level evidence only. The following were intentionally excluded:

- private or public cryptographic keys;
- account names beyond the documented asset identity;
- passwords, tokens, QR codes, and credential archives;
- live private and public IP addresses;
- peer endpoints and carrier addresses;
- MAC addresses and wireless BSSIDs;
- unredacted router or dashboard screenshots;
- full firewall exports that disclose operational addressing; and
- raw logs containing identifiers not required to prove the control.

## Validation summary

| Control | Sanitized observation | Result |
|---|---|---|
| Server address | Persistent private address present on the approved interface | Pass |
| Routing | Default route used the expected ISP gateway | Pass |
| DNS | External name resolution succeeded | Pass |
| Router hardening | UPnP, WPS, DMZ, guest network, smart-device network, and DDNS disabled | Pass |
| Router protection | High firewall, SPI/anti-DoS, and WAN ping discard enabled | Pass |
| WireGuard service | Interface active and listening on the approved UDP port | Pass |
| WireGuard persistence | systemd unit active and enabled | Pass |
| Mobile VPN | Recent cellular handshake and bidirectional transfer observed | Pass |
| Managed laptop DNS | Atlas local hostname resolved through the approved Pi-hole resolver | Pass |
| Managed laptop SSH | Dedicated Ed25519 key accepted; client and server fingerprints matched | Pass |
| Caddy | Service active | Pass |
| Docker | Service active | Pass |
| Dockge | Container healthy | Pass |
| Wazuh | Indexer, manager, dashboard, and Filebeat active | Pass |
| Pi-hole | Container healthy | Pass |
| Normal DNS | Approved software-development domain resolved normally | Pass |
| DNS blocking | Known advertising domain returned the configured blocking address | Pass |
| VPN DNS | Mobile client resolved through Pi-hole over WireGuard | Pass |
| ClamAV | Daemon and signature updater active | Pass |
| Malware test | EICAR signature detected and test file removed | Pass |
| Wazuh malware alert | Level-8 ClamAV detection alert generated | Pass |
| Scheduled scan | Daily timer enabled for 03:15 America/Toronto | Pass |
| UFW | Management services restricted to trusted LAN and VPN | Pass |
| Suricata safety state | Service inactive and disabled pending wired Ethernet | Pass |
| Memory | 15 GiB installed; approximately 11 GiB available at final check | Pass |
| Storage | 226 GiB filesystem; approximately 190 GiB available at final check | Pass |

## Service-state evidence

At the final health check, the following services reported active:

- Caddy
- Docker
- WireGuard
- Wazuh indexer
- Wazuh manager
- Wazuh dashboard
- Filebeat
- ClamAV daemon
- ClamAV signature updater

Suricata reported inactive and disabled. This is the approved Phase 4 state, not a failed validation.

## Functional evidence

### DNS resolution and blocking

An approved normal domain returned a routable public address through Pi-hole. A known advertising domain returned `0.0.0.0`, confirming list-based blocking.

The specific resolver address and client identifiers were withheld.

### WireGuard

The server reported:

- the expected peer;
- a recent handshake;
- bidirectional byte transfer; and
- the peer-specific tunnel address.

Keys, endpoint details, and exact addressing were withheld.

### Managed laptop administration

The managed Windows laptop resolved Atlas through the approved local DNS service and completed SSH public-key authentication using its dedicated Ed25519 identity. The client-side public-key fingerprint matched the authorized key recorded on Atlas, and the server journal recorded an accepted public-key login.

The live laptop address, public-key material, username, source port, and raw authentication log were withheld.

### Malware detection

The industry-standard EICAR test string produced:

- a ClamAV `FOUND` result;
- a ClamAV log entry;
- a Wazuh `ClamAV: Virus detected` alert at level 8; and
- immediate deletion of the test artifact.

No real malware was introduced.

### Resource capacity

The final health check showed approximately:

- 11 GiB of memory available;
- negligible swap use;
- 190 GiB of filesystem capacity available; and
- 12 percent root-filesystem utilization.

## Exceptions and deferred validation

Suricata successfully passed configuration and rule-loading tests, including the local rule file. Runtime capture was not accepted because the temporary Wi-Fi interface lost connectivity during activation.

Runtime IDS validation will be repeated after Project Olympus supplies wired Ethernet and the final monitored interface.

Household-wide Pi-hole validation is also deferred. Pilot workstation and VPN-client validation are sufficient for Phase 4 without making a Wi-Fi-hosted server a mandatory resolver for every household device.

## Evidence integrity

This evidence was transcribed from direct command output and administrative interfaces during the implementation session. Raw evidence remains private because it contains operational addressing and identifiers. The public record preserves the control result, approximate capacity where useful, and the reason for each redaction.
