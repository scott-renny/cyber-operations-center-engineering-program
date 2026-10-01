# Phase 10 — Identity Services

> **Status:** 🟨 In Progress  
> **Platform:** Windows Server 2025 Evaluation, Windows 11 Enterprise Evaluation, Kali Linux (next)  
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

### Windows 11 domain client and delegated administration

- Built `WIN11-CLIENT` with Windows 11 Enterprise Evaluation and joined it to `corp.lab.test`.
- Placed the computer in the protected workstation OU and validated Kerberos/DC discovery and the domain secure channel.
- Verified a normal employee account receives no local administrative privilege.
- Linked a workstation Local Administrators GPO that applies `DL-Workstation-LocalAdmins` to the built-in Administrators group.
- Proved the complete AGDLP path: `adm-arivera → GG-Workstation-Admins → DL-Workstation-LocalAdmins → local Administrators`.
- Preserved a separate local recovery administrator.

### Machine-account quota hardening

During the client join, a normal user credential unexpectedly succeeded. Investigation found the default `ms-DS-MachineAccountQuota` value was 10.

- Reduced `ms-DS-MachineAccountQuota` from 10 to 0.
- Delegated workstation computer-object administration explicitly to `GG-Workstation-Admins` on the workstation OU.
- Verified the OU ACL for computer-object creation/deletion, password reset/change, and required read/write properties.

This converted an implicit broad join capability into an intentional role-based administrative path.

### Privileged logon restrictions

Linked a dedicated GPO to the workstation OU that denies `GG-Tier0-Admins`:

- local interactive logon; and
- Remote Desktop Services logon.

The restriction was validated by denying `da-arivera` at WIN11-CLIENT while `adm-arivera` continued to sign in and administer the workstation.

### Advanced audit policy

Created and linked a dedicated Windows Audit Policy GPO to workstations and domain controllers. The baseline captures authentication, Kerberos, lockout, account/group management, process creation, audit/authentication policy changes, and key system integrity/state events. The advanced subcategory policy is forced to override legacy category settings.

The resulting telemetry supports later analysis of events such as 4624/4625, 4688, 4768, and 4769.

### Patching, DNS remediation, and pre-attack baseline

DC01 and WIN11-CLIENT were patched before adversary simulation. A persistent multihomed-DC DNS issue was then reproduced: the NAT IPv4 and IPv6 addresses were being published alongside the isolated lab address even though ordinary NAT-interface DNS registration was disabled.

The DNS Server listener was restricted to `10.10.10.10`, the service was restarted, and DC registration was deliberately forced with `nltest /dsregdns`. The unwanted NAT records did not return. WIN11-CLIENT was then validated to resolve DC01 only through `10.10.10.10`, with a healthy domain secure channel.

Powered-off VirtualBox restore points were captured:

- `DC01 - Pre-Attack Identity Baseline`
- `WIN11-CLIENT - Pre-Attack Identity Baseline`

This establishes the clean boundary between the build/harden work and the upcoming controlled attack/detection work.

## Validation state

At the end of the current work session:

- ADWS — Running
- DNS — Running
- KDC — Running
- Netlogon — Running
- NTDS — Running
- `dcdiag /test:Connectivity` — Passed
- PowerShell 7.6.6 — Verified

## Phase 10 risk controls

Phase 10 directly exercises existing program risks around excessive administrative privilege and intentionally vulnerable lab systems. The current controls are:

- daily, administrative, and Tier-0 identities are separated rather than using one broadly privileged account;
- Tier-0 authority is assigned through a dedicated role group, with the Tier-0 user placed in Protected Users and marked non-delegable;
- the deliberately vulnerable `svc_backup` identity is lab-only, is not a general privileged administrator, and exists specifically for controlled Kerberoasting detection work;
- attack traffic remains confined to the isolated VirtualBox lab network rather than being bridged to the household LAN;
- synthetic lab identities are used instead of real credentials or production data;
- password-spray exercises must remain below the configured lockout threshold and use documented stop conditions;
- offensive testing is not considered complete until telemetry, cleanup, and restored-state validation are recorded; and
- public documentation excludes passwords, hashes, secrets, recovery material, and sensitive infrastructure details.

These controls reduce the likelihood that the intentionally vulnerable identity path or privileged accounts become an uncontrolled risk while preserving the attack-and-defense learning objective.

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

1. Build/configure the Kali attacker VM on the isolated Phase 10 network.
2. Configure/validate Wazuh and Sysmon collection for relevant Windows Security and identity events.
3. Perform controlled password-spray, Kerberoasting, and credential-access exercises only inside the owned lab.
4. Validate detections and document incident-response cases for the attack exercises.
5. Deploy and use Greenbone/OpenVAS for vulnerability-management practice.
6. Remediate findings, re-scan, and record validation evidence.
7. Complete the Phase 10 acceptance checklist and completion record.

## Scope and safety

The offensive portion of this phase is limited to intentionally vulnerable systems and identities owned by the lab. The isolated internal VirtualBox network is used for attack traffic; vulnerable services are not bridged onto the home LAN.

No real credentials, passwords, hashes, recovery secrets, or sensitive infrastructure details are committed to this repository.
