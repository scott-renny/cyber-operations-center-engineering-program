# Phase 8.5 Linux Mint Migration Validation Checklist

## Installation trust

- [ ] Current supported Linux Mint Cinnamon image obtained from the Linux Mint project
- [ ] Published checksum obtained through an independent official path
- [ ] Signed checksum verified
- [ ] Image checksum verified
- [ ] Installation media created and boot-tested
- [ ] Firmware and storage targets positively identified before destructive installation

## Platform security

- [ ] UEFI mode confirmed
- [ ] Secure Boot enabled and verified
- [ ] Required hardware functions without disabling Secure Boot
- [ ] LUKS2-backed encryption selected during installation
- [ ] Root and user data confirmed on encrypted backing storage
- [ ] Encryption passphrase and recovery process tested
- [ ] Recovery material stored outside the workstation and repository
- [ ] AppArmor reports active profiles
- [ ] No AppArmor denials were bypassed by disabling protection
- [ ] UFW enabled and active
- [ ] Active zone and allowed services reviewed
- [ ] No unnecessary listening services
- [ ] Screen lock and password-on-resume validated
- [ ] Firmware, Linux Mint, and application updates applied

## Identity and secrets

- [ ] Standard daily account established
- [ ] Administrative elevation requires deliberate authentication
- [ ] Password manager installed from a trusted source
- [ ] Primary and recovery authentication tested
- [ ] Hardware security keys enrolled only after account inventory review
- [ ] Old SSH private keys reviewed; new keys issued where practical
- [ ] Old workstation credentials and registrations scheduled for revocation

## Monitoring

- [ ] Supported Wazuh Linux agent installed
- [ ] Agent version compatible with the manager
- [ ] Permanent Linux Mint asset identity approved
- [ ] Wazuh service enabled and active
- [ ] Centralized connectivity confirmed
- [ ] Controlled file-integrity event received
- [ ] System inventory and vulnerability visibility confirmed
- [ ] Relevant authentication, sudo, AppArmor, UFW, and system logs collected
- [ ] Temporary enrollment exposure closed after registration

## Selective data restoration

- [ ] Approved Phase 8 snapshot identified
- [ ] Historical warning-tagged snapshots excluded from bulk restore
- [ ] Restore destination is the new user home, not a Windows profile overlay
- [ ] Documents, media, repositories, and approved project data restored by category
- [ ] Downloads restored only by explicit review
- [ ] Windows executables, registry data, services, and caches excluded
- [ ] Restored data scanned
- [ ] Representative source and restored files compared
- [ ] Ownership and permissions reviewed
- [ ] Sensitive files restricted to the intended user
- [ ] Browser state rebuilt without importing unsafe caches or complete profiles

## Application acceptance

- [ ] Every required application has a recorded Linux Mint disposition
- [ ] Native or Flatpak applications installed only from reviewed sources
- [ ] Critical workflows tested
- [ ] Windows virtual machines isolated and justified
- [ ] No compatibility layer granted broad host access without review
- [ ] Backup client and schedule rebuilt for Linux Mint
- [ ] First Linux Mint backup completed and restored successfully

## Retirement gate

- [ ] User confirms Linux Mint is the accepted primary workstation
- [ ] Required data and applications validated
- [ ] Linux Mint monitoring and backups healthy
- [ ] Temporary Windows Wazuh identity revoked
- [ ] Windows-specific VPN or service registrations revoked
- [ ] Hardware-key registrations updated deliberately
- [ ] Legacy storage sanitized
- [ ] Hardware disposition recorded
- [ ] Phase 8.5 completion report published
