# Device Inventory Standard

## Purpose

This document defines the authoritative schema that Phase 20 NetBox population and all interim inventory records must follow.

## Required fields

| Field | Requirement |
|---|---|
| Asset ID | Stable, non-secret unique identifier |
| Device name | Approved hostname or sanitized display name |
| Device class | Server, workstation, laptop, mobile, tablet, network, IoT, lab target, removable media |
| Role | Operational purpose |
| Owner/custodian | Accountable person or household role |
| Criticality | Critical, high, moderate, low |
| Manufacturer/model | Hardware identification |
| Serial/asset tag | Restricted field; never public |
| CPU/RAM/storage | Capacity and platform planning |
| Operating system | Edition, version, build, support status |
| Firmware/BIOS | Version and last review date |
| Network profile | Wired, wireless, roaming, isolated, management-only |
| Trust zone | Management, trusted internal, user, guest, IoT, lab, untrusted, external |
| IP allocation | Static, DHCP reservation, dynamic, not applicable |
| Addresses | Restricted IP/MAC/VPN identifiers |
| Management platform | NetBox, endpoint manager, MDM, manual, unmanaged exception |
| Monitoring agents | Wazuh, Sysmon, Velociraptor, FleetDM, Prometheus exporter, other |
| Backup status | Protected, partial, not required, exception |
| Encryption status | Full-disk, volume, unavailable, exception |
| MFA/security key | Required status without storing secret material |
| Hardening baseline | Baseline name/version and last validation |
| Patch/compliance status | Compliant, overdue, exception, isolated |
| Data classification | Highest data class normally processed |
| Recovery method | Rebuild, image, restore, vendor reset, none |
| Lifecycle status | Planned, active, maintenance, test-only, quarantined, retired, disposed |
| Purchase/warranty | Restricted operational metadata |
| Planned replacement date | Lifecycle forecast |
| Retirement approval | Date and approver |
| Sanitization method/status | Not started, verified, failed/rework |
| Final disposition | Reuse, sale, donation, recycle, destruction, retained archive |
| Evidence link | Sanitization/disposition record location |
| Last reviewed | Date and reviewer |

## Lifecycle rules

- Inventory entry is created before or during onboarding.
- No device is considered trusted solely because it is personally owned.
- Roaming endpoints use secure remote access and are evaluated by identity, authorization, device state, and exposure—not location alone.
- Unsupported devices are isolated, upgraded, repurposed as explicitly vulnerable lab targets, or retired under a documented exception.
- A retired device is not removed from inventory until data sanitization and final disposition are verified.

## Minimum onboarding evidence

- hardware and OS confirmed;
- owner and role assigned;
- trust zone and network profile approved;
- encryption and backup decisions recorded;
- monitoring and management agents validated;
- hardening baseline applied or exception opened;
- recovery method tested or documented.

## Public portfolio representation

Public inventories use generalized names and omit serials, MACs, live IPs, exact locations, warranty identifiers, family-member mappings, and recovery details.
