# MITRE ATT&CK Mapping and Detection Opportunities

## 1. Project Overview

**Organization:** Northstar Financial Services (fictional)  
**Incident ID:** NS-2026-001  
**Role:** Simulated Junior Cloud Security Analyst  
**Framework:** MITRE ATT&CK Enterprise  
**Status:** Simulated analysis; no live environment was investigated

This document maps observed behaviors from a simulated security incident to relevant MITRE ATT&CK techniques. The goal is to organize investigation findings, identify detection opportunities, and communicate potential attacker behavior consistently.

A technique is included only when the simulated evidence supports a reasonable connection. A mapping is an investigative hypothesis, not proof that an attacker used a particular technique.

## 2. Incident Summary

The simulated incident involves an invoice-themed email, a suspicious Word document, PowerShell execution, a script named `invoice.ps1`, an outbound connection to `185.44.91.12`, and subsequent access to Finance Quarterly Reports.

The available timeline supports investigating a potentially malicious document and suspicious script activity. It does not establish that credentials were stolen, persistence was created, or data was exfiltrated.

## 3. ATT&CK Technique Mapping

| Observed Behavior | Potential ATT&CK Technique | ID | Confidence and Rationale |
|---|---|---|---|
| Invoice-themed email delivers a suspicious document | Phishing: Spearphishing Attachment | T1566.001 | Plausible, but email contents and delivery evidence should be reviewed to confirm the attachment was the delivery method |
| Word launches PowerShell | Command and Scripting Interpreter: PowerShell | T1059.001 | Strong behavioral match based on the simulated process timeline |
| Script executes after the document opens | User Execution: Malicious File | T1204.002 | Plausible if the file is confirmed malicious and user execution caused the activity |
| Script communicates with an external IP | Application Layer Protocol or another network technique may apply | To be determined | Insufficient protocol and traffic details to select a specific technique confidently |
| Finance reports are accessed | Collection or other data-access techniques may apply | To be determined | Access alone does not establish collection or exfiltration |

Technique selection should be checked against the current MITRE ATT&CK Enterprise knowledge base before being used in a real investigation.

## 4. Evidence Required to Improve Confidence

### Phishing attachment
- Original email and attachment.
- Sender and message headers.
- File hash and file reputation.
- Evidence showing how the document was delivered and opened.

### PowerShell execution
- Process creation events.
- Full command line and parent-child process relationship.
- Script contents and hash.
- Related endpoint alerts and any downloaded files.

### External communication
- Destination port and protocol.
- Network connection logs.
- Process associated with the connection.
- Relevant DNS, proxy, firewall, or other network records.

### Financial report access
- File-access audit logs.
- Identity and device associated with each access.
- Evidence of downloads, copying, or transfers.
- Relevant data-loss prevention or cloud audit alerts.

## 5. Detection Opportunities

| Detection Opportunity | Data Source | Suggested Analyst Action |
|---|---|---|
| Office application launches PowerShell | EDR process telemetry | Review the process tree, command line, and document involved |
| Suspicious script execution | EDR and script-related logs, when available | Inspect the script and associated process activity |
| Unexpected outbound communication | Endpoint and network logs | Identify the initiating process and investigate the destination |
| Unusual access to sensitive reports | File and cloud audit logs | Confirm the user, device, access pattern, and any data transfer |
| Related behavior across multiple endpoints | SIEM and EDR | Search for matching processes, file hashes, destinations, and timestamps |

These are detection ideas, not claims that the controls are already configured or tested.

## 6. Recommended Investigation Sequence

1. Validate the suspicious email and document.
2. Reconstruct the process chain from Word to PowerShell and the script.
3. Determine what the script executed and whether it created or downloaded additional files.
4. Correlate the external connection with endpoint and network telemetry.
5. Review access to the financial reports and investigate potential data exposure.
6. Search for similar activity across other accounts and devices.
7. Record the evidence supporting each ATT&CK mapping.
8. Update the incident assessment as new evidence becomes available.

## 7. Limitations

- This is a simulated scenario, not a live threat investigation.
- The incident timeline does not provide complete email headers, script contents, network packet data, or file-access audit records.
- A suspicious behavior does not automatically establish malicious intent.
- Technique mappings should be updated when additional evidence changes the assessment.
- No production detection rules were deployed or validated as part of this project.

## 8. Key Takeaway

MITRE ATT&CK helps security analysts describe observed behavior, communicate investigation findings, and identify opportunities to improve detection coverage. Reliable mapping requires evidence, appropriate confidence levels, and a clear distinction between observed facts and unconfirmed hypotheses.
