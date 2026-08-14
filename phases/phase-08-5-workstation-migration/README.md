# Phase 8.5 — Fedora Workstation Migration

> **Status:** Planned  
> **Predecessor:** [Phase 8 — Endpoint Engineering](../phase-08-endpoint-engineering/README.md)  
> **Successor:** Phase 9 — Nextcloud Platform  
> **Decision:** [ADR-011 — Use Fedora Workstation](../../docs/decisions/ADR-011-use-fedora-for-primary-workstation.md)

## Purpose

Replace the temporary Windows 10 workstation with a clean, encrypted, monitored Fedora Workstation without weakening the restore-tested state established in Phase 8.

This is a cross-platform migration. Fedora will be installed cleanly. Approved user data will be restored selectively; Windows applications, profiles, services, registry state, caches, and executables will not be transplanted.

## Authoritative references

- [Fedora Workstation](https://fedoraproject.org/workstation/)
- [Fedora Workstation download and verification](https://fedoraproject.org/workstation/download/)
- [Fedora Secure Boot](https://fedoraproject.org/wiki/Secureboot)
- [Fedora disk-encryption guide](https://fedoraproject.org/wiki/Disk_Encryption_User_Guide)
- [Wazuh Linux-agent deployment](https://documentation.wazuh.com/current/installation-guide/wazuh-agent/wazuh-agent-package-linux.html)
- [Wazuh package list](https://documentation.wazuh.com/current/installation-guide/packages-list.html)

Use the current official instructions at implementation time. Commands and release identifiers are intentionally not frozen in this planning record.

## Entry gate

- Phase 8 completion approved
- Approved clean Restic migration snapshot available
- Representative restore test passed
- Historical snapshots containing unsafe downloads warning-tagged
- [Application compatibility inventory](APPLICATION-COMPATIBILITY-INVENTORY.md) completed for every required workflow
- [Risk assessment](RISK-ASSESSMENT.md) reviewed
- Fedora hardware compatibility checked
- Required data categories and secret-handling decisions documented privately
- Installation destination disk positively identified
- Fedora recovery and rollback plan approved

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

1. Obtain the current supported Fedora Workstation image from the Fedora Project.
2. Obtain Fedora signing material and the signed checksum through official paths.
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

### 4. Establish the Fedora baseline

- Apply firmware, Fedora, and application updates.
- Verify Secure Boot state.
- Verify the LUKS2 encrypted backing devices for root and user data.
- Verify SELinux is Enforcing; resolve policy or labeling issues rather than disabling it.
- Verify firewalld is enabled and active.
- Review the active firewall zone, allowed services, and listening sockets.
- Configure screen locking and password-on-resume.
- Remove or disable unnecessary services.
- Prefer Fedora packages, reviewed Flatpaks, or verified upstream publishers.
- Keep development dependencies isolated by project or container where practical.

### 5. Restore selectively

Restore only reviewed categories such as documents, media, repositories, approved project data, and specifically accepted virtual-machine disks.

Do not bulk-restore:

- Windows or Program Files directories;
- the complete Windows user profile;
- AppData, registry hives, scheduled tasks, or services;
- browser caches or complete browser profiles;
- installers, key generators, activators, or unreviewed Downloads;
- Windows executables as Fedora applications; or
- secrets whose ownership or provenance is uncertain.

Scan restored data, compare representative files with the approved source, correct ownership and permissions, and rotate SSH keys or other durable credentials where practical.

### 6. Rebuild applications

Use the [application compatibility inventory](APPLICATION-COMPATIBILITY-INVENTORY.md). Prefer native Fedora packages, reviewed Flatpaks, web applications, or Linux replacements. Use an isolated Windows virtual machine only for a justified Windows-only workload. Treat Wine or Bottles as a narrow tested exception.

### 7. Reconnect security services

- Install a supported Wazuh Linux agent compatible with the manager.
- Use a permanent Fedora asset identity.
- Validate service startup, encrypted connectivity, file-integrity events, system inventory, configuration assessment, vulnerability visibility, and relevant system logs.
- Close temporary enrollment access after registration.
- Configure WireGuard through NetworkManager only if the fixed workstation has an approved need.
- Rebuild hardware-key enrollments deliberately and test recovery paths.

### 8. Establish Fedora backup and recovery

Create a Fedora-native backup job for approved user and configuration data. Complete one successful backup and one isolated restore before Windows retirement. Preserve the Phase 8 Windows source until Fedora acceptance is complete.

### 9. Accept and retire

Complete the [migration validation checklist](MIGRATION-VALIDATION-CHECKLIST.md). Revoke the temporary Windows Wazuh identity and obsolete device registrations. Sanitize legacy storage only after the user accepts Fedora, data and applications pass validation, Wazuh is healthy, and Fedora backup restoration succeeds.

## Stop conditions

Stop and investigate if:

- Fedora media signature or checksum validation fails;
- the destination disk is uncertain;
- required hardware cannot operate securely;
- encryption recovery is untested;
- SELinux would need to be disabled;
- unexpected inbound services remain exposed;
- malware is detected;
- restored data fails integrity checks;
- a required workflow has no accepted disposition;
- Wazuh telemetry is absent;
- the Fedora backup cannot be restored; or
- retirement criteria are incomplete.

## Completion criteria

- Current supported Fedora Workstation installed from verified media
- UEFI Secure Boot validated or a narrowly documented hardware exception approved
- LUKS2-backed encryption and recovery validated
- SELinux Enforcing
- firewalld active with reviewed zones and services
- Current firmware, Fedora, and applications
- Selective data restoration scanned and sampled successfully
- Required applications and workflows accepted
- Permanent Wazuh Linux identity and telemetry active
- Hardware-key and recovery paths tested
- Fedora backup and isolated restore passed
- Temporary Windows registrations revoked
- Legacy storage sanitized and disposition recorded
- Phase 8.5 completion report published
