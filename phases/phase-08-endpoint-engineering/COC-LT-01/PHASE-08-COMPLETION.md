# Phase 8 Completion Report — COC-LT-01

> **Status:** Complete  
> **Completion date:** 2026-08-07  
> **Asset:** COC-LT-01  
> **Scope:** Laptop endpoint work only

## Executive summary

Phase 8 established a validated endpoint-security baseline for COC-LT-01. The completed work combines hardware-backed platform trust, native Windows protections, VPN policy, centralized Wazuh monitoring, browser hardening, phishing-resistant authentication for two critical services, and a smaller public attack surface.

## Objectives achieved

- Verify the platform trust foundation.
- Apply practical Windows 11 Home protections.
- Provide separate VPN behavior for trusted and untrusted networks.
- Validate endpoint file-integrity and configuration visibility in Wazuh.
- Reduce browser and credential risk.
- Protect Microsoft and Bitwarden access with a hardware security key.
- Require VPN access for remote administration.
- Record limitations, evidence boundaries, and deferred work accurately.

## Security outcome

COC-LT-01 now uses layered controls rather than relying on any single product. The untrusted-network profile provides full-tunnel routing, controlled DNS, and a kill switch. The server-side exposure change removes unnecessary public web forwarding. Wazuh provides independent monitoring, and hardware-key authentication reduces phishing risk for completed enrollments.

## Lessons learned

- Passkey labels do not prove storage location; an independent sign-in test must require the physical key.
- A hardware-key PIN is distinct from the Windows Hello PIN.
- Enrollment should be followed immediately by a private-session authentication test.
- Recovery methods should remain until redundant factors are enrolled and tested.
- Windows 11 Home limitations require explicit compensating controls and honest documentation.
- A VPN kill switch is valuable only when its failure behavior is tested.
- Monitoring must be tested with a controlled event rather than inferred from agent installation.

## Known limitations and residual risk

- Enterprise policy enforcement available in higher Windows editions is not present.
- Hardware-key enrollment is complete only for Microsoft and Bitwarden.
- The secondary hardware key has not been enrolled.
- Screenshots and raw output have not been published.
- Sysmon, custom detections, endpoint management, and later identity work remain outside this phase.

## Completion decision

The documented COC-LT-01 Phase 8 baseline is complete. No claim is made for other endpoints or deferred controls. Future changes should preserve the VPN-only administration boundary and repeat the validation suite after material platform, networking, or monitoring changes.
