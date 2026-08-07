# COC-LT-01 Phase 8 Validation Results

> **Result:** Passed for the controls listed below  
> **Evidence:** Sanitized narrative; sensitive raw output excluded

| Area | Method | Result |
|---|---|---|
| Secure Boot | Windows security-state review | Verified enabled |
| TPM | Windows TPM status review | TPM 2.0 verified |
| Windows Hello | Local sign-in configuration review | PIN configured |
| Defender | Windows Security review | Protection verified |
| Tamper Protection | Windows Security review | Enabled |
| Smart App Control | Windows Security review | Active |
| Controlled Folder Access | Ransomware-protection review | Enabled |
| Windows Firewall | Firewall status review | Reviewed and active |
| WireGuard peer | `wg show` on endpoint infrastructure | Peer state verified |
| Split tunnel | Approved private-resource connectivity | Passed |
| Full tunnel | External route/egress test | Passed |
| VPN DNS | Name-resolution test while tunneled | Passed |
| Kill switch | Tunnel-unavailable traffic test | Passed |
| Wazuh agent | Manager agent-state review | Connected |
| Wazuh FIM | Controlled test-file activity | Event detected |
| Wazuh SCA | Configuration-assessment review | Results available |
| Browser | Firefox settings and extension review | Baseline applied |
| Microsoft identity | Private-session hardware-key sign-in | Passed |
| Bitwarden identity | Hardware-key enrollment | Completed |
| Public exposure | `ufw status` and reachability review | HTTP/HTTPS removed; WireGuard retained |

## Interpretation

These results establish the Phase 8 baseline at the time of testing. They do not guarantee future state. Material updates, security-control changes, VPN changes, or monitoring failures require revalidation.

## Deferred evidence

Public screenshots and raw outputs were not added because they may disclose account details, addresses, identifiers, or security configuration. Sanitized evidence may be added later under repository evidence-handling rules without changing the completion claims.
