# Linux Mint Cinnamon Workstation Setup and Learning Roadmap

> **Audience:** First-time Linux user
>
> **Primary OS:** Linux Mint Cinnamon
>
> **Decision record:** [ADR-012](decisions/ADR-012-linux-mint-cinnamon-primary-workstation.md)
>
> **Rule:** Complete and validate one stage before starting the next.

## Purpose

This guide builds the primary Project Cerberus workstation from zero assumed Linux knowledge. It separates essential foundation work from later specialist tooling so the learner can understand, validate, and recover each layer instead of installing everything at once.

Fedora KDE was the previous plan. It is superseded, not erased. Do not translate old instructions mechanically: `dnf`, RPM packages, COPR, and RPM Fusion are Fedora mechanisms. On Linux Mint, use `apt`, the Mint Software Manager, Flatpak when justified, or a vendor's documented Ubuntu/Debian repository.

## Before changing the computer

- [ ] Inventory hardware, applications, accounts, licenses, files, browser data, SSH keys, and recovery keys.
- [ ] Create two verified backups of irreplaceable data, with one copy disconnected.
- [ ] Export only the configuration and evidence allowed by the data-governance and portfolio policies.
- [ ] Confirm password-manager access and store disk-encryption, account-recovery, and security-key recovery information safely.
- [ ] Download Linux Mint Cinnamon from the official Linux Mint site and verify its published SHA-256 checksum.
- [ ] Create and test the installer USB without wiping the current disk.
- [ ] Record the wipe scope and satisfy the [Phase 1 entry gate](../phases/phase-00-program-governance/README.md#phase-1-entry-gate).

## Stage 1: Install and recover

During installation, choose full-disk encryption when compatible with the documented recovery plan. Do not enable automatic login. After first boot, open **Update Manager**, apply all supported updates, reboot, and use **Driver Manager** only for hardware that needs a recommended proprietary driver.

Open Terminal with `Ctrl`+`Alt`+`T`, then learn these safe inspection commands:

```bash
pwd
ls -la
whoami
ip address
lsblk
df -h
```

Create a Timeshift system snapshot and separately configure user-data backups. Timeshift is not a substitute for a file backup.

Validation:

- [ ] Wi-Fi/Ethernet, audio, Bluetooth, displays, webcam, suspend/resume, and reboot work.
- [ ] Updates complete without errors.
- [ ] The disk-recovery key is readable from another device.
- [ ] A test file can be restored from the user-data backup.

## Stage 2: Learn the operating system

Learn the filesystem (`/`, `/home`, `/etc`, `/var`), paths, files and directories, users and groups, permissions, processes, services, logs, package management, and help pages. Practice in a disposable directory or VM.

Core package workflow:

```bash
sudo apt update
apt list --upgradable
sudo apt upgrade
apt search <package-name>
apt show <package-name>
sudo apt install <package-name>
```

Read a command's help before copying unfamiliar commands. Never pipe an internet download directly into a privileged shell. Keep a learning log containing the goal, command, expected result, actual result, and recovery step.

## Stage 3: Secure access and source control

Install the baseline packages from Mint/Ubuntu repositories:

```bash
sudo apt update
sudo apt install curl git openssh-client ufw
sudo ufw enable
sudo ufw status verbose
```

Install `openssh-server` only if the workstation must accept inbound connections. Confirm the firewall rule and local network exposure before enabling it. Generate a modern SSH key, protect it with a passphrase, and add only the public key to services:

```bash
ssh-keygen -t ed25519 -a 100
git config --global user.name "Your Name"
git config --global user.email "your-address@example.com"
```

Install GitHub CLI from its current official Debian/Ubuntu instructions, then authenticate with `gh auth login`. Do not place tokens or private keys in the repository.

Use a reputable password manager. Register two hardware security keys where the service supports them, keep one as a secured backup, and save recovery codes offline.

## Stage 4: Virtualization

Confirm virtualization is enabled in firmware, then install the native virtualization stack:

```bash
sudo apt install qemu-kvm libvirt-daemon-system libvirt-clients virt-manager
sudo usermod -aG libvirt "$USER"
```

Sign out and back in before testing group membership. Create a small Linux test VM in virt-manager, use the default NAT network, patch the guest, take a snapshot, and practice restoring it. Do not bridge a VM to the physical network until the trust and exposure implications are understood.

## Stage 5: Containers -- Docker first

Docker is the beginner-first path because it matches the project's server architecture and learning material. Follow Docker's current official Ubuntu installation instructions, selecting the Ubuntu base version that the installed Mint release uses. Do not reuse Fedora/RPM instructions.

Validate the engine and Compose plugin:

```bash
docker version
docker compose version
sudo docker run --rm hello-world
```

Learn images, containers, ports, volumes, networks, logs, Compose files, updates, and cleanup. Understand that the `docker` group grants root-equivalent control before choosing whether to add the user to it.

After completing at least one documented Compose deployment, install Podman from `apt` and repeat a small lab:

```bash
sudo apt install podman
podman run --rm docker.io/library/hello-world
```

Record differences in daemon model, rootless operation, networking, Compose compatibility, and service management. Podman supplements Docker; it does not replace the initial Docker path.

## Stage 6: Python and automation

Keep the operating system's Python environment clean:

```bash
sudo apt install python3 python3-venv pipx ansible
python3 --version
ansible --version
```

Install `uv` using its current official documentation, verify the downloaded installer or package where possible, and use project-local environments. Learn Python files, virtual environments, dependencies, formatting, tests, and secret-safe configuration before using Ansible against real hosts.

Begin Ansible with `localhost`, inventory files, facts, check mode, and a reversible playbook. Never test an unfamiliar playbook against production or the only recoverable host.

## Stage 7: Add tools when a phase needs them

Do not install this entire section on day one. For tools that change quickly, use current official Debian/Ubuntu instructions and verify repository signing keys, supported releases, and checksums.

| Capability | Tool | Learning gate |
|---|---|---|
| Cloud administration | AWS CLI | Configure a least-privilege lab account; never commit credentials |
| Infrastructure as code | OpenTofu or Terraform | Learn plan/state/drift in a disposable lab; choose one primary tool per project |
| Kubernetes | kubectl, Helm, k9s | Start only after containers, YAML, networking, and secrets are understood |
| Packet and host analysis | Wireshark, Nmap | Capture or scan only systems and networks explicitly authorized for testing |
| Browser-based analysis | CyberChef | Prefer the official site or a pinned local container; sanitize sensitive inputs |
| Remote administration | Remmina | Save credentials in the password manager, not plain-text profiles |
| File synchronization | Syncthing | Limit trusted devices and folders; validate versioning and recovery |
| Nearby transfer | LocalSend | Use trusted local networks and verify the destination before accepting files |

Useful Mint repository packages include:

```bash
sudo apt install wireshark nmap remmina syncthing
```

Wireshark may ask whether non-root users can capture packets. Grant capture access only to the dedicated group and only when required. LocalSend and k9s may be better installed from their current verified upstream release or supported app source if the Mint repository does not provide an appropriate version.

## Stage 8: Operate and document

For every installed tool, record its purpose and owner; installation source and version; privileged groups, ports, services, and credentials; backup location; update and removal procedure; validation; limitations; and recovery procedure.

Monthly, review updates, failed services, disk space, backup results, firewall rules, SSH access, container exposure, VM snapshots, and stale credentials. Quarterly, test a file restore and review hardware security keys and recovery codes.

## Completion criteria

- [ ] Linux Mint Cinnamon is updated, encrypted as planned, backed up, and recoverable.
- [ ] The learner can explain basic navigation, packages, permissions, processes, services, logs, and the firewall.
- [ ] SSH and GitHub authentication work without exposed secrets.
- [ ] A KVM/libvirt VM can be created, isolated, snapshotted, and restored.
- [ ] A Docker Compose application can be deployed, inspected, updated, backed up, and removed.
- [ ] Podman has been tested only after the Docker learning gate.
- [ ] Python/uv and an Ansible localhost lab work without modifying system Python.
- [ ] Specialist tools are installed only when needed and have documented validation and recovery steps.
