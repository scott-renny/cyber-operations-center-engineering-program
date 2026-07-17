# 🛡️ Cyber Operations Center (COC) Homelab

> **Building an enterprise-inspired Cyber Operations Center from the ground up using open-source technologies, automation, infrastructure engineering, and real-world defensive security workflows.**

---

# Project Evolution

This repository represents a complete redesign of my original cybersecurity home lab projects.

My initial repositories focused on learning individual technologies through standalone labs such as network security, backups, DNS filtering, monitoring, and SOC fundamentals. Those projects provided an excellent foundation and helped me develop practical skills across multiple areas of cybersecurity.

As my knowledge, experience, and long-term goals evolved, I realized that modern security operations are not built from isolated tools—they rely on integrated systems working together.

Rather than continuing to expand several independent repositories, I made the decision to redesign everything from the ground up.

This project consolidates those lessons into a single enterprise-inspired **Cyber Operations Center (COC)**. It brings together infrastructure, networking, monitoring, logging, automation, documentation, and operational workflows into one cohesive environment that reflects how modern Security Operations Centers operate.

The earlier repositories remain available as historical milestones documenting where my learning journey began. This repository is now the primary focus of development and serves as the central hub for future projects, research, experimentation, and continuous improvement.

This project reflects my commitment to continuous learning, technical documentation, thoughtful engineering, and building practical cybersecurity skills through hands-on implementation.

---

# Overview

The Cyber Operations Center Homelab is designed to simulate many of the technologies, processes, and workflows found within enterprise security environments.

Rather than demonstrating isolated labs, this repository documents the design, implementation, operation, and continuous improvement of a complete security-focused infrastructure.

Areas of focus include:

* Security Operations (SOC)
* Detection Engineering
* Threat Hunting
* Incident Response
* Digital Forensics
* Infrastructure Engineering
* System Administration
* Network Security
* Automation
* Documentation
* Continuous Improvement

Every major component is documented from planning through deployment, with an emphasis on understanding **why** technologies are implemented—not just **how** they are configured.

---

# Lab Environment

The Cyber Operations Center is built using a combination of physical devices, virtual machines, containers, and mobile platforms. The environment is intentionally designed to reflect a realistic, multi-platform infrastructure rather than relying on a single workstation.

### Current Environment

* **Windows 10 Desktop** — Primary lab workstation and testing platform
* **Windows 11 Laptop** — Mobile administration, development, and documentation
* **Samsung Galaxy Devices** — Mobile administration, dashboards, notifications, and validation of cross-device functionality

### Planned Infrastructure

* Dedicated **Windows 11 Operations Workstation**
* **Ubuntu Server** hosting self-managed infrastructure and automation
* Additional virtual machines for Active Directory, security testing, and enterprise simulations
* Containerized services using Docker and Docker Compose
* Multi-monitor operations center for monitoring, investigations, dashboards, and administration

As the project evolves, systems will be upgraded, migrated, repurposed, and expanded. The objective is to document the engineering process while building a scalable Cyber Operations Center rather than maintaining a fixed hardware configuration.

---

# Project Goals

* Build an enterprise-inspired Cyber Operations Center
* Develop practical SOC and Blue Team skills
* Gain hands-on experience with enterprise technologies
* Design secure infrastructure using industry best practices
* Create reusable automation and deployment workflows
* Practice system administration and infrastructure engineering
* Document every major implementation and design decision
* Build a professional portfolio that demonstrates continuous learning and technical growth

---

# Architecture

The environment is designed as a modular platform that will continue to expand over time.

```text
                    Internet
                        │
                Router / Firewall
                        │
               ───────────────────
                        │
                 Managed Network
                        │
      ┌──────────────┬──────────────┐
      │              │              │
 Infrastructure   Operations    Management
     Server       Workstations     Systems
      │              │              │
 Docker         Windows Lab     Monitoring
      │              │              │
 SIEM ─────── Logs ─────── Sensors
      │
 Dashboards
```

Additional systems and integrations will be added as the project grows.

---

# Current & Planned Technologies

## Operating Systems

* Windows 11
* Windows Server
* Ubuntu Server
* Kali Linux

## Infrastructure

* Docker
* Docker Compose
* VirtualBox
* Git
* GitHub

## Networking

* DNS
* DHCP
* VLANs
* VPN
* Firewall Management
* Static Addressing

## Security

* Wazuh
* Sysmon
* Windows Event Logging
* Security Onion *(planned)*
* Suricata *(planned)*
* Zeek *(planned)*

## Monitoring

* Grafana
* Prometheus
* Uptime Kuma

## Automation

* Python
* Bash
* PowerShell

---

# Repository Structure

```text
cyber-operations-center-homelab/

├── architecture/
│   ├── diagrams/
│   ├── network/
│   └── documentation/
│
├── cyber-operations-center/
│   ├── dashboards/
│   ├── detections/
│   ├── playbooks/
│   ├── incidents/
│   └── reports/
│
├── engineering/
│   ├── automation/
│   ├── docker/
│   ├── scripts/
│   └── infrastructure/
│
├── operations/
│   ├── server/
│   ├── networking/
│   ├── monitoring/
│   └── hardening/
│
├── project-management/
│   ├── roadmap/
│   ├── milestones/
│   ├── changelog/
│   └── documentation/
│
└── assets/
    ├── images/
    ├── screenshots/
    └── branding/
```

---

# Roadmap

## Phase 1 – Foundation

* Repository design
* Documentation standards
* Infrastructure planning
* Network architecture

## Phase 2 – Core Infrastructure

* Ubuntu Server
* Docker platform
* Self-hosted services
* Monitoring stack

## Phase 3 – Enterprise Environment

* Windows Server
* Active Directory
* Windows clients
* Centralized logging

## Phase 4 – Security Operations

* SIEM
* Detection Engineering
* Dashboards
* Threat Hunting

## Phase 5 – Incident Response

* Digital Forensics
* Malware Analysis
* Incident Response Playbooks
* Security Automation

## Phase 6 – Expansion

* Advanced integrations
* Infrastructure optimization
* Portfolio enhancements
* Continuous improvement

---

# Documentation Philosophy

Every implementation should answer four questions:

* **Why** was this technology selected?
* **How** was it implemented?
* **What** challenges were encountered?
* **What** improvements are planned?

The goal is to document the engineering process as thoroughly as the finished solution so that others can understand both the technical implementation and the reasoning behind each decision.

---

# Project Status

🚧 **Actively Under Development**

This repository is continuously evolving as new technologies, capabilities, documentation, and improvements are added.

---

# License

Released under the MIT License.

---

# About the Author

I'm building this Cyber Operations Center to deepen my practical cybersecurity skills through hands-on engineering, continuous learning, and detailed technical documentation.

My objective is to create an enterprise-inspired environment that demonstrates not only technical knowledge, but also the ability to design, operate, document, secure, troubleshoot, and continuously improve complex systems over time.

This repository represents that ongoing journey.
