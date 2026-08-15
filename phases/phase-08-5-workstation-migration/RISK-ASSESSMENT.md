# Phase 8.5 Linux Mint Migration Risk Assessment

| Risk | Control | Stop condition |
|---|---|---|
| Wrong disk erased | Positively identify firmware, installer, and destination storage | Any uncertainty about the target disk |
| Linux Mint image tampered with | Verify the image hash against the checksum obtained from official Linux Mint sources | Checksum failure |
| Data omitted from migration | Complete application/data inventory and retain approved Restic source | Required data category not represented |
| Malware restored | Exclude warning-tagged snapshots, restore selectively, rescan | Any malware detection |
| Windows-only workflow unavailable | Record and test replacement, VM, exception, or retirement | Required workflow has no accepted disposition |
| Encryption inaccessible | Test LUKS unlock and protected recovery material before migration acceptance | Recovery path untested or failed |
| Secure Boot incompatibility | Test all required hardware and signed drivers before acceptance | Required device needs Secure Boot disabled without approved exception |
| AppArmor weakened for compatibility | Resolve profiles rather than disabling protection | Proposed permanent disabled state |
| Firewall exposure | Review UFW rules and listening sockets | Unexpected inbound service |
| Secrets copied insecurely | Restore minimum secrets, restrict permissions, rotate where practical | Secret ownership or provenance uncertain |
| Telemetry gap | Enroll supported Wazuh agent and generate controlled evidence | No central event receipt |
| Backup gap after cutover | Build and restore-test Linux Mint backup before retirement | No successful Linux Mint restore |
| Premature Windows retirement | Require signed-off application, data, monitoring, and backup gates | Any incomplete acceptance criterion |

## Residual risk

Linux application behavior, proprietary hardware drivers, Windows-only software, and user-workflow differences may still require controlled exceptions. Exceptions must be narrow, documented, tested, and reviewed after material Linux Mint or hardware changes.
