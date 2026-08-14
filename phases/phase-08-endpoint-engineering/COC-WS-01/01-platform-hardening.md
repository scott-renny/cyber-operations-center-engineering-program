# COC-WS-01 Platform Hardening

## Platform assessment

The workstation runs Windows 10 Pro 22H2 on legacy hardware. Secure Boot is available and enabled. No TPM is presented to Windows, so hardware-backed BitLocker protection is unavailable. Windows Update confirmed current cumulative updates, Defender intelligence, and Extended Security Updates enrollment.

## Native security baseline

- Antivirus, antispyware, real-time, behavior, IOAV, on-access, cloud, and tamper protection enabled
- Potentially unwanted application protection enforced
- Network protection enabled after an audit period produced no compatibility events
- Controlled Folder Access retained in Audit mode because testing confirmed legitimate automation impact
- No active threats after remediation and rescanning
- All Windows Firewall profiles enabled
- UAC enabled with secure-desktop consent prompting
- Automatic workstation lock set to 900 seconds and password-on-wake enabled
- Built-in Administrator and Guest accounts disabled
- Unneeded guest-style account disabled and primary local administrator corrected to require a password
- Intentional standard and Codex sandbox accounts retained with limited membership
- SMB1, insecure SMB guest logons, and Windows PowerShell 2 disabled
- Remote Desktop and Remote Registry disabled; WinRM not exposed
- No unexpected Defender exclusions or non-default SMB shares observed

## Privacy

Advertising ID and tailored diagnostic experiences were disabled. Cross-device activity publication and upload were disabled. Diagnostic data was set to the lowest effective Windows 10 Pro policy level rather than an unsupported value.

## Software maintenance

Installed applications were updated through the Windows package manager. 7-Zip and the Sysinternals Suite were added as maintained utilities. Defender remains the primary Windows antimalware engine; a second resident antivirus was intentionally not installed.

## Connectivity decision

A fixed desktop does not require a routine WireGuard client merely to reach services on its trusted home LAN. Remote access remains bounded by the server-side VPN architecture.
