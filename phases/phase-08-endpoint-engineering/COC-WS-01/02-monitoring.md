# COC-WS-01 Monitoring

## Wazuh

The Windows agent was installed at the same release level as the manager and enrolled under the temporary public-safe name `win10-desktop`. The service starts automatically and uses the dedicated agent channel.

Enrollment was opened only for the registration window. After the key was issued and the agent became active, the enrollment service and its firewall access were disabled. Normal agent telemetry continues on the separate agent-traffic channel. The temporary identity will be revoked when the workstation is retired.

## Sysmon

Microsoft Sysinternals Sysmon was installed from a signed distribution. The configuration passed XML and Sysmon schema validation. Its service and driver start automatically.

The Wazuh agent subscribes to the Microsoft-Windows-Sysmon/Operational channel. Controlled process activity confirmed local event creation, event-channel collection, centralized receipt under the workstation agent, and rule processing with ATT&CK context.

## Operational considerations

Sysmon can generate high event volume. Configuration changes should be versioned, validated locally, and reviewed for Wazuh noise. The current configuration is an initial telemetry baseline, not a finished detection-engineering product.

## Evidence boundary

Manager addresses, enrollment material, agent keys, local account names, and raw event payloads are retained privately.
