# ADR-012: Linux Mint Cinnamon is the primary workstation

- **Status:** Accepted
- **Date:** 2026-08-15
- **Owner:** COC Program Owner
- **Related phase(s):** Phase 8.5
- **Related risk(s):** R-021
- **Supersedes:** [ADR-011](ADR-011-use-fedora-for-primary-workstation.md)

## Context

ADR-011 selected Fedora KDE for the replacement workstation. Before Phase 8.5 implementation, the program locked Linux Mint Cinnamon instead. The intended operator begins with no assumed Linux knowledge, so the decision prioritizes a familiar desktop, conservative maintenance, Ubuntu-compatible documentation, and a gradual learning path while preserving the same clean, encrypted, monitored migration objective.

## Decision

Use the current supported Linux Mint Cinnamon release as the primary daily-driver and administration workstation. Use Linux Mint/Ubuntu `apt` packages and compatible vendor repositories instead of Fedora `dnf`, RPM, COPR, or RPM Fusion instructions.

Docker and Docker Compose are the beginner-first container workflow. Podman remains in scope for later comparative learning. Retain KVM/QEMU, libvirt, virt-manager, SSH, Git/GitHub CLI, Python/uv, Ansible, AWS CLI, Terraform or OpenTofu, kubectl, Helm, k9s, Wireshark, Nmap, CyberChef, Remmina, Syncthing, LocalSend, and password-manager/security-key tooling, introduced progressively.

Ubuntu Server remains the service host. This decision changes the replacement workstation, not the server platform.

## Alternatives Considered

- **Fedora KDE:** Strong security defaults and useful Red Hat ecosystem exposure, but a faster change cadence and less direct alignment with the chosen beginner-oriented Ubuntu/Mint learning path.
- **Ubuntu Desktop:** Broad support, but Cinnamon and the Linux Mint desktop experience are preferred.
- **Windows with WSL:** Useful as a secondary compatibility path, but insufficient as the primary Linux desktop and KVM host.

## Rationale

Linux Mint Cinnamon reduces initial desktop friction while preserving the Linux, virtualization, container, automation, cloud, Kubernetes, and security skills required by the program.

## Security Implications

- Verify official installation-media checksums and enable full-disk encryption with a tested recovery path.
- Apply updates before additional tooling and enable the host firewall.
- Treat `sudo`, `docker`, and `libvirt`-related groups as privileged.
- Use signed repositories, a password manager, offline recovery codes, and two hardware security keys where practical.
- Preserve the Phase 8 Windows source until the Mint backup and isolated restore pass.

## Consequences

ADR-011 is superseded. Fedora commands and controls are historical rather than active Phase 8.5 instructions. Fedora remains a future VM or secondary learning target. Phase 8.5 uses Mint/Ubuntu package, AppArmor, UFW, encryption, monitoring, backup, and recovery controls.

## Validation

- Mint boots with Secure Boot and full-disk encryption validated as supported by the chosen installer and hardware.
- Updates, UFW, AppArmor, Wazuh, backup/restore, hardware, and security-key workflows pass.
- Docker Compose and a KVM/libvirt test VM run successfully.
- SSH and GitHub authentication work without exposed secrets.

## Review Date or Trigger

Review near Mint end of support, after material hardware incompatibility, or when required tooling or learning objectives change.
