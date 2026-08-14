# COC-WS-01 Validation

| Control | Result |
|---|---|
| Windows 10 Pro 22H2 and ESU servicing | Pass |
| Outstanding Windows software updates | Pass — zero after update and restart |
| Secure Boot | Pass |
| TPM | Not available — documented exception |
| Operating-system drive encryption | Not enabled — documented Phase 8.5 exception |
| Defender core and tamper protections | Pass |
| PUA and network protection | Pass — enforced |
| Controlled Folder Access | Audit-only exception |
| Active Defender threats | Pass — zero |
| Defender full, Downloads, and offline scans | Pass after remediation |
| Firewall Domain, Private, and Public profiles | Pass |
| UAC, inactivity lock, and password on wake | Pass |
| SMB1, insecure SMB guest access, and PowerShell 2 | Pass — disabled |
| Unneeded guest-style account | Pass — disabled |
| Remote Desktop and Remote Registry | Pass — disabled |
| Unexpected Defender exclusions | Pass — none observed |
| Sysmon service, driver, and event generation | Pass |
| Wazuh service, connectivity, and Sysmon receipt | Pass |
| Enrollment exposure after registration | Pass — closed |
| Encrypted backup snapshot | Pass |
| Unsafe filenames absent from approved snapshot | Pass |
| Restic restore and hash comparison | Pass |
| Full ClamAV staging scan | Pass — zero infected files |

Raw screenshots, local paths, addresses, agent keys, and backup identifiers are retained privately. Revalidate after material Windows, Defender, Sysmon, Wazuh, or backup changes and immediately before Phase 8.5.
