# Phase 1 — Sanitized Validation Evidence

**Validation date:** 2026-07-27  
**Asset ID:** `coc-srv-01`  
**Public-release status:** Approved after sanitization

## Evidence handling

This public evidence record intentionally omits:

- passwords and Wi-Fi credentials;
- machine and boot identifiers;
- MAC addresses and hardware serial numbers;
- live private IP addresses;
- exact physical location details; and
- screenshots containing screen reflections or operational identifiers.

Original console photographs were used during guided implementation but are retained outside the public repository. Text below preserves the validated technical facts without exposing restricted fields.

## Operating-system baseline

Commands:

```bash
hostnamectl
lsb_release -a
```

Sanitized result:

```text
Static hostname: coc-srv-01
Chassis: laptop
Operating System: Ubuntu 24.04.4 LTS
Kernel: Linux 6.8.0-136-generic
Architecture: x86-64
Hardware Vendor: Dell Inc.
Hardware Model: Latitude E7250

Distributor ID: Ubuntu
Description: Ubuntu 24.04.4 LTS
Release: 24.04
Codename: noble
```

Result: **Pass** — the server runs the required Ubuntu Server 24.04 LTS baseline under the final asset hostname.

## Storage baseline

Command:

```bash
lsblk
```

Sanitized result:

```text
NAME                      SIZE TYPE MOUNTPOINTS
sda                     232.9G disk
├─sda1                      1G part /boot/efi
├─sda2                      2G part /boot
└─sda3                  229.8G part
  └─ubuntu--vg-ubuntu--lv
                        229.8G lvm  /
```

Result: **Pass** — the internal SSD was repartitioned for the clean installation, and the root logical volume uses the available LVM capacity.

The external backup HDD is absent from this output because it remained physically disconnected.

## Installation-media integrity

Command:

```bash
sha256sum -c SHA256SUMS --ignore-missing
```

Result:

```text
ubuntu-24.04.4-live-server-amd64.iso: OK
```

Result: **Pass** — the downloaded image matched Canonical's published checksum before it was written to USB.

## Wireless-driver validation

Command:

```bash
lspci -nnk | grep -A3 -i network
```

Sanitized result:

```text
Network controller: Broadcom Inc. BCM4352 802.11ac Dual Band Wireless Network Adapter
Kernel driver in use: wl
Kernel modules: bcma, wl
```

Command:

```bash
ip -4 -br address
```

Sanitized result:

```text
lo       UNKNOWN 127.0.0.1/8
wlp2s0   UP      192.168.1.x/24
```

Result: **Pass** — the proprietary Broadcom driver is active, and Wi-Fi reconnects through DHCP after reboot.

## SSH validation

Commands:

```bash
systemctl is-active ssh
sudo ss -lntp | grep ':22'
```

Sanitized result:

```text
active
LISTEN ... :22 ... sshd
```

A separate Windows workstation completed an interactive SSH login and received the expected prompt:

```text
scott@coc-srv-01:~$
```

Result: **Pass** — OpenSSH is enabled, listening, and remotely accessible on the trusted household network.

## Patch and reboot validation

Commands used:

```bash
sudo apt update
sudo apt full-upgrade -y
sudo reboot
```

After reboot, hostname, storage, Wi-Fi, and SSH checks were repeated successfully.

Result: **Pass** — the clean baseline remained operational after applying available updates and restarting.

## Power-behavior validation

Command:

```bash
systemctl is-enabled sleep.target suspend.target hibernate.target hybrid-sleep.target
```

Expected and observed state:

```text
masked
masked
masked
masked
```

`systemd-logind` is also configured to ignore lid-close and idle actions.

Result: **Pass** — laptop power defaults will not suspend server workloads when the lid closes or the system sits idle.

## Phase 1 validation result

| Control | Result |
|---|---|
| Official installation media checksum | Pass |
| Backup HDD excluded from wipe | Pass |
| Full internal-disk reinstall | Pass |
| Ubuntu Server 24.04 LTS baseline | Pass |
| Final asset hostname | Pass |
| Minimized installation profile | Pass |
| Full LVM root allocation | Pass |
| Broadcom Wi-Fi recovery | Pass |
| Automatic network reconnection | Pass |
| Operating-system updates | Pass |
| Reboot persistence | Pass |
| OpenSSH service | Pass |
| Remote SSH login | Pass |
| Lid and sleep controls | Pass |
| Public evidence sanitization | Pass |

**Overall result: PASS — Phase 1 completion criteria satisfied.**
