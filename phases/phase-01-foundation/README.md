# Phase 1 — Foundation: Full Wipe & Clean-Slate Rebuild

**Status:** Complete  
**Completion date:** 2026-07-27  
**Budget:** $0  
**Asset ID:** `coc-srv-01`  
**Friendly name:** Atlas

## Goal

Replace several months of iterative homelab configuration with a clean, consistently versioned, documented Ubuntu Server foundation for every subsequent Cyber Operations Center phase.

## Scope

Phase 1 covered:

- household DNS and DHCP continuity before the maintenance window;
- isolation of the external backup HDD from the destructive operation;
- acquisition and checksum verification of official Ubuntu installation media;
- complete erasure and reinstallation of the server's internal SSD;
- assignment of the final asset-style hostname;
- installation of a minimized Ubuntu Server baseline;
- restoration of the laptop's Broadcom wireless support;
- installation and validation of OpenSSH;
- operating-system updates and reboot validation; and
- prevention of lid-close, idle, suspend, and hibernation events from interrupting server workloads.

The external backup HDD, legacy repositories, and previous project artifacts were explicitly outside the wipe scope.

## Change planning and service continuity

The server previously supported household services, including DNS, DHCP-dependent infrastructure, remote access, and parental-control functions. Before the wipe:

- the router was returned to public DNS;
- router-provided DHCP was available;
- the external backup HDD was physically disconnected; and
- previous project work remained preserved in legacy repositories.

The public DNS fallback remains temporary and will be removed only after Pi-hole is rebuilt and validated in Phase 4.

## Installation media

The official Ubuntu Server 24.04.4 LTS AMD64 image was downloaded from Canonical and verified against the published SHA-256 checksum before being written to an 8 GB USB drive.

Validation result:

```text
ubuntu-24.04.4-live-server-amd64.iso: OK
```

The USB installer is retained as recovery media.

## Storage implementation

The installer was booted in UEFI mode. The external backup HDD remained disconnected, leaving only the internal SSD and installer USB visible during disk selection.

The internal SSD received a full-disk reinstall with LVM:

| Mount point | Type | Approximate size |
|---|---|---:|
| `/boot/efi` | FAT32 EFI system partition | 1 GB |
| `/boot` | ext4 | 2 GB |
| `/` | ext4 on LVM | 229.8 GB |

Full-disk encryption was not enabled because Atlas must restart unattended after power events and maintenance. This decision will be revisited if the server's physical-risk profile changes.

## Installed baseline

| Item | Validated state |
|---|---|
| Hardware | Dell Latitude E7250 |
| Operating system | Ubuntu Server 24.04.4 LTS (Noble) |
| Architecture | x86-64 |
| Hostname | `coc-srv-01` |
| Installation profile | Minimized Ubuntu Server |
| Boot mode | UEFI |
| Storage | Full internal SSD allocated through LVM |
| Network | Broadcom BCM4352 Wi-Fi using the proprietary `wl` driver |
| Addressing | Private DHCP address; public value intentionally sanitized |
| Remote administration | OpenSSH installed, enabled, and tested |
| Patch state | Package indexes refreshed; full upgrade completed; reboot validated |
| Sleep behavior | Lid close and idle actions ignored; sleep targets masked |

The friendly name **Atlas** is used in diagrams and narrative documentation. The stable technical hostname remains `coc-srv-01`.

## Wireless-driver recovery

The minimized installer did not provide a working driver for the Broadcom BCM4352 adapter. Temporary phone tethering was used to reach Ubuntu repositories. The following packages and controls restored wireless operation:

- `bcmwl-kernel-source` for the proprietary `wl` kernel module;
- `wpasupplicant` for Wi-Fi authentication; and
- Netplan configuration with DHCP for the wireless interface.

The server was rebooted to allow module-selection changes to take effect. Validation confirmed that `wl` controlled the adapter and that Wi-Fi reconnected without tethering.

Wi-Fi credentials are stored only in a root-readable Netplan file and are not committed to this repository.

## SSH implementation

The offline minimized installation did not leave SSH active, so `openssh-server` was installed after networking was restored. The service was enabled at boot and validated through a successful login from a separate Windows workstation.

Password-based access remains temporarily available for initial administration. Phase 2 will introduce SSH keys, validate key-based login, and disable password authentication.

## Server power behavior

Because Atlas is a laptop operating as a server, default laptop sleep behavior was explicitly disabled.

`systemd-logind` is configured to ignore:

- lid-close events on battery or external power;
- docked lid-close events; and
- idle actions.

