# KQL Investigation Queries for SOC Analysts

## 1. Project Overview

**Organization:** Northstar Financial Services (fictional)  
**Role:** Simulated Junior Cloud Security Analyst  
**Tool:** Kusto Query Language (KQL)  
**Environment:** Microsoft Sentinel-style simulated investigation

This document contains example KQL queries for investigating suspicious authentication activity, correlating events, and identifying potential endpoint or account compromise.

**Important:** These are example queries for portfolio practice. They have not been executed against a live Microsoft Sentinel workspace. Table names and fields must be verified against the actual data connectors and schemas in use.

## 2. Investigation Scenario

Incident NS-2026-001 involves a suspicious invoice document, unexpected PowerShell execution, external network communication, and access to sensitive financial reports.

The investigation aims to answer:

- Did the affected user experience repeated failed sign-ins?
- Were there successful sign-ins after suspicious failures?
- What endpoint activity occurred around the incident?
- Were sensitive resources accessed?
- Are there related events that require escalation?

## 3. Query 1 — Review Failed Sign-Ins

**Objective:** Identify failed sign-in attempts associated with the affected user.

```kusto
SigninLogs
| where UserPrincipalName =~ "alex@northstar.com"
| where ResultType != "0"
| project TimeGenerated, UserPrincipalName, IPAddress, AppDisplayName, ResultType, ResultDescription
| order by TimeGenerated desc
```

**Analyst notes:**

- `SigninLogs` contains Microsoft Entra sign-in events when the relevant connector is configured.
- `ResultType != "0"` filters for non-success results in the typical Entra sign-in schema.
- Review the result description, IP address, application, and time to determine whether the failures are suspicious.
- Repeated failures alone do not prove a brute-force attack; they may also result from user error or an application using outdated credentials.

## 4. Query 2 — Review Successful Sign-Ins

**Objective:** Review successful sign-ins for the affected user during the investigation.

```kusto
SigninLogs
| where UserPrincipalName =~ "alex@northstar.com"
| where ResultType == "0"
| project TimeGenerated, UserPrincipalName, IPAddress, AppDisplayName, Location, ConditionalAccessStatus
| order by TimeGenerated desc
```

**Analyst notes:**

Compare sign-in times, IP addresses, applications, and available location or Conditional Access information with the user's normal activity. An unfamiliar location or IP is a lead for investigation, not proof of compromise by itself.

## 5. Query 3 — Investigate PowerShell Activity

**Objective:** Search endpoint telemetry for PowerShell processes on a known affected device.

```kusto
DeviceProcessEvents
| where Timestamp > ago(24h)
| where DeviceName =~ "REPLACE-WITH-AFFECTED-DEVICE"
| where FileName in~ ("powershell.exe", "pwsh.exe")
| project Timestamp, DeviceName, AccountName, FileName, ProcessCommandLine, InitiatingProcessFileName
| order by Timestamp desc
```

**Analyst notes:**

- Replace the placeholder with the actual device name.
- `DeviceProcessEvents` is available in Microsoft Defender XDR advanced hunting and may be accessible through other workflows depending on the environment.
- Review the initiating process, command line, account, and timestamp.
- Office applications launching PowerShell can be suspicious, but investigate the complete process chain and business context before drawing a conclusion.

## 6. Query 4 — Search for Office Applications Launching PowerShell

**Objective:** Identify potentially suspicious parent-child process relationships.

```kusto
DeviceProcessEvents
| where Timestamp > ago(24h)
| where FileName in~ ("powershell.exe", "pwsh.exe")
| where InitiatingProcessFileName in~ ("winword.exe", "excel.exe", "powerpnt.exe")
| project Timestamp, DeviceName, AccountName, InitiatingProcessFileName, FileName, ProcessCommandLine
| order by Timestamp desc
```

**Analyst notes:**

This query looks for PowerShell processes initiated by Microsoft Office applications. The result is a detection lead, not a final determination of malicious activity. Review command-line details, file reputation, endpoint alerts, and related events.

## 7. Query 5 — Review Outbound Network Connections

**Objective:** Search available endpoint network telemetry for connections to the external IP associated with the simulated incident.

```kusto
DeviceNetworkEvents
| where Timestamp > ago(24h)
| where RemoteIP == "185.44.91.12"
| project Timestamp, DeviceName, InitiatingProcessAccountName, InitiatingProcessFileName, RemoteIP, RemotePort, Protocol
| order by Timestamp desc
```

**Analyst notes:**

Confirm that the relevant network telemetry is available and that the remote IP is represented in the expected field. Investigate the initiating process, destination, connection timing, and related alerts. A connection to an external IP does not by itself establish that the destination is malicious.

## 8. Query 6 — Review Potentially Related Activity on the Endpoint

**Objective:** Build a chronological view of recent process events on the affected device.

```kusto
DeviceProcessEvents
| where Timestamp between (ago(24h) .. now())
| where DeviceName =~ "REPLACE-WITH-AFFECTED-DEVICE"
| project Timestamp, DeviceName, AccountName, FileName, ProcessCommandLine, InitiatingProcessFileName
| order by Timestamp asc
```

**Analyst notes:**

Use the chronological output to identify relevant processes before and after the suspected execution. Correlate timestamps with authentication, network, file-access, and security-alert evidence.

## 9. Investigation Workflow

1. Establish the incident time window and identify the affected account and device.
2. Review failed and successful sign-ins.
3. Search endpoint telemetry for the suspicious document's process chain.
4. Review outbound connections and related security alerts.
5. Investigate access to sensitive files using the appropriate available audit logs.
6. Correlate the evidence into a timeline.
7. Record confirmed facts, hypotheses, and unresolved questions separately.
8. Escalate or recommend containment based on the severity and evidence.

## 10. Query Limitations

- Table availability depends on enabled data connectors, licensing, permissions, and workspace configuration.
- Field names and values can vary between products and data sources.
- The sample time windows are illustrative; use the incident's actual time range when investigating a real case.
- A query returning no results does not prove that an event did not occur. The relevant data may be unavailable, delayed, filtered, or stored elsewhere.
- Queries should be validated in an authorized environment before being used operationally.

## 11. Key Takeaway

KQL helps security analysts filter and correlate large volumes of security telemetry. Effective investigation requires more than running queries: analysts must validate the data source, interpret results in context, correlate multiple evidence sources, and clearly communicate what is known and unknown.
