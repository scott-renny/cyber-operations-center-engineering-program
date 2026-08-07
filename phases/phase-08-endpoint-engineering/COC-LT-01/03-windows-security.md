# COC-LT-01 Windows Security

## Platform baseline

| Control | Phase 8 state | Security purpose |
|---|---|---|
| Windows 11 Home | Installed platform | Supported endpoint operating system |
| TPM 2.0 | Verified | Hardware-backed key protection and Windows Hello |
| Secure Boot | Verified | Boot-chain integrity |
| Windows Hello PIN | Configured | Device-bound local authentication |
| Microsoft Defender | Verified | Anti-malware and endpoint protection |
| Tamper Protection | Enabled | Resistance to unauthorized security-setting changes |
| Smart App Control | Active | Application reputation and execution protection |
| Controlled Folder Access | Enabled | Protection of important files against unauthorized modification |
| Windows Firewall | Reviewed | Host-level network filtering |

## Controlled Folder Access operations

A blocked application must be investigated before it is allowed. Approval should be limited to the exact trusted executable, and unexpected blocks should be correlated with Wazuh and Defender telemetry.

## Windows 11 Home constraint

The Home edition does not provide the complete centrally managed enterprise control set expected from Pro, Enterprise, Intune, or Active Directory-backed policy. Phase 8 does not claim those capabilities. The accepted compensating baseline combines native protection, VPN-based access restrictions, a hardened browser, Wazuh monitoring, least-privilege operation, and repeatable checks.

## Maintenance

Revalidate after major Windows upgrades, security-control state changes, firmware changes, Wazuh loss of connectivity, or unexplained Controlled Folder Access events.
