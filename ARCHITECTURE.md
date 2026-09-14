# Cyber Operations Center Engineering Program Architecture

> **Version:** 1.4  
> **Status:** Active Development

---

# Purpose

This document defines the overall architecture of the Cyber Operations Center Engineering Program.

Rather than documenting individual services independently, this document explains how every system contributes to the overall security architecture and operational capabilities of the environment.

Every technology deployed within this project should support one or more operational objectives.

---

# Architectural Goals

The architecture is designed to achieve the following goals:

- Enterprise-inspired design
- Defense in Depth
- Zero Trust networking
- High visibility
- Secure remote administration
- Operational resilience
- Scalability
- Modular growth
- Centralized monitoring
- Automation
- Comprehensive documentation

---

# Core Design Principles

## Security by Design

Security is considered before deployment rather than after implementation.

---

## Defense in Depth

Multiple security controls are layered throughout the environment.

Examples include:

- Network segmentation
- Host hardening
- Endpoint monitoring
- Intrusion detection
- Log aggregation
- Threat intelligence
- Continuous monitoring

---

## Zero Trust

No user, endpoint, or service is automatically trusted.

Authentication and authorization are continuously validated wherever practical.

---

## Observability

Every critical component should produce telemetry.

Telemetry should be centralized whenever possible for monitoring, troubleshooting, and detection engineering.

---

## Automation

Repetitive operational tasks should eventually become automated.

Examples include:

- Container deployment
- Configuration management
- Alerting
- Backups
- Health monitoring
- Incident response workflows

---

# High-Level Architecture

```
                           Internet
                               │
                               │
                        Private Access
                               │
                     Network Gateway
                               │
                    ┌──────────┴──────────┐
                    │                     │
               Management LAN        User Network
                    │                     │
             Ubuntu Server         Windows Devices
                    │                     │
         Caddy HTTPS Gateway       Phase 10 Identity Lab
                    │                     │
        Docker Container Platform      DC01 / AD DS / DNS
                    │
 ┌──────────────────┼────────────────────┐
 │                  │                    │
 Monitoring     Security Stack      Infrastructure
 │                  │                    │
 Grafana         Wazuh              Nextcloud
 Prometheus      Suricata           Backup
 NET-WATCH       Zeek               Media Server
                 Graylog
                 MISP
                 TheHive
                 Cortex
                 Velociraptor
```

---

# Implemented Operations Access Layer

Phase 2 introduced Caddy as the private HTTPS entry point on `coc-srv-01`. It currently serves a static operations portal and provides reverse-proxy routing for internal services.

The access layer is protected by the host baseline:

- Ed25519 key-only SSH administration;
- default-deny UFW policy;
- Fail2Ban SSH monitoring;
- AppArmor and Auditd;
- automatic security updates; and
- a private asset registry outside the public web root.

The portal uses Caddy's internal certificate authority. Trust is distributed only after fingerprint verification and does not imply public exposure.

---

# Implemented Nextcloud File Access & Sync

Phase 9 completed on September 10, 2026 EDT / September 11 UTC. Nextcloud 34.0.3 file access and sync is complete on Atlas, with Tailscale private access through a canonical HTTPS hostname and Caddy, tested Restic backup and database restore, Wazuh FIM alert validation, EICAR-tested ClamAV, working 2FA and outbound email, configured Windows 11 and Windows 10 clients, and successful reboot persistence. Galaxy S25 and Tab A11 Nextcloud onboarding are intentionally deferred and are not Phase 9 blockers.

The implemented Nextcloud path is Windows client → Tailscale/private DNS → canonical HTTPS hostname → Caddy → loopback-bound Nextcloud Apache, with PostgreSQL, Redis and a separate cron container. See the [Phase 9 completion record](phases/phase-09-nextcloud/README.md).

---

# Implemented Phase 10 Identity Baseline

Phase 10 uses an isolated VirtualBox lab on the Windows 11 laptop so the identity environment is portable and attack traffic does not need to traverse the home LAN. The current domain controller is Windows Server 2025 Standard Evaluation running AD DS and DNS for `corp.lab.test`.

The baseline currently includes:

- `DC01` as the authoritative domain controller and DNS server;
- Windows Server 2025 domain and forest functional levels;
- repaired and validated AD-integrated `corp.lab.test` and `_msdcs.corp.lab.test` DNS zones;
- protected organizational units for users, privileged accounts, service accounts, workstations, servers, and groups;
- Global Security role groups and Domain Local permission groups following an AGDLP-style model;
- separate everyday, administrative, and Tier-0 identities;
- Tier-0 membership in Protected Users with delegation disabled;
- a strengthened password and lockout baseline;
- a KDS root key and Group Managed Service Account reference design; and
- a deliberately isolated legacy service identity with an SPN for later Kerberoasting exercises.

The lab keeps secure and intentionally vulnerable identities separate so defensive controls can be compared against realistic legacy attack paths. GPO-based privileged-logon boundaries, the Windows 11 domain client, Kali attacker, Wazuh/Sysmon telemetry, controlled identity attacks, incident-response records, and vulnerability-management work remain in progress.

See the [Phase 10 identity-services record](phases/phase-10-identity-services/README.md).

---

# Implemented Container Platform

Phase 3 introduced Docker Engine, Docker Compose, and Dockge on `coc-srv-01`.

Dockge's native HTTP service is bound to `127.0.0.1` and is reachable from the trusted LAN only through a dedicated Caddy HTTPS endpoint. The firewall permits that endpoint only from the trusted local network. Dockge has access to the Docker socket and is treated as a privileged administrative control plane.

Every later Compose stack follows these network conventions:

