# Cyber Operations Center Engineering Program Architecture

> **Version:** 1.2  
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
                        WireGuard VPN
                               │
                     Omada Network Gateway
                               │
                    ┌──────────┴──────────┐
                    │                     │
               Management LAN        User Network
                    │                     │
             Ubuntu Server         Windows Devices
                    │
         Caddy HTTPS Gateway
                    │
        Docker Container Platform
                    │
 ┌──────────────────┼────────────────────┐
 │                  │                    │
 Monitoring     Security Stack      Infrastructure
 │                  │                    │
 Grafana         Wazuh              Nextcloud
 Prometheus      Suricata           Identity
 NET-WATCH       Zeek               Backup
                 Graylog            Media Server
                 MISP
                 TheHive
                 Cortex
                 Velociraptor
```

---

# Implemented Operations Access Layer

Phase 2 introduced Caddy as the private HTTPS entry point on `coc-srv-01`. It currently serves a static operations portal and will provide reverse-proxy routing for later internal services.

The access layer is protected by the host baseline:

- Ed25519 key-only SSH administration;
- default-deny UFW policy;
- Fail2Ban SSH monitoring;
- AppArmor and Auditd;
- automatic security updates; and
- a private asset registry outside the public web root.

The portal uses Caddy's internal certificate authority. Trust is distributed only after fingerprint verification and does not imply public exposure.

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

# Primary Infrastructure Components

## Network

Responsible for secure connectivity throughout the environment.

Examples include:

- Omada
- VLANs
- Firewall Rules
- VPN
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

## Identity

Responsible for authentication and authorization.

Future capabilities include:

- Active Directory
- Identity Management
- Role-Based Access Control

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

Future capabilities include:

- Automated backups
- Configuration backups
- Disaster recovery testing

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
- Detection Engineering
- Threat Hunting
- Digital Forensics
- Threat Intelligence
- Incident Response
- Automation
- Secure System Administration
- Operational Documentation

Every component deployed should contribute to one or more of these operational capabilities.
