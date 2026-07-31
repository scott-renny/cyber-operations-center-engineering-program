# Phase 5 Validation Evidence

**Status:** Server-side controls validated; endpoint controls pending  
**Evidence classification:** Public, sanitized  
**Validation date:** 2026-07-31  
**Asset:** Atlas (`coc-srv-01`)

## Publication decision

This record contains outcome-level evidence only. The following were intentionally excluded:

- disk serial numbers and filesystem UUIDs;
- live private addresses and VPN addressing;
- account names other than the approved asset identity;
- passwords, password files, private keys, certificates, and credential archives;
- Restic repository identifiers;
- raw backup contents;
- full firewall exports;
- unredacted dashboard screenshots; and
- logs containing unnecessary operational identifiers.

## Validation summary

| Control | Sanitized observation | Result |
|---|---|---|
| Disk identity | External backup disk distinguished from the active system disk by multiple attributes | Pass |
| Disk health | SMART overall health passed; short self-test completed without error | Pass |
| Destructive safety | Target partition confirmed unmounted and explicitly authorized | Pass |
| Filesystem | New ext4 filesystem created and mounted by UUID | Pass |
| Persistent mount | Configuration parsed without errors and remounted successfully | Pass |
| Capacity | Expected usable capacity visible at the backup mount | Pass |
| Mount safety | Scripts rejected unverified mount state and UUID | Pass |
| Rsync failure handling | Unreadable protected file caused a reported failure and nonzero exit | Pass |
| Least privilege | Root-protected credential archive retained restrictive ownership | Pass |
| Rsync retry | Corrected run completed with exit code 0 | Pass |
| Rsync copy integrity | Representative source and destination files matched byte for byte | Pass |
| Restic password access | Exact automation account read the mode-600 password file | Pass |
| Restic snapshot | Initial encrypted snapshot completed successfully | Pass |
| Restic incrementality | Second snapshot reused the parent and stored only changed data | Pass |
| Retention | Daily, weekly, and monthly policy applied successfully | Pass |
| Repository integrity | Restic check reported no errors | Pass |
| Restore | Latest snapshot restored successfully to a separate directory | Pass |
| Restore integrity | Representative restored files matched sources byte for byte | Pass |
| Restore permissions | Restricted ownership and modes were preserved | Pass |
| Samba authentication | Authenticated upload, list, download, and delete succeeded | Pass |
| Samba read-back | Downloaded test content matched the source | Pass |
| Anonymous Samba | Access denied | Pass |
| Firewall | Samba limited to trusted LAN and VPN sources | Pass |
| Wazuh log paths | Two named stable log files registered | Pass |
| Wazuh failure rule | Expected level-7 rule selected and alerted | Pass |
| Wazuh success rule | Expected level-5 rule selected and alerted | Pass |
| Dashboard | Both sanitized test outcomes visible for Atlas | Pass |
| Windows desktop | Implementation not yet performed | Pending |
| Windows laptop LAN | Implementation not yet performed | Pending |
| Windows laptop VPN | WireGuard profile and test not yet available | Pending |

## Functional evidence

### Disk preparation

Read-only identity, capacity, partition, USB-bridge, and SMART checks were performed before the destructive action. The operating-system disk was identified by its active root and boot mounts. The external target was separately identified, tested, unmounted, and explicitly authorized.

The new filesystem received a new UUID, mounted at the approved path, and exposed the expected usable capacity.

### Rsync

The first run demonstrated that the failure path was real: a root-protected credential archive could not be read by the normal automation account, and the script returned a failure rather than masking the omission.

The credential archive contained security-sensitive installation material. Its restrictive permissions were preserved. The script was updated to document and exclude the accepted least-privilege gap. A second run succeeded, and representative home, Docker-stack, and management-platform files matched their copies.

### Restic

Two encrypted snapshots were created. The second snapshot used the first as its parent and added only changed data.

Retention completed successfully. Repository checking examined packs, snapshots, trees, and blobs and reported no errors.

A real restore recovered the latest snapshot into a separate directory. Representative files matched the active sources, and restrictive permissions remained intact.

### Samba

A test file was uploaded through SMB authentication, listed, downloaded, compared, and deleted. The read-back content matched the source. A separate anonymous attempt was denied.

### Wazuh

The log collector registered exactly two named backup log paths. No backup wildcard was used.

Rule testing proved the expected pre-decoding and rule selection for both status markers. End-to-end synthetic events written to the stable files produced the expected level-7 and level-5 alerts in the Wazuh dashboard.

## Recovery objectives

- **RPO:** up to 24 hours from nightly scheduling.
- **Demonstrated RTO:** under one minute for the small validation dataset.
- **Full-volume RTO:** pending a representative large-data recovery exercise.

## Accepted limitations

- The rsync mirror is not encrypted at rest.
- Root- and container-owned exclusions reduce rsync coverage.
- Live container databases may require application-aware export or quiescing for guaranteed consistency.
- The Restic recovery password must be retained outside the protected server.
- The Samba guest-mapping compatibility setting remains globally available, although the backup share itself denies guest access and requires a named account.
- Windows desktop and laptop automation remain incomplete.
- Laptop WireGuard fallback cannot be validated until the required profile exists.

## Evidence integrity

Evidence was transcribed from direct command output and administrative interfaces during the implementation session. Raw artifacts remain private because they contain operational identifiers, addresses, filesystem metadata, or security-sensitive paths.

This public record preserves the control result, failure behavior, recovery result, and reason for each sanitization decision.
