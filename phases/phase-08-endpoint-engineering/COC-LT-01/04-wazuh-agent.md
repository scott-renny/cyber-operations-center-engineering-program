# COC-LT-01 Wazuh Agent

## Objective

Provide centralized endpoint visibility and validate that relevant file and configuration activity on COC-LT-01 reaches the existing Wazuh security platform.

## Implemented capabilities

- Wazuh agent installed and enrolled as COC-LT-01.
- Agent connectivity to the manager validated.
- File Integrity Monitoring configured.
- Real-time file-change monitoring validated with a controlled test file.
- Resulting event visibility confirmed in Wazuh.
- Security Configuration Assessment results reviewed.
- MITRE ATT&CK context available for applicable alerts.

## Validation flow

```text
Controlled test file
        |
Create or modify
        |
Wazuh real-time FIM
        |
Manager ingestion
        |
Visible event and applicable MITRE context
```

## Operational checks

- Confirm the COC-LT-01 agent is active after reboot and network changes.
- Investigate unexpected FIM additions, modifications, and deletions.
- Review Security Configuration Assessment findings as prioritized hardening input, not as automatic proof of compromise.
- Re-run the controlled FIM test after agent upgrades or material configuration changes.

## Evidence handling

The public repository records the test method and outcome only. Raw alerts, host identifiers, manager addresses, and screenshots that disclose environment details remain outside the public record.
