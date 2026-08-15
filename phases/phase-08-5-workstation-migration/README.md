# Phase 8.5 — Linux Mint Cinnamon Workstation Migration

> **Status:** Planned  
> **Predecessor:** [Phase 8 — Endpoint Engineering](../phase-08-endpoint-engineering/README.md)  
> **Successor:** Phase 9 — Nextcloud Platform  
> **Decision:** [ADR-012 — Use Linux Mint Cinnamon](../../docs/decisions/ADR-012-linux-mint-cinnamon-primary-workstation.md)

## Purpose

Replace the temporary Windows 10 workstation with a clean, encrypted, monitored Linux Mint Cinnamon workstation without weakening the restore-tested state established in Phase 8.

This is a cross-platform migration. Linux Mint will be installed cleanly. Approved user data will be restored selectively; Windows applications, profiles, services, registry state, caches, and executables will not be transplanted.

## Authoritative references

- [Linux Mint](https://linuxmint.com/)
- [Linux Mint installation guide](https://linuxmint-installation-guide.readthedocs.io/)
- [Ubuntu Secure Boot](https://wiki.ubuntu.com/UEFI/SecureBoot)
- [Beginner workstation roadmap](../../docs/WORKSTATION-SETUP.md)
- [Wazuh Linux-agent deployment](https://documentation.wazuh.com/current/installation-guide/wazuh-agent/wazuh-agent-package-linux.html)
- [Wazuh package list](https://documentation.wazuh.com/current/installation-guide/packages-list.html)
- [Cerberus Operations Runbooks](https://github.com/scott-renny/project-cerberus-build/tree/main/docs/operations)

Use the current official instructions at implementation time. Commands and release identifiers are intentionally not frozen in this planning record.

## Entry gate

- Phase 8 completion approved
- Approved clean Restic migration snapshot available
- Representative restore test passed
- Historical snapshots containing unsafe downloads warning-tagged
- [Application compatibility inventory](APPLICATION-COMPATIBILITY-INVENTORY.md) completed for every required workflow
- [Risk assessment](RISK-ASSESSMENT.md) reviewed
- Linux Mint hardware compatibility checked
- Required data categories and secret-handling decisions documented privately
- Installation destination disk positively identified
- Linux Mint recovery and rollback plan approved
- Cerberus update, backup/rebuild, Wazuh, isolation, graphics, and security-key runbooks reviewed

## Planned sequence

### 1. Inventory and preserve

1. Complete the application compatibility inventory.
2. Classify migration data: restore, rebuild, rotate, archive, or discard.
3. Create a final Windows staging copy after any last approved changes.
4. Run Defender and server-side ClamAV validation.
5. Create a new encrypted Restic snapshot.
6. Verify absence of known unsafe filenames and restore a representative file.
7. Record the final approved migration source privately.

### 2. Verify installation media

1. Obtain the current supported Linux Mint Cinnamon image from the Linux Mint project.
2. Obtain the published checksum through an independent official path and verify the image.
3. Verify the checksum signature.
4. Verify the image SHA-256 checksum.
5. Create and boot-test installation media.

### 3. Install securely

1. Boot the installer in UEFI mode.
2. Confirm the destination disk before any destructive action.
3. Retain Secure Boot where required hardware is compatible.
4. Select installer-managed LUKS2-backed encryption for system and user data.
5. Use a strong, unique encryption passphrase and store recovery material privately.
6. Create a standard daily user and use deliberate administrative elevation.
7. Do not enable automatic login.

The EFI system partition and boot components may not be LUKS-encrypted. Secure Boot provides integrity protection for the signed boot chain; post-install validation must confirm the actual storage layout rather than claiming every disk sector is encrypted.

### 4. Establish the Linux Mint baseline

- Apply firmware, Linux Mint, and application updates.
- Verify Secure Boot state.
- Verify the LUKS2 encrypted backing devices for root and user data.
- Verify AppArmor is active; resolve profile issues rather than disabling protection.
- Verify UFW is enabled with no unnecessary inbound services.
- Review the active firewall zone, allowed services, and listening sockets.
- Configure screen locking and password-on-resume.
- Remove or disable unnecessary services.
- Prefer Mint/Ubuntu `apt` packages, reviewed Flatpaks, or verified upstream publishers.
- Keep development dependencies isolated by project or container where practical.

### 5. Restore selectively

Restore only reviewed categories such as documents, media, repositories, approved project data, and specifically accepted virtual-machine disks.

Do not bulk-restore:

- Windows or Program Files directories;
- the complete Windows user profile;
- AppData, registry hives, scheduled tasks, or services;
- browser caches or complete browser profiles;
- installers, key generators, activators, or unreviewed Downloads;
- Windows executables as Linux Mint applications; or
- secrets whose ownership or provenance is uncertain.

Scan restored data, compare representative files with the approved source, correct ownership and permissions, and rotate SSH keys or other durable credentials where practical.

### 6. Rebuild applications

Use the [application compatibility inventory](APPLICATION-COMPATIBILITY-INVENTORY.md). Prefer Mint/Ubuntu packages, reviewed Flatpaks, web applications, or Linux replacements. Use an isolated Windows virtual machine only for a justified Windows-only workload. Treat Wine or Bottles as a narrow tested exception.

### 7. Reconnect security services

- Install a supported Wazuh Linux agent compatible with the manager.
- Use a permanent Linux Mint asset identity.
- Validate service startup, encrypted connectivity, file-integrity events, system inventory, configuration assessment, vulnerability visibility, and relevant system logs.
- Close temporary enrollment access after registration.
- Configure WireGuard through NetworkManager only if the fixed workstation has an approved need.
- Rebuild hardware-key enrollments deliberately and test recovery paths.

### 8. Establish Linux Mint backup and recovery

Create a Linux-native backup job for approved user and configuration data. Complete one successful backup and one isolated restore before Windows retirement. Preserve the Phase 8 Windows source until Mint acceptance is complete.

### 9. Accept and retire

Complete the [migration validation checklist](MIGRATION-VALIDATION-CHECKLIST.md). Revoke the temporary Windows Wazuh identity and obsolete device registrations. Sanitize legacy storage only after the user accepts Mint, data and applications pass validation, Wazuh is healthy, and Mint backup restoration succeeds.

## Stop conditions

Stop and investigate if:

- Linux Mint installation media checksum validation fails;
- the destination disk is uncertain;
- required hardware cannot operate securely;
- encryption recovery is untested;
- AppArmor would need to be disabled;
- unexpected inbound services remain exposed;
- malware is detected;
- restored data fails integrity checks;
- a required workflow has no accepted disposition;
- Wazuh telemetry is absent;
- the Linux Mint backup cannot be restored; or
- retirement criteria are incomplete.

## Completion criteria

- Current supported Linux Mint Cinnamon installed from verified media
- UEFI Secure Boot validated or a narrowly documented hardware exception approved
- LUKS2-backed encryption and recovery validated
- AppArmor active
- UFW active with reviewed rules
- Current firmware, Linux Mint, and applications
- Selective data restoration scanned and sampled successfully
- Required applications and workflows accepted
- Permanent Wazuh Linux identity and telemetry active
- Hardware-key and recovery paths tested
- Linux Mint backup and isolated restore passed
- Temporary Windows registrations revoked
- Legacy storage sanitized and disposition recorded
- Phase 8.5 completion report published
