# ADR-011: Use Fedora Workstation for the replacement workstation

- **Status:** Superseded by [ADR-012](ADR-012-linux-mint-cinnamon-primary-workstation.md)
- **Date:** 2026-08-13
- **Owner:** COC Program Owner
- **Supersedes:** [ADR-010](ADR-010-defer-win10-encryption-to-replacement.md)
- **Related phase(s):** Phase 8 and Phase 8.5
- **Related asset(s):** COC-WS-01 and its replacement

## Context

ADR-010 assumed that the legacy Windows 10 workstation would be replaced by Windows 11 Pro. The platform decision changed before Phase 8.5 implementation. The replacement will instead run Fedora Workstation.

The clean, encrypted, restore-tested Phase 8 migration source remains valid, but operating-system controls, application compatibility, telemetry, encryption, and restoration procedures must now be designed for a cross-platform migration.

## Decision

Install the current supported Fedora Workstation release from verified Fedora media on the replacement workstation.

Require:

- UEFI Secure Boot where compatible with the selected hardware and required signed drivers;
- installer-managed LUKS2-backed encryption for system and user data;
- SELinux in Enforcing mode;
- firewalld active with no unnecessary inbound services;
- automatic screen locking and a strong local credential;
- prompt Fedora security updates;
- a supported Wazuh Linux agent with file-integrity, inventory, configuration, and log visibility;
- selective restoration of reviewed user data rather than restoration of the Windows profile or applications;
- explicit disposition of every required Windows application; and
- revocation, sanitization, and retirement of the legacy workstation only after Fedora acceptance testing.

## Alternatives Considered

Proceed with Windows 11 Pro; install another Linux distribution; dual boot Windows and Fedora; run Windows as the primary platform with Fedora virtualized; or use Fedora as the primary workstation and virtualize only approved Windows-only workloads.

## Rationale

Fedora provides a current Linux workstation, strong default mandatory access controls through SELinux, native firewalld integration, signed Secure Boot support, modern package management, and a direct path for Linux engineering skills. It also reduces dependence on an unsupported Windows 10 platform.

A clean Fedora installation is safer and more maintainable than transplanting Windows state. Limited virtualization remains available for justified Windows-only workloads without making Windows the primary endpoint.

## Security Implications

Cross-platform migration can expose secrets, unsafe downloads, incompatible applications, and permission mistakes if the Windows profile is restored wholesale. Restore only approved data categories, rescan restored content, reinstall applications from trusted Fedora repositories or verified publishers, and rotate credentials or SSH keys when practical.

LUKS2 protects data at rest after shutdown but does not replace strong session locking, patching, Secure Boot, or endpoint telemetry. Recovery material must remain outside the public repository and be restore-tested.

## Consequences

ADR-010 is superseded. Phase 8.5 documentation must use Fedora controls rather than BitLocker, Defender, Windows Firewall, or Sysmon. Windows executables and configuration stores are not migration artifacts. Windows-only applications require a documented replacement, isolated virtual machine, narrowly approved compatibility layer, or retirement decision.

## Validation

Validate the installation-media signature and checksum, UEFI Secure Boot state, encrypted block-device layout, SELinux Enforcing state, firewalld service and zones, update state, Wazuh connectivity and event receipt, selective restore integrity, application acceptance, hardware-key authentication, and legacy-device sanitization.

## Review Date or Trigger

Review after a Fedora edition change, major hardware incompatibility, Secure Boot exception, encryption recovery failure, required Windows-only application gap, Wazuh incompatibility, or decision to introduce dual boot.