```yaml
networks:
  frontend:
    driver: bridge
  backend:
    driver: bridge
    internal: true
```

User-facing services use `frontend`. Private dependencies such as databases use only `backend`. Dual-homed services require review because they can relay traffic between networks.

Stack directories, service names, and explicit container names use descriptive lowercase kebab-case. Operational labels identify the program, deployment phase, and workload role.

Docker uses the `json-file` logging driver with a 10 MB maximum file size and three retained files per container. Compose file-backed secrets are used when applications support `/run/secrets/<name>`; source files require mode `0600` and remain outside version control. These secrets reduce environment-variable exposure but are not encrypted at rest.

Docker Swarm remains disabled because Dockge manages ordinary Compose stacks. A second orchestration model will be introduced only through an explicit architecture decision.

---

# Implemented Endpoint Security Layer

Phase 8 established platform-appropriate baselines for the Windows 11 Home laptop, legacy Windows 10 migration source, Galaxy phone, and Galaxy tablet.

The layer combines native protections and firewalls; current patching; private portable-device access; Wazuh monitoring for Windows; Sysmon on the legacy workstation; validated hardware-key authentication; mobile permission, recovery, and installation controls; and encrypted, restore-tested workstation migration data.

The legacy workstation has no TPM and remains unencrypted under a time-bounded exception. Phase 8.5 will replace it with Linux Mint Cinnamon. Production acceptance requires verified installation media, UEFI Secure Boot, full-disk encryption with tested recovery, AppArmor, UFW, current updates, Wazuh Linux telemetry, selective data restoration, and a restore-tested Mint backup.

Public records exclude live addresses, unique identifiers, VPN or agent keys, recovery material, and account details.

---

# Primary Infrastructure Components

## Network

Responsible for secure connectivity throughout the environment.

Examples include:

- Network gateway and segmentation
- VLANs
- Firewall rules
- Private remote access
- DNS
- DHCP

---

## Compute

Provides the execution platform for services.

Examples include:

- Ubuntu Server
- Docker
- Containers
- Virtual Machines

---

## Administration Workstation

Linux Mint Cinnamon is the primary daily-driver, administration, and learning workstation. It is a client and management endpoint, not a replacement for the Ubuntu Server service host.

The workstation uses Docker and Docker Compose as the beginner-first container workflow, with Podman retained for later comparative learning. KVM/QEMU, libvirt, and virt-manager provide local virtual machines. SSH, Git/GitHub CLI, Python/uv, Ansible, AWS CLI, Terraform or OpenTofu, kubectl, Helm, k9s, Wireshark, Nmap, CyberChef, Remmina, Syncthing, LocalSend, and password-manager/security-key tooling are introduced progressively when required.

Package instructions use Linux Mint/Ubuntu `apt` sources and compatible vendor repositories. Fedora `dnf` and RPM Fusion instructions are historical only; see [ADR-012](docs/decisions/ADR-012-linux-mint-cinnamon-primary-workstation.md).

---

## Identity

Responsible for authentication, authorization, privileged-access design, and identity-focused detection practice.

Implemented Phase 10 capabilities include:

- Windows Server 2025 Active Directory Domain Services
- AD-integrated DNS
- organizational-unit and security-group design
- AGDLP-style role and permission nesting
- separate everyday, administrative, and Tier-0 identities
- Protected Users and non-delegable Tier-0 credentials
- Group Managed Service Account foundations
- controlled legacy service-account attack paths

Planned Phase 10 capabilities include:

- Group Policy hardening and privileged-logon boundaries
- Windows 11 domain-client administration
- Wazuh/Sysmon identity telemetry
- controlled password-spray and Kerberoasting exercises
- incident-response documentation
- vulnerability-management validation

---

## Monitoring

Provides operational awareness.

Examples include:

- Grafana
- Prometheus
- NET-WATCH

---

## Detection Engineering

Responsible for identifying malicious activity.

Examples include:

- Wazuh
- Zeek
- Suricata
- Graylog

---

## Threat Intelligence

Collects and correlates indicators of compromise.

Examples include:

- MISP

---

## Incident Response

Supports investigation and response.

Examples include:

- TheHive
- Cortex

---

## Digital Forensics

Supports endpoint investigations.

Examples include:

- Velociraptor

---

## Backup

Ensures recoverability.

Capabilities include:

- automated backups
- configuration backups
- restore validation
- disaster-recovery testing

---

# Data Flow Philosophy

Information should move through the environment in a logical and observable manner.

Typical workflow:

Endpoints

↓

Security Sensors

↓

Log Collection

↓

Detection Engine

↓

Threat Intelligence

↓

Incident Response

↓

Analyst Investigation

↓

Lessons Learned

↓

Continuous Improvement

---

# Architectural Decision Records

Major architectural decisions should be documented using Architecture Decision Records (ADRs).

The current decision process, template, and accepted records are indexed in [docs/decisions/README.md](docs/decisions/README.md).

Examples include:

- Technology selections
- Network design decisions
- Security trade-offs
- Deployment strategies
- Major infrastructure changes

---

# Scalability

The architecture is intentionally modular.

Future services should integrate into the existing architecture without requiring significant redesign.

---

# Long-Term Vision

The Cyber Operations Center Engineering Program is designed to evolve into a fully documented enterprise-inspired security environment capable of demonstrating:

- Infrastructure Engineering
- Security Operations
- Identity Security
- Detection Engineering
- Threat Hunting
- Digital Forensics
- Threat Intelligence
- Incident Response
- Automation
- Secure System Administration
- Operational Documentation

Every component deployed should contribute to one or more of these operational capabilities.
