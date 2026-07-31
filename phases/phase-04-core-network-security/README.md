# Phase 4 — Core Network and Security Services

**Status:** Complete  
**Completion date:** 2026-07-31  
**Budget:** $0  
**Asset ID:** `coc-srv-01`  
**Friendly name:** Atlas

## Goal

Establish the first integrated network and security services on Atlas while preserving household-network stability and maintaining a documented path to the future Project Olympus network architecture.

## Scope

Phase 4 delivered:

- a persistent server address outside the router's dynamic allocation pool;
- router and wireless hardening within the controls exposed by the ISP equipment;
- a WireGuard remote-access VPN;
- Wazuh security monitoring and dashboard services;
- Pi-hole DNS filtering as a controlled pilot;
- ClamAV malware detection with scheduled targeted scanning;
- UFW restrictions for LAN and VPN administration;
- prepared Suricata configuration and rules, with activation deliberately deferred; and
- validation of service health, DNS filtering, remote VPN access, malware alerting, memory, and storage.

The phase prioritized stability over maximum feature activation. Controls that were unsafe on the temporary Wi-Fi uplink or dependent on unfinished Project Olympus infrastructure were documented and deferred.

## Architecture

```text
Remote phone
    │
    │ WireGuard VPN
    ▼
ISP router ───────── trusted LAN clients
    │                         │
    └──────────────┬──────────┘
                   ▼
             Atlas (Ubuntu)
                   │
      ┌────────────┼─────────────┬─────────────┐
      ▼            ▼             ▼             ▼
   Caddy        Pi-hole        Wazuh         ClamAV
   Dockge       DNS filter     SIEM/XDR      malware scan
      │
      ▼
   Docker
```

Suricata is installed and prepared but remains stopped until Atlas uses wired Ethernet. Starting AF_PACKET capture on the temporary Broadcom Wi-Fi interface caused loss of connectivity during testing; the rollback restored service.

## Implemented services

| Component | Validated state |
|---|---|
| Ubuntu Server | 24.04.4 LTS |
| Caddy | Active |
| Docker and Dockge | Active; Dockge healthy |
| WireGuard | Active, enabled at boot, remote handshake validated |
| Wazuh | Manager, indexer, dashboard, and Filebeat active |
| Pi-hole | Healthy; DNS resolution and blocking validated |
| ClamAV | Daemon and signature updater active |
| Scheduled malware scan | Daily timer enabled with timezone-specific schedule |
| Suricata | Installed, configured, tested, intentionally disabled |
| UFW | Active with LAN/VPN-scoped management rules |

Versions record the validated completion state and are not immutable pins for future maintenance.

## Network baseline

Atlas uses a persistent private address outside the router's DHCP pool. The gateway and upstream DNS remain provided by the ISP router during the transitional design.

The router configuration was reviewed and hardened as follows:

- administrator credentials changed and stored outside the repository;
- UPnP disabled;
- WPS disabled on both wireless access points;
- DMZ disabled;
- SPI and anti-DoS protections enabled;
- unsolicited WAN ping responses discarded;
- stale port-forwarding configuration removed;
- only the WireGuard UDP forwarding rule retained;
- guest and smart-device networks kept disabled; and
- dynamic DNS left disabled to avoid adding an unnecessary availability dependency.

Ordinary household devices remain on DHCP. Additional address reservations and network segmentation are deferred until Project Olympus defines the permanent subnets and VLANs.

## WireGuard remote access

WireGuard provides authenticated access from a mobile peer to the management network. The server tunnel uses a dedicated private subnet and performs forwarding and NAT through the current uplink.

Security controls include:

- server and peer private keys stored outside version control;
- server configuration restricted to root;
- a single-purpose inbound UDP firewall rule;
- peer-specific tunnel addressing;
- split-tunnel routing limited to the VPN and trusted LAN;
- persistent keepalive for mobile-network reliability; and
- successful cellular handshake and data-transfer validation.

No private key, peer identity, public endpoint, live address, QR code, or credential is included in the public record.

## Wazuh monitoring

Wazuh was installed as an all-in-one deployment with the indexer, manager, dashboard, and Filebeat services. The local host is monitored as the manager's built-in agent.

Validated capabilities include:

- Security Configuration Assessment;
- file-integrity monitoring;
- system and software inventory;
- vulnerability scanning;
- system journal collection;
- Pi-hole operational warning/error collection;
- ClamAV detection collection; and
- prepared Suricata EVE JSON collection for future activation.

The dashboard is restricted to trusted LAN and VPN sources. Generated credentials and the installation credential archive remain outside the repository.

## Pi-hole DNS filtering

Pi-hole runs as a Dockge-managed Docker Compose stack. DNS and the administrative interface bind only to the server's private LAN address.

The deployment includes:

- persistent configuration and log storage;
- a Docker secret for the web password;
- DNSSEC validation;
- explicit upstream resolvers;
- local name resolution for Atlas;
- a controlled Windows workstation pilot;
- mobile DNS filtering over WireGuard;
- the default StevenBlack list; and
- HaGeZi Multi PRO after controlled validation.

Household-wide DHCP advertisement of Pi-hole is intentionally deferred. The current server depends on Wi-Fi, so making it the only resolver for every device would create an avoidable household availability risk.

