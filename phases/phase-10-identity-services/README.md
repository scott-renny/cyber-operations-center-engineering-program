# Phase 10 — Identity Services

> **Status:** 🟨 In Progress  
> **Platform:** Windows Server 2025 Evaluation, Windows 11 client (planned), Kali Linux (planned)  
> **Lab domain:** `corp.lab.test`  
> **Primary DC:** `DC01`

## Objective

Build, administer, attack, monitor, investigate, and harden a modern Windows enterprise identity environment. The phase is designed to demonstrate both Windows/Active Directory administration and defensive security skills while keeping all offensive activity confined to an isolated, owned lab.

## Current architecture

The identity lab is hosted in VirtualBox on the Windows 11 laptop so it can remain portable. The lab uses an isolated internal network for Active Directory and attack traffic plus a separate NAT adapter for controlled outbound access. The domain controller is Windows Server 2025 Standard Evaluation with AD DS and DNS.

The forest and domain are:

- DNS domain: `corp.lab.test`
- NetBIOS domain: `CORP`
- Domain controller: `DC01.corp.lab.test`
- Domain functional level: Windows Server 2025
- Forest functional level: Windows Server 2025

## Completed work

### Domain controller foundation

- Installed Windows Server 2025 Evaluation with Desktop Experience.
- Promoted `DC01` into a new `corp.lab.test` forest.
- Repaired AD Web Services after the initial promotion freeze.
- Rebuilt the AD-integrated `corp.lab.test` and `_msdcs.corp.lab.test` DNS zones after promotion left them incomplete.
- Removed stale NAT DNS registration and verified that the DC resolves through the lab interface.
- Verified SYSVOL and NETLOGON shares, domain-controller discovery, Kerberos/DNS locator records, and `dcdiag /test:Connectivity`.
- Increased the VM to 6 GB RAM and 4 vCPU after stability problems at the original allocation.
- Installed PowerShell 7.6.6 alongside Windows PowerShell 5.1.

### Organizational design

Created protected OUs for:

- privileged accounts
- standard admin accounts
- users
- workstations
- servers
- service accounts
- security groups

Created Global Security role groups for employees, IT admins, SOC analysts, server admins, workstation admins, and Tier-0 admins.

Created Domain Local permission groups for server and workstation local administration and nested the Global role groups into them using an AGDLP-style model.

### User and privilege separation

Created representative user identities for normal employees, SOC, and IT administration. The IT identity model intentionally separates everyday, administrative, and Tier-0 use:

```text
arivera
└─ everyday IT account

adm-arivera
├─ GG-IT-Admins
├─ GG-Server-Admins
└─ GG-Workstation-Admins

da-arivera
├─ GG-Tier0-Admins
├─ Protected Users
├─ AccountNotDelegated = True
└─ Domain Admin authority inherited through GG-Tier0-Admins
```

`GG-Tier0-Admins` is nested into the built-in `Domain Admins` group so the privileged role is assigned to a group rather than directly to the user.

### Password and lockout baseline

The default domain policy was strengthened to:

- minimum password length: 15 characters
- complexity: enabled
- password history: 24
- minimum password age: 1 day
- maximum password age: 90 days
- account lockout threshold: 10 failed attempts
- lockout duration: 15 minutes
- lockout observation window: 15 minutes

This provides a defined defensive baseline before the controlled password-spray exercise.

### Service identities

A KDS root key was created and validated for Group Managed Service Accounts.

Secure reference identity:

- `gmsa-backup$`
- AD-managed password
- automatic password rotation
- managed password retrieval currently restricted to the domain controller until a dedicated service host exists

Deliberately vulnerable lab identity:

- `svc_backup`
- traditional static service account
- `PasswordNeverExpires = True`
- SPN: `MSSQLSvc/legacy-backup.corp.lab.test:1433`
- clearly labelled as a lab-only identity for the later Kerberoasting exercise

The vulnerable account is intentionally separate from the secure baseline and is not used as a general privileged administrator.

## Validation state

At the end of the current work session:

- ADWS — Running
- DNS — Running
- KDC — Running
- Netlogon — Running
- NTDS — Running
- `dcdiag /test:Connectivity` — Passed
- PowerShell 7.6.6 — Verified

## Security principles demonstrated

- least privilege
- separation of duties
- separate daily/admin/Tier-0 identities
- role-based group assignment
- AGDLP-style permission nesting
- protected privileged identities
- non-delegable Tier-0 credentials
- managed service identities
- deliberately isolated vulnerable identities for attack simulation
- password and lockout policy hardening
- secure DNS/AD service validation

## Remaining Phase 10 work

1. Apply GPO-based privileged-logon boundaries and additional domain/DC hardening.
2. Build the Windows 11 domain client and join it to `corp.lab.test`.
3. Build the Kali attacker VM on the isolated Phase 10 network.
4. Configure Wazuh/Sysmon collection for relevant Windows Security and identity events.
5. Perform controlled password-spray, Kerberoasting, and credential-access exercises only inside the owned lab.
6. Validate detections and document incident-response cases for the attack exercises.
7. Deploy and use Greenbone/OpenVAS for vulnerability-management practice.
8. Remediate findings, re-scan, and record validation evidence.
9. Complete the Phase 10 acceptance checklist and completion record.

## Scope and safety

The offensive portion of this phase is limited to intentionally vulnerable systems and identities owned by the lab. The isolated internal VirtualBox network is used for attack traffic; vulnerable services are not bridged onto the home LAN.

No real credentials, passwords, hashes, recovery secrets, or sensitive infrastructure details are committed to this repository.
