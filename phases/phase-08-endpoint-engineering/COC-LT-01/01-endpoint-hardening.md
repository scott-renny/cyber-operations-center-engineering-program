# COC-LT-01 Endpoint Hardening

## Objective

Reduce the likelihood and impact of endpoint compromise while preserving practical use on both trusted and untrusted networks.

## Implemented baseline

- Verified TPM 2.0 readiness.
- Verified Secure Boot.
- Configured Windows Hello PIN for TPM-backed local authentication.
- Verified Microsoft Defender protections.
- Enabled Tamper Protection.
- Confirmed Smart App Control was active.
- Enabled Controlled Folder Access.
- Reviewed Windows Firewall state.
- Deployed and validated the Wazuh agent.
- Hardened Firefox and installed the approved security extensions.
- Implemented WireGuard profiles for trusted and untrusted network use.
- Added hardware-backed authentication to Microsoft and Bitwarden.

## Defense-in-depth model

```text
Verified boot and TPM
        |
Windows authentication and Defender controls
        |
Host firewall and Controlled Folder Access
        |
WireGuard policy based on network trust
        |
Wazuh monitoring and file-integrity telemetry
        |
Hardened browser and hardware-backed account authentication
```

## Operational rules

- Use the full-tunnel profile on untrusted networks.
- Do not disable the kill switch to work around connectivity without documenting and diagnosing the failure.
- Review Controlled Folder Access blocks before allowing an application.
- Keep recovery methods available until redundant hardware-key enrollment is completed and tested.
- Treat Wazuh silence as a monitoring fault, not proof of a healthy endpoint.

## Known limitation

Windows 11 Home does not expose the full centrally managed enterprise policy surface. The resulting gap is accepted for this phase and reduced through layered native controls, network restrictions, monitoring, and documented validation.