## ClamAV malware scanning

ClamAV runs as a host service with automatic signature updates. A targeted scan covers approved data and service paths through a systemd oneshot service and daily timer.

The timer uses an explicit America/Toronto schedule while the server retains UTC for consistent security telemetry.

The EICAR antivirus test file was detected successfully, removed immediately, logged by ClamAV, and converted by Wazuh into a level-8 virus-detection alert. No live malware was used.

## Firewall policy

UFW retains a default-deny inbound policy. Administrative and application access is restricted as follows:

- SSH: trusted LAN and WireGuard subnet;
- Caddy HTTP/HTTPS: trusted LAN and WireGuard subnet;
- Dockge HTTPS: trusted LAN and WireGuard subnet;
- Wazuh dashboard: trusted LAN and WireGuard subnet;
- Pi-hole DNS and dashboard: trusted LAN and WireGuard subnet; and
- WireGuard UDP: internet-facing entry point.

Broad IPv4 and unnecessary IPv6 management rules were removed after replacement rules were validated from a second session.

## Validation checklist

- [x] Persistent server addressing validated
- [x] Default route and DNS resolution validated
- [x] Router hardening settings reviewed
- [x] WireGuard starts at boot
- [x] Mobile peer handshake validated over cellular
- [x] VPN data transfer and LAN access validated
- [x] Wazuh core services active
- [x] Wazuh dashboard accessible from an approved network
- [x] Pi-hole container healthy
- [x] Normal DNS resolution succeeds
- [x] Listed advertising domain returns the configured blocking response
- [x] Pi-hole filtering works through the mobile VPN
- [x] ClamAV daemon and signature updater active
- [x] EICAR test detected and reported by Wazuh
- [x] Daily malware-scan timer enabled
- [x] UFW broad management rules removed after scoped-rule validation
- [x] Suricata inactive and disabled by design
- [x] Memory and storage capacity remain healthy
- [x] Public documentation sanitized

## Troubleshooting record

### Suricata disrupted the temporary Wi-Fi uplink

Suricata's AF_PACKET capture was pointed at the Broadcom wireless interface because Ethernet was not yet connected. Starting the service caused the wireless path to lose usable connectivity, which also interrupted SSH and web dashboards.

Local console access was used to restart the Netplan-managed WPA supplicant. Connectivity recovered, and Suricata was disabled. Suricata will not be re-enabled until wired Ethernet is available and the capture path is revalidated.

### Bookmarked dashboards stopped resolving after the address change

The administrative workstation contained a static hosts-file entry for the server's former address. Updating and later removing the stale entry restored access after Pi-hole assumed local-name resolution.

### WireGuard service showed inactive after manual startup

The interface had been started directly with `wg-quick`, so systemd did not own the running instance. The interface was brought down and restarted through `wg-quick@wg0`, after which systemd correctly reported the service as active.

### Pi-hole log inspection used unsupported BusyBox options

The container's BusyBox `find` implementation did not support GNU `-printf`. A portable shell loop was used instead, and persistent log mounts were added before Wazuh integration.

## Security considerations

- Secrets, keys, tokens, live addresses, public endpoints, MAC addresses, and credential archives are excluded.
- The server remains on a transitional trusted LAN without VLAN isolation.
- Pi-hole is not yet a household-wide dependency.
- Suricata monitoring is unavailable until the wired migration.
- Wazuh and management dashboards are restricted to trusted LAN and VPN sources.
- Router dynamic DNS remains disabled.
- Router remote administration, DMZ, UPnP, WPS, guest networking, and smart-device networking remain disabled.
- Firewall changes were validated before broad rules were removed.

## Lessons learned

- A valid IDS configuration test does not prove that a capture method is safe for the active interface.
- Remote network changes require a local recovery path and staged validation.
- DNS migrations must account for local hosts-file overrides and resolver caches.
- A security service should not become a household-wide dependency until its platform and network path are resilient.
- Systemd should own long-running interfaces and services intended to start at boot.
- Harmless test artifacts can validate an end-to-end malware detection pipeline without using real malware.
- Public evidence should prove control state without exposing operational identifiers.

## Known limitations and Project Olympus deferrals

- Atlas remains connected through Wi-Fi.
- Suricata remains inactive and disabled.
- The LAN remains flat and controlled by ISP equipment.
- Pi-hole is limited to pilot clients and VPN peers.
- DHCP remains on the ISP router.
- VLANs, guest isolation, IoT isolation, and permanent address planning are pending.
- Wi-Fi naming and final wireless security redesign are pending.
- Dynamic DNS is not configured; a public-address change may temporarily interrupt remote VPN access without affecting household internet.

## Evidence

Sanitized validation results and the public-release decision are recorded in [evidence/README.md](evidence/README.md).

## Outcome

Atlas now provides a stable VPN, DNS-filtering, security-monitoring, malware-detection, reverse-proxy, firewall, and container-management baseline. Phase 4 is complete, with network-wide controls deliberately staged for Project Olympus rather than introduced on the temporary Wi-Fi architecture.

The environment is ready for **Phase 5 — Backup and Recovery** while Project Olympus remains a separately controlled network-modernization dependency.
