# Infrastructure Security Enhancement

Enhanced infrastructure security through Wazuh monitoring and Trivy vulnerability scanning, supported by Zabbix infrastructure monitoring and alerting and Grafana dashboards.

## Operational need

Legacy runtimes and container dependencies require ongoing security review. Security events, infrastructure outages, and image vulnerabilities each need a clear operational owner and response process.

## My contribution

- Implemented Wazuh security monitoring to improve visibility into security events.
- Established Trivy container-image vulnerability scanning to identify known findings and support remediation.
- Centralized infrastructure monitoring and operational alerting through Zabbix.
- Used Grafana dashboards to visualize operational metrics.
- Modernized legacy IoT workloads on Ubuntu and Docker, upgrading PHP and Apache while preserving historical records and data logger connectivity.
- Validated application behavior and prepared backups and rollback steps before runtime changes.

## Tool responsibilities

| Capability | Tool or practice |
| --- | --- |
| Security-event visibility | Wazuh |
| Container-image vulnerability assessment | Trivy |
| Infrastructure health and operational alerting | Zabbix |
| Operational visualization | Grafana |
| Vulnerability remediation | Runtime updates, compatibility checks and rollback preparation |

These capabilities complement one another. Grafana is used for dashboards, not alerting. This case study does not assert that Wazuh or Trivy findings are automatically forwarded to Zabbix.

## Remediation approach

1. Identify the affected workload and its deployed runtime or container image.
2. Review relevant vulnerability findings and prioritize remediation.
3. Prepare and check the replacement image before changing the running service.
4. Validate authentication, application functions and monitoring after deployment.
5. Retain a rollback path and repeat assessment as new findings become available.

A scan result describes a specific image at a point in time. Remediation of reported findings is not a guarantee that a workload has no vulnerabilities.

## Business value

- Clearer security and infrastructure visibility for operational decisions.
- A practical path for addressing known vulnerabilities in legacy workloads.
- Continued service connectivity during modernization.
- A maintainable foundation for ongoing security monitoring and patch management.

## Next phase

AI-assisted summaries and notification rules can later use approved operational information through the Internal AI Assistant and Notification Gateway. This integration remains planned.

## Security and confidentiality

This portfolio case study omits production endpoints, credentials, internal addresses, raw security logs, sensitive scan reports and proprietary source code.

[Back to portfolio](../README.md)
