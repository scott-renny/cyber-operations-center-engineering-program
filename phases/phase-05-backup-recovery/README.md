# Phase 5 — Backup and Recovery

**Status:** In Progress  
**Server-side validation date:** 2026-07-31  
**Windows 10 validation date:** 2026-08-04  
**Budget:** $0  
**Asset ID:** `coc-srv-01`  
**Friendly name:** Atlas

## Goal

Establish a monitored local backup and recovery architecture for Atlas, then extend that architecture to the Windows desktop and laptop without representing untested endpoint or VPN behavior as complete.

## Current scope

Completed and validated now:

- destructive-target verification and clean ext4 rebuild of the preserved external backup disk;
- UUID-based persistent mounting with a mount-point safety gate;
- unprivileged rsync mirrors for approved server and Docker data;
- encrypted, deduplicated Restic snapshots with retention and integrity checks;
- an authenticated Samba backup share restricted to trusted LAN and VPN sources;
- real Restic restore and byte-comparison testing;
- a scheduled Windows 10 SMB mirror split into core, Downloads, and powered-off VirtualBox modes;
- encrypted and deduplicated server-side snapshots of the Windows mirror with a successful restore; and
- Wazuh collection and alerting for Linux, Windows, and encrypted-network backup logs.

Still in progress:

- Windows 11 laptop LAN automation;
- laptop no-connection behavior;
- laptop WireGuard fallback after the required profile is available; and
- Windows 11 laptop restore testing.

## Architecture

```text
Approved server data
        │
        ├──────── rsync mirror ─────────────┐
        │                                   │
        └──────── encrypted Restic ─────────┤
                                            ▼
                                  External backup disk
                                            │
                         ┌──────────────────┴──────────────────┐
                         ▼                                     ▼
                Authenticated SMB share                 Stable job logs
                         │                                     │
       Windows SMB mirrors and encrypted snapshots             Wazuh
                                                               │
                                                     success/failure alerts
```

The public record intentionally omits live addresses, filesystem UUIDs, disk serial numbers, credentials, repository identifiers, private paths containing secrets, and raw screenshots.

## Storage preparation

The preserved external backup disk was identified by model, capacity, transport, filesystem label, and SMART data before destructive work began. The system disk was separately identified by its active root, boot, and EFI mounts.

Validation included:

- exact byte-capacity inspection;
- partition-table inspection;
- USB bridge identification;
- SMART identity and health review;
- a successful SMART short self-test;
- confirmation that the target partition was unmounted; and
- explicit authorization before formatting.

The disk was reformatted as ext4, assigned a new filesystem UUID, mounted persistently through `/etc/fstab`, and verified with `findmnt` and `df`. The backup mount is not world-accessible.

The original planning note overstated the disk capacity. Device-level evidence established the actual installed capacity, and the private operational record was corrected.

## Rsync mirror

The rsync job runs as an unprivileged account and refuses to write unless the expected filesystem UUID is mounted at the backup path. This prevents a missing external disk from redirecting backup data onto the server's system disk.

Protected categories include:

- the approved administrator home directory;
- Docker stack definitions and persistent application data; and
- Dockge application data.

Known root- or container-owned locations are explicitly excluded. The initial run correctly returned a failure when it encountered a root-protected Wazuh credential archive. The archive contains private keys and passwords, so its restrictive ownership was preserved and the least-privilege exclusion was documented rather than weakening permissions or running the entire backup as root.

The corrected run completed successfully. Representative files from each protected category matched their backup copies byte for byte.

### Rsync limitation

The rsync mirror is not encrypted at rest. It provides a directly accessible local recovery copy, while sensitive home data is additionally protected by Restic encryption.

Docker data is copied while containers remain active. Live database and write-ahead-log files may not constitute an application-consistent recovery point. Application-aware exports or controlled quiescing remain a future improvement.

## Restic snapshots

Restic provides encrypted, compressed, deduplicated, versioned snapshots for the approved server home data and the Windows network-backup mirror.

Controls include:

- a password file restricted to the exact automation account;
- a separately retained recovery password requirement;
- repository-path and mounted-filesystem verification;
- nightly snapshot creation;
- 7 daily, 4 weekly, and 3 monthly recovery periods;
- retention and pruning after backup completion;
- a weekly repository integrity check; and
- stable Wazuh-compatible logging.

Backup, retention, and integrity-check modes were tested manually under the same unprivileged account used by scheduling. The integrity check reported no repository errors.

The first encrypted snapshot of the Windows mirror processed approximately 76 GiB in 1 hour 6 minutes. A representative file was restored from that repository and matched the SMB mirror byte for byte.

## Restore validation

A real restore of the latest snapshot completed successfully into a separate recovery directory.

Validation confirmed:

- successful restore exit status;
- restored files and directories;
- preserved ownership and restrictive permissions;
- byte-for-byte matches for representative documentation and automation scripts; and
- continued exclusion of the protected Wazuh credential archive.

Recovery objectives at the current validated scale:

- **RPO:** up to 24 hours from nightly scheduling.
- **Demonstrated RTO:** under one minute for the small validation dataset.
- **Full-volume RTO:** not yet validated and dependent on data volume, disk throughput, and the recovery destination.

