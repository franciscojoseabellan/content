---

## Cortex XDR Lite - Incident Handling

The **Cortex XDR Lite - Incident Handling** playbook is triggered by fetching a Palo Alto Networks Cortex XDR incident and executes the following:

**Analysis:**
- Enriches all the indicators from XDR incidents and alerts, providing additional context and information about these indicators.

**Investigation:**
- Checks for related XDR alerts to the user and the endpoint by Mitre tactics to identify malicious activity.
- Checks for specific arguments for malicious usage from the command line.

**Verdict:**
- Determines the incident's verdict by considering indicator enrichment results, user and host risk levels, command line analysis, and the number of related XDR alerts (medium severity or higher) to the user and the endpoint by Mitre tactics.

**Verdict Handling:**
- Handles malicious incidents by initiating appropriate response actions, including blocking malicious indicators, isolating endpoints, and disabling user accounts.

---

## Dependencies

This playbook uses the following sub-playbooks, integrations, and scripts.

### Sub-playbooks

* Cortex XDR - Get entity alerts by MITRE tactics
* Command-Line Analysis
* Block Indicators - Generic v3
* Cortex XDR - Isolate Endpoint
* Entity Enrichment - Generic v3

### Integrations

* CortexXDRIR
* Cortex XDR - IR

### Scripts

* Set
* SetAndHandleEmpty

### Commands

* xdr-update-incident
* xdr-get-incident-extra-data

## Playbook Inputs

---

| **Name** | **Description** | **Default Value** | **Required** |
| --- | --- | --- | --- |
| incident_id | Incident ID. | incident.xdrincidentid | Optional |
| EndpointID | XDR endpoint ID. | PaloAltoNetworksXDR.Incident.alerts.endpoint_id | Optional |
| Hostname | Hostname. | PaloAltoNetworksXDR.Incident.alerts.host_name | Optional |
| Username | Username. | PaloAltoNetworksXDR.Incident.alerts.user_name | Optional |
| AutoIsolateEndpoint | Whether to isolate the endpoint automatically. | False | Optional |
| AutoBlockIndicators | Possible values: True/False.  Default: True.<br/>Should the given indicators be automatically blocked, or should the user be given the option to choose?<br/><br/>If set to False - no prompt will appear, and all provided indicators will be blocked automatically.<br/>If set to True - the user will be prompted to select which indicators to block. | False | Optional |
| UserVerification | Possible values: True/False.  Default: False.<br/>Whether to provide user verification for blocking IPs. <br/><br/>False - No prompt will be displayed to the user.<br/>True - The server will ask the user for blocking verification and will display the blocking list. | False | Optional |
| XDRRelatedAlertsThreshold | This is the minimum threshold for XDR-related alerts of medium severity or higher, based on MITRE tactics used to identify malicious activity on the endpoint and by the user.<br/>Example: If this input is set to '5' and it detects '6' XDR-related alerts, it will classify this check as indicating malicious activity.<br/>The default value is '5'. | 5 | Optional |
| InternalRange | This input is used in the "Entity Enrichment - Generic v3" playbook.<br/>A list of internal IP ranges to check IP addresses against. The list should be provided in CIDR notation, separated by commas. An example of a list of ranges is: "172.16.0.0/12,10.0.0.0/8,192.168.0.0/16" \(without quotes\). If a list is not provided, uses the default list provided in the IsIPInRanges script \(the known IPv4 private address ranges\). | 172.16.0.0/12,10.0.0.0/8,192.168.0.0/16 | Optional |
| XDRDomain | XDR instance domain. | incident.xdrurl | Optional |

## Playbook Outputs

---
There are no outputs for this playbook.

## Playbook Image

---

![Cortex XDR Lite - Incident Handling](../doc_files/Cortex_XDR_Lite_-_Incident_Handling.png)
