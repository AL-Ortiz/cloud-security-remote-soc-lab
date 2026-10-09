# EDR Investigation and Process Analysis

## 1. Project Overview

**Organization:** Northstar Financial Services (fictional)  
**Role:** Simulated Junior Cloud Security Analyst  
**Security Concepts:** Endpoint Detection and Response (EDR), process analysis, threat investigation, and containment  
**Status:** Simulated investigation; no live endpoint was accessed

This document demonstrates how a SOC analyst can use endpoint telemetry to investigate suspicious process execution, identify related activity, and recommend appropriate containment actions.

## 2. Incident Summary

**Incident ID:** NS-2026-001  
**Affected User:** Alex (`alex@northstar.com`)  
**Affected Resource:** Finance Quarterly Reports  
**Initial Assessment:** Suspected malicious document execution

The simulated timeline shows an invoice-themed document being opened, followed by Microsoft Word launching PowerShell. A script then executes, an external IP address is contacted, and sensitive financial reports are accessed.

These events warrant investigation. They do not independently prove data exfiltration or persistent remote access.

## 3. Process Execution Timeline

| Time | Observed Event | Security Significance |
|---|---|---|
| 2:47 PM | Invoice-themed email received | Potential initial delivery method |
| 2:50 PM | `Invoice_10482.docx` opened | User interaction with the suspicious file |
| 2:50 PM | `WINWORD.EXE` launches `powershell.exe` | Unusual parent-child process relationship |
| 2:52 PM | `invoice.ps1` executes | Script activity requires analysis |
| 2:55 PM | Connection to `185.44.91.12` | External communication requires investigation |
| 3:01 PM | Finance Quarterly Reports accessed | Potential sensitive-data exposure |
| 3:02 PM | SIEM alert generated | Security team receives detection |
| 3:11 PM | User denies intentionally opening the document | Supports further investigation |

The timeline is based on a fictional exercise and should be treated as simulated evidence.

## 4. Process Tree Analysis

The key process relationship is:

```text
WINWORD.EXE
└── powershell.exe
    └── invoice.ps1
```

### Why this matters

Microsoft Word normally processes documents. If it launches PowerShell unexpectedly, the analyst should determine why the process was started and what commands were executed.

PowerShell is also a legitimate administration tool, so its presence alone is not proof of malware.

### Evidence to collect

- Parent and child process names.
- Process command lines and timestamps.
- User account associated with each process.
- File paths, hashes, and signatures where available.
- Related EDR detections and alerts.
- Network connections associated with the process.
- Other processes created before and after the suspicious activity.

Preserve relevant evidence according to the organization's procedures before removing artifacts.

## 5. Investigation Questions

### Process behavior
- What exact command line was used to launch PowerShell?
- Did the script download or execute additional files?
- Were additional processes created?
- Did the script attempt to modify security settings or establish persistence?

### Network activity
- Which process initiated the connection to `185.44.91.12`?
- What destination port and protocol were used?
- Was the connection successful?
- Did other endpoints communicate with the same destination?

### Account and data access
- Was Alex's account used for any unexpected activity?
- Which financial reports were accessed?
- Were files copied, downloaded, or transmitted externally?
- Were other accounts or systems affected?

These questions remain open until supported by evidence.

## 6. Containment Recommendations

The response team should follow approved incident procedures and consider the following actions based on the evidence:

1. Isolate the affected endpoint using available EDR controls.
2. Stop confirmed malicious processes when authorized and appropriate.
3. Quarantine the suspicious document and related artifacts.
4. Preserve process, file, network, and authentication evidence.
5. Revoke active sessions and investigate potential account compromise.
6. Block confirmed malicious destinations where appropriate.
7. Search for similar process activity on other endpoints.
8. Confirm that containment has succeeded and monitor for recurrence.

Avoid disabling PowerShell organization-wide or blocking all external network traffic. Controls should target the confirmed behavior and maintain necessary business operations.

## 7. Eradication and Recovery

After the investigation establishes the scope of the incident:

- Remove confirmed malicious artifacts using approved procedures.
- Check for persistence mechanisms and additional payloads.
- Reset credentials and strengthen authentication if compromise is suspected or confirmed.
- Restore affected systems from trusted sources if required.
- Verify endpoint health and security-tool operation.
- Monitor for renewed suspicious activity.
- Document recovery approval and remaining risks.

Deleting files before preserving evidence can hinder the investigation. Recovery should not begin until the response team determines that it is appropriate.

## 8. EDR Detection Improvements

Recommended detection opportunities include:

- Office applications launching PowerShell or other scripting tools.
- Suspicious or encoded command-line arguments.
- Scripts initiating unexpected outbound network connections.
- Unusual access to sensitive files following suspicious process execution.
- Attempts to disable endpoint protection.
- Similar process chains appearing across multiple devices.

Detections should be tested against legitimate administrative workflows to reduce false positives.

## 9. Investigation Conclusion

The simulated evidence supports treating the event as a likely malicious-document incident involving suspicious script execution and external communication.

The strongest observed indicators are the unusual Word-to-PowerShell process relationship, execution of `invoice.ps1`, and subsequent access to sensitive financial reports.

The investigation must still establish what the script did, whether additional systems were affected, and whether data was transferred outside the organization. Those outcomes cannot be confirmed from the available timeline alone.

## 10. Key Takeaway

EDR investigation requires analysts to reconstruct process activity, correlate endpoint and network evidence, preserve artifacts, and recommend proportionate containment. A reliable conclusion distinguishes observed behavior from assumptions and identifies what additional evidence is needed.