A successful backup command is not accepted as proof of recoverability. Restore testing remains part of ongoing operations.

## Samba network share

The Samba share uses a dedicated non-interactive account and a restricted backup group.

Controls include:

- authenticated access only;
- guest access disabled for the backup share;
- forced file ownership;
- controlled file and directory creation modes;
- share browsing disabled;
- symbolic-link following disabled;
- a default-deny host firewall; and
- Samba access limited to the trusted LAN and WireGuard subnets.

An authenticated upload, listing, download, byte comparison, and deletion test completed successfully. Anonymous access returned an access-denied result.

The global `map to guest = Bad User` setting remains a documented compatibility tradeoff. Risk to the backup share is constrained by `guest ok = no`, an explicit valid-user requirement, and source-restricted firewall rules.

## Wazuh monitoring

Wazuh monitors four named, stable backup log files covering the rsync mirror, server-home Restic repository, Windows backup summaries, and encrypted Windows-mirror repository. Wildcard paths are intentionally prohibited for accumulating backup logs because tracking a growing collection of timestamped files can saturate the event queue.

Custom rules provide:

- a level-7 backup-failure alert; and
- a level-5 backup-success alert.

The original draft proposed process-monitoring rule 530 as the parent. Testing showed that rule 530 only matches command-monitor output beginning with `ossec: output:` and cannot parent ordinary backup syslog events. The implemented rules instead match the pre-decoded backup program names and escaped status markers.

Both rules passed `wazuh-logtest`. End-to-end events written to the named files were collected and displayed in the Wazuh dashboard at the expected levels.

## Scheduling

The server schedule uses non-overlapping jobs:

1. rsync mirror;
2. Restic snapshot;
3. Restic retention and pruning; and
4. weekly Restic integrity checking.

Exact times and operational identifiers remain in the private configuration.

## Windows endpoint plan

### Windows 10 desktop

The Windows 10 desktop implementation is complete and validated on the trusted LAN.

Controls include:

- an explicit user-profile source and direct UNC destination;
- separate Core, Downloads, VirtualBox, and All modes;
- incremental Robocopy behavior without deletion propagation;
- acceptable handling of Robocopy codes 0 through 7;
- an exclusive lock that prevents overlapping jobs;
- a VirtualBox-running safety check;
- locale-independent syslog timestamps;
- restricted script and local-log permissions;
- Task Scheduler execution as the signed-in user while the screen is locked; and
- stable remote summaries collected by Wazuh.

The Core task runs during each overnight work shift. Downloads and powered-off VirtualBox data run on separate weekly schedules to avoid long competing transfers. All three scheduled tasks returned successful results in validation.

A direct SMB restore matched the Windows source by SHA-256. The server then created an encrypted snapshot of the Windows mirror, restored the same representative file, and produced another byte-for-byte match. Temporary restore directories were removed after evidence collection.

The mirror uses additive `/E` behavior rather than `/MIR`; deleting a Windows source file does not automatically delete the recovery copy. Version history is provided by the encrypted server-side Restic repository.

Windows 10 is beyond ordinary support and must receive applicable extended security coverage or remain a temporary lab endpoint pending upgrade.

### Windows 11 laptop

Laptop implementation will proceed now for:

- direct LAN backup; and
- a clean no-connection outcome with local logging.

WireGuard fallback remains pending until the required laptop profile exists. The phase will not claim VPN coverage until off-network reachability, SMB authentication, backup execution, and restore behavior have been tested through the tunnel.

## Validation checklist

- [x] External backup disk positively identified before formatting
- [x] SMART short self-test completed without error
- [x] Target partition confirmed unmounted before formatting
- [x] New ext4 filesystem mounted persistently by UUID
- [x] Mount-point safety gate validated
- [x] Rsync failure reporting validated
- [x] Least-privilege exclusions documented
- [x] Corrected rsync run completed successfully
- [x] Representative rsync copies matched byte for byte
- [x] Restic repository initialized as the automation user
- [x] Incremental encrypted snapshots created
- [x] Retention mode completed successfully
- [x] Repository integrity check completed without errors
- [x] Real restore completed successfully
- [x] Restored files matched source files
- [x] Samba authenticated read/write/delete test passed
- [x] Samba anonymous access denied
- [x] Firewall limited Samba to trusted sources
- [x] Wazuh failure rule validated
- [x] Wazuh success rule validated
- [x] End-to-end Wazuh dashboard evidence captured
- [x] Windows 10 desktop scheduled backup validated
- [x] Windows 10 desktop restore validated
- [ ] Windows 11 laptop LAN backup validated
- [ ] Windows 11 laptop no-connection behavior validated
- [ ] Windows 11 laptop WireGuard backup validated
- [ ] Windows 11 laptop restore validated
- [ ] Full-volume recovery time measured

## Evidence

Sanitized outcome-level evidence is recorded in [evidence/README.md](evidence/README.md).

## Outcome

Atlas now has validated local rsync and encrypted Restic recovery paths, an authenticated network-backup target, scheduled Windows 10 protection, successful direct and encrypted restore tests, and Wazuh visibility into backup health.

The Windows 10 portion is complete. Phase 5 remains **in progress** until the approved Windows 11 laptop LAN, disconnected, restore, and later WireGuard scenarios are complete.
