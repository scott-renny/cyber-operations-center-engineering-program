# Phase 5 — Backup and Recovery

> **Status:** Complete  
> **Completed:** 2026-08-05  
> **Next phase:** Phase 6 — NET-WATCH

## Purpose

Establish a repeatable, monitored backup-and-recovery capability for important server configuration, operational data, Windows workstation files, and laptop user data.

## Completed capabilities

### Backup storage and server protection

- Dedicated external storage with persistent UUID-based mounting
- Filesystem identity and mount-point checks before automated writes
- Unprivileged rsync mirrors for approved server and container data
- Encrypted, compressed, deduplicated Restic snapshots
- Scheduled retention, pruning, and repository integrity checks
- Authenticated Samba storage restricted to trusted network sources
- Documented least-privilege exclusions for protected credential material

### Windows 10 workstation protection

- Incremental SMB backups using explicit source paths and a direct UNC destination
- Separate Core, Downloads, powered-off VirtualBox, and full modes
- An overlap lock preventing simultaneous jobs
- A guard that skips virtual-machine data while VirtualBox is running
- Correct handling of successful Robocopy codes 0 through 7
- Task Scheduler execution as the signed-in user while the screen is locked
- Direct SMB restore validation with matching SHA-256 hashes
- Encrypted server-side snapshots of the Windows mirror
- Successful encrypted restore with byte-for-byte comparison

### Windows 11 laptop protection

- Successful backup over the trusted LAN
- Nightly scheduled execution under the signed-in user
- Successful WireGuard fallback when direct LAN SMB was unavailable
- A clean no-connection outcome that logged a skip and returned code 0
- Successful representative restore with zero failed files
- Credential Manager use without embedding the Samba password in scripts
- Deliberate exclusion of live local application state requiring VSS or imaging

### Monitoring and evidence

- Stable local and remote logs
- Wazuh collection of server, workstation, laptop, and encrypted-snapshot outcomes
- Level-5 success and level-7 failure rules
- Successful rule testing and end-to-end alert validation
- Sanitized public evidence excluding credentials and private identifiers

## Architecture

~~~text
Approved server data ── rsync and encrypted Restic ──┐
                                                     ▼
                                           External backup disk
                                                     ▲
Windows workstation ── authenticated SMB mirror ────┤
Windows laptop ── LAN or WireGuard SMB mirror ──────┘
                                                     │
                                   encrypted Restic version history
                                                     │
                                           tested restore paths

Stable backup logs ────────────────────────────────► Wazuh
~~~

The directly accessible mirrors provide fast local recovery. Restic provides the encrypted, deduplicated, versioned path.

## Scheduling

Server jobs use non-overlapping schedules for rsync, snapshots, retention, pruning, and repository checks.

The Windows workstation separates small daily data from larger Downloads and powered-off VirtualBox jobs. The laptop runs nightly and selects LAN first, WireGuard second, or exits cleanly when neither path is available.

Exact times, addresses, filesystem identifiers, repository identifiers, and accounts remain in private operational configuration.

## Validation summary

Phase completion required demonstrated recovery, not merely successful backup commands.

Validated outcomes include:

- positive identification and health testing of the external target before formatting;
- successful persistent mounting and mount-safety checks;
- rsync failure reporting, corrected execution, and byte comparisons;
- successful Restic backup, retention, and integrity modes;
- a server-home restore preserving representative content and permissions;
- authenticated Samba read, write, download, comparison, and deletion;
- denial of anonymous Samba access;
- successful workstation Core, Downloads, and VirtualBox scheduled tasks;
- matching workstation source, SMB copy, and direct restore hashes;
- an encrypted workstation-mirror snapshot of approximately 76 GiB completed in about 1 hour 6 minutes;
- a byte-identical workstation restore from the encrypted repository;
- successful laptop LAN backup and scheduled task execution;
- successful laptop WireGuard fallback;
- a clean laptop no-connection skip with exit code 0;
- restoration of 320 laptop files totaling approximately 5.82 MB in 37 seconds with zero failures; and
- expected Wazuh backup-health alerts.

Detailed sanitized outcomes are recorded in [evidence/README.md](evidence/README.md).

## Recovery objectives

- **Server and workstation RPO:** up to 24 hours
- **Laptop RPO:** up to 24 hours
- **Laptop demonstrated sample RTO:** 37 seconds for 320 files totaling approximately 5.82 MB
- **Small server and workstation sample restores:** under one minute
- **Full-device recovery time:** dependent on dataset size, throughput, and destination

## Security considerations

- Credentials, encryption secrets, private keys, and recovery passwords remain outside the public repository.
- Scripts use explicit destinations and reject unsafe or unavailable paths.
- Windows tasks run as the approved signed-in user rather than SYSTEM to use protected Credential Manager entries.
- Robocopy uses additive behavior rather than automatic deletion propagation; encrypted Restic supplies version history.
- VirtualBox data is copied only while the VM is stopped.
- Laptop local application state is excluded because consistent recovery requires VSS, application-aware export, or imaging.
- Restore tests use controlled destinations and remove temporary data afterward.
- Published evidence omits live addresses, UUIDs, serials, repository identifiers, credentials, raw content, and unredacted screenshots.
- Windows 10 remains a temporary lab endpoint requiring applicable extended security coverage or upgrade.

## Accepted limitations

- Direct rsync and SMB mirrors are not encrypted at rest.
- Root- and container-owned exclusions reduce unprivileged rsync coverage.
- Live databases may require application-aware export or quiescing.
- Laptop local application state requires VSS or imaging.
- Recovery passwords must be retained separately.
- Bare-metal recovery was outside this phase.

## Operational outcome

The environment entered Phase 6 with validated server, Windows workstation, and Windows laptop recovery paths. Phase 5 demonstrated scheduled execution, encrypted versioning, integrity checking, LAN and VPN transport, graceful disconnected behavior, monitoring, and real restores.

## Related project history

Earlier backup engineering and lessons learned are preserved in the [Backup Lab](https://github.com/scott-renny/backup-lab) legacy project.