The following targets are masked:

- `sleep.target`;
- `suspend.target`;
- `hibernate.target`; and
- `hybrid-sleep.target`.

The laptop must remain on a hard, ventilated surface, particularly when operated with the lid closed.

## Validation checklist

- [x] Router provides temporary public DNS and DHCP
- [x] Backup HDD physically disconnected before the wipe
- [x] Previous project material retained in legacy repositories
- [x] Official Ubuntu Server ISO downloaded
- [x] ISO checksum validated
- [x] Installer USB created and booted in UEFI mode
- [x] Internal SSD selected and fully erased
- [x] Ubuntu Server 24.04.4 LTS installed
- [x] Minimized installation profile retained
- [x] Hostname set to `coc-srv-01`
- [x] Entire internal SSD allocated through LVM
- [x] Broadcom `wl` driver installed and active
- [x] Wi-Fi reconnects automatically after reboot
- [x] Full operating-system update completed
- [x] OpenSSH installed, enabled, listening, and remotely tested
- [x] Lid-close and idle actions configured not to suspend the server
- [x] Sleep, suspend, hibernate, and hybrid-sleep targets masked
- [x] Sanitized validation evidence recorded

## Security considerations

- The backup HDD was physically excluded from the wipe scope.
- No passwords, Wi-Fi credentials, machine IDs, boot IDs, MAC addresses, serial numbers, or live private IP addresses are stored in the public repository.
- Public screenshots are withheld where reflections or infrastructure details could expose personal or operational information.
- SSH password authentication is a temporary Phase 1 bootstrap condition and will be removed after key validation in Phase 2.
- The server currently relies on Wi-Fi. Wired networking remains the preferred future state for reliability and infrastructure services.
- The current address is assigned by DHCP. Phase 2 will establish a router reservation before services depend on a stable address.

## Troubleshooting record

### Installer USB did not appear in the UEFI boot menu

The existing USB contained driver packages rather than bootable installation media. It was erased and recreated from the verified Ubuntu Server ISO. The firmware then detected it as a UEFI USB device.

### USB image writing appeared to stall

The image data had been copied, but `dd` remained active while `conv=fsync` flushed the USB device's cache. The process was allowed to finish and returned the expected records-in/records-out summary.

### Broadcom Wi-Fi was absent after installation

The BCM4352 adapter required `bcmwl-kernel-source`. The minimized environment also required `wpasupplicant`. Temporary USB tethering provided repository access.

### Phone tethering repeatedly disappeared

Kernel USB error `-71` and RNDIS watchdog messages indicated an unstable physical data connection. Reconnecting the phone restored temporary connectivity long enough to install the required packages. The tether was removed after Wi-Fi validation.

### Netplan Wi-Fi service returned status 203/EXEC

The generated Wi-Fi service could not execute because `wpa_supplicant` was missing from the minimized installation. Installing `wpasupplicant` and applying Netplan resolved the failure.

## Lessons learned

- Verify that installation media is actually bootable rather than relying on its label or prior use.
- A checksum validates the downloaded image; it does not prove an existing USB was written correctly.
- Physical disconnection is the strongest protection for excluded storage during destructive work.
- Minimized server installations reduce boot noise and package count but may omit expected operational utilities.
- Proprietary wireless drivers can require both a kernel module and a separate authentication component.
- Temporary connectivity needs a fallback when the primary adapter depends on a post-install driver.
- Asset-style hostnames scale better than friendly names; both can coexist through documented naming.
- Laptop power defaults must be changed explicitly before the device can serve reliably with its lid closed.

## Known limitations and deferred work

- The server currently uses Wi-Fi rather than wired Ethernet.
- Its DHCP address is not yet reserved.
- SSH password authentication remains enabled until keys are validated.
- Base firewall, intrusion prevention, auditing, and mandatory-access-control validation belong to Phase 2.
- The external backup HDD remains disconnected and will receive deliberate handling during Phase 5.
- Public DNS fallback remains in place until Pi-hole is rebuilt and validated in Phase 4.

## Evidence

Sanitized command evidence and the public-release decision for screenshots are recorded in [evidence/README.md](evidence/README.md).

## Outcome

Atlas now boots from a clean, updated, minimized Ubuntu Server 24.04.4 LTS baseline with a stable asset identity, full internal-disk allocation, automatic Wi-Fi, working remote administration, and server-appropriate power behavior.

Phase 1 removed the prior configuration drift without restoring legacy services. The environment is ready for **Phase 2 — Base Hardening**.
