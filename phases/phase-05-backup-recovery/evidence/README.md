# Phase 5 Validation Evidence

> **Status:** Complete  
> **Evidence classification:** Public, sanitized  
> **Validation period:** 2026-07-31 through 2026-08-05

## Publication decision

This file records outcome-level evidence only. It excludes live addresses, filesystem UUIDs, disk serials, repository identifiers, credentials, password material, private keys, certificates, raw backup content, complete firewall exports, and unredacted screenshots.

## Validation matrix

| Control | Sanitized observation | Result |
|---|---|---|
| Backup target | External disk distinguished from the active system disk and health-tested | Pass |
| Destructive safety | Target unmounted, verified, and explicitly authorized before formatting | Pass |
| Persistent filesystem | New filesystem mounted persistently with expected capacity | Pass |
| Mount safety | Automation verified the mounted filesystem before writing | Pass |
| Rsync failure | Protected unreadable material produced a reported failure | Pass |
| Least privilege | Protected credentials kept restrictive ownership and were explicitly excluded | Pass |
| Rsync integrity | Representative source and mirror files matched byte for byte | Pass |
| Server Restic | Snapshots, retention, pruning, and checks passed | Pass |
| Server restore | Representative files restored with matching content and permissions | Pass |
| Samba authentication | Authenticated upload, list, download, comparison, and deletion passed | Pass |
| Anonymous Samba | Access denied | Pass |
| Firewall scope | Samba restricted to trusted LAN and VPN sources | Pass |
| Workstation scheduling | Core, Downloads, and powered-off VirtualBox tasks returned result 0 | Pass |
| Workstation direct restore | Source, SMB mirror, and restore SHA-256 hashes matched | Pass |
| Workstation encrypted snapshot | Approximately 76 GiB completed in about 1 hour 6 minutes | Pass |
| Workstation encrypted restore | Representative file matched the SMB mirror byte for byte | Pass |
| Laptop LAN | Backup completed with acceptable Robocopy code 3 | Pass |
| Laptop scheduled task | Nightly task manually completed with result 0 | Pass |
| Laptop VPN fallback | WireGuard backup completed with acceptable Robocopy code 1 | Pass |
| Laptop disconnected behavior | Logged skip and exit code 0 when both SMB paths were unavailable | Pass |
| Laptop restore | 320 files, approximately 5.82 MB, restored in 37 seconds with zero failures | Pass |
| Wazuh failure rule | Expected level-7 alert generated | Pass |
| Wazuh success rule | Expected level-5 alert generated | Pass |
| Operational monitoring | Server, workstation, laptop, and encrypted-snapshot events collected | Pass |

## Server evidence

The external target was identified and health-tested before destructive work. The new filesystem mounted persistently, and automation rejected an unverified mount.

The first rsync execution proved the failure path when protected credential material could not be read. Permissions were preserved, the exclusion was documented, and the corrected run succeeded. Representative files matched.

Encrypted backup, retention, pruning, and repository checking succeeded. A controlled restore recovered representative content with matching data and restrictive permissions.

## Windows workstation evidence

The workstation used authenticated UNC access and incremental Robocopy. Core, Downloads, and powered-off VirtualBox jobs were separated, and each Task Scheduler job returned result 0.

A representative source, SMB copy, and direct restore had identical hashes. The server then encrypted and versioned the mirror. Its first snapshot processed approximately 76 GiB in about 1 hour 6 minutes. A representative encrypted restore matched byte for byte.

The script included an overlap lock, a VirtualBox-running guard, locale-independent timestamps, and correct Robocopy exit handling.

## Windows laptop evidence

The laptop ran under the approved signed-in user so Credential Manager could protect the Samba password.

Validated scenarios:

- direct LAN success with acceptable Robocopy code 3;
- nightly Task Scheduler execution with result 0;
- WireGuard fallback success with acceptable Robocopy code 1 while LAN SMB was blocked;
- no-connection handling with a logged skip and exit code 0; and
- restoration of 320 files totaling approximately 5.82 MB in 37 seconds with zero failures and acceptable code 1.

Approved user files, cloud-synchronized content, SSH material, roaming configuration, and portable configuration were covered. Live local application state was excluded because caches, databases, and registry-backed state require VSS, application-aware export, or imaging.

Temporary firewall rules used to isolate LAN, VPN, and disconnected paths were removed immediately after testing.

## Monitoring evidence

Named stable logs were used instead of accumulating wildcard logs. Custom Wazuh rules matched backup program names and explicit status markers.

Rule testing selected the expected success and failure rules. End-to-end events from server jobs, Windows scheduling, and encrypted snapshots produced alerts. Rotated archives retained evidence of the first large encrypted workstation snapshot.

## Recovery objectives

- **RPO:** up to 24 hours
- **Laptop sample RTO:** 37 seconds for 320 files totaling approximately 5.82 MB
- **Small server and workstation restores:** under one minute
- **Full-device RTO:** dependent on size, throughput, and destination performance

## Accepted limitations

- Direct mirrors are not encrypted at rest.
- Protected root- and container-owned exclusions reduce unprivileged rsync coverage.
- Live databases may need quiescing or application-aware export.
- Laptop local application state requires VSS or imaging.
- Bare-metal recovery was outside this phase.
- Recovery secrets must remain available outside the protected server.

## Evidence integrity

Evidence was transcribed from direct command output and administrative interfaces. Temporary restore locations and test firewall rules were removed after validation. The public record preserves outcomes, failure behavior, recovery results, and sanitization decisions without publishing sensitive operational data.
