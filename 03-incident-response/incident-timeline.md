# Security Incident Timeline

## 1. Incident Information

- **Organization:** Northstar Financial Services (fictional)
- **Incident ID:** NS-2026-001
- **Incident Type:** Suspected malicious document execution and possible account compromise
- **Affected User:** Alex (`alex@northstar.com`)
- **Affected Resource:** Finance Quarterly Reports
- **Environment:** Simulated Azure, Microsoft Entra ID, Microsoft 365, SIEM, and endpoint security tools
- **Status:** Containment actions proposed or recorded in the simulated exercise; further investigation required
- **Evidence Type:** Fictional scenario data created for portfolio practice

## 2. Executive Summary

A simulated invoice-themed email was followed by the opening of a Word document, PowerShell execution, script activity, outbound communication with an external IP address, and access to sensitive financial reports.

A SIEM alert was generated after the suspicious activity began. The user subsequently denied intentionally opening the document.

The sequence warrants investigation as a likely security incident. The available evidence does not confirm data exfiltration, persistent remote access, or the full scope of potential compromise.

## 3. Event Timeline

| Time | Event | Security Significance |
|---|---|---|
| 2:47 PM | Alex receives an invoice-themed email | Potential delivery of a malicious attachment |
| 2:50 PM | `Invoice_10482.docx` is opened | Suspicious document interaction |
| 2:50 PM | `WINWORD.EXE` launches `powershell.exe` | Unusual process relationship requiring investigation |
| 2:52 PM | PowerShell executes `invoice.ps1` | Script execution may indicate malicious activity |
| 2:55 PM | Script contacts `185.44.91.12` | External communication requires validation |
| 3:01 PM | Finance Quarterly Reports are accessed | Potential exposure of sensitive information |
| 3:02 PM | SIEM generates an alert | Detection and escalation opportunity |
| 3:11 PM | Alex denies intentionally opening the document | User statement supports continued investigation |

**Timestamp limitation:** The scenario does not specify a timezone or provide raw event logs. The times above are reproduced from the simulated exercise and should not be treated as independently verified timestamps.

## 4. Initial Assessment

### Observed facts within the scenario

- An invoice-themed email was received.
- A Word document was opened.
- Word launched PowerShell.
- A script executed.
- An external IP address was contacted.
- Finance Quarterly Reports were accessed.
- A SIEM alert was generated.
- The user denied intentionally opening the document.

### Analyst assessment

The combination of suspicious document execution, script activity, external communication, and access to sensitive reports supports classifying this as a suspected security incident with high potential impact.

The available information does not establish:

- The exact behavior of the script.
- Whether the external destination was malicious.
- Whether credentials were stolen.
- Whether data was copied or transmitted outside the organization.
- Whether persistence or lateral movement occurred.
- Whether other users or devices were affected.

## 5. Response Actions and Evidence Handling

The following actions are recommended for this simulated incident. They should not be interpreted as proof that changes were performed in a live environment.

| Priority | Action | Purpose |
|---|---|---|
| Immediate | Isolate the affected endpoint when appropriate | Limit potentially malicious activity |
| Immediate | Preserve relevant endpoint, email, identity, and network evidence | Support investigation and incident reconstruction |
| Immediate | Revoke active sessions if account compromise is suspected | Reduce the risk of continued unauthorized access |
| High | Quarantine the suspicious document and contain confirmed malicious artifacts | Prevent further execution |
| High | Investigate the external IP and associated process | Determine the nature of the communication |
| High | Review access to Finance Quarterly Reports | Establish potential data exposure |
| High | Search for similar activity across other accounts and devices | Determine the incident scope |
| Follow-up | Reset credentials and strengthen authentication when warranted | Address potential identity compromise |
| Follow-up | Validate recovery and monitor for recurrence | Confirm that containment remains effective |

## 6. Evidence Preservation

Relevant evidence should be preserved in accordance with organizational procedures, including:

- Original email and attachment, with available metadata.
- File hashes, paths, and security-tool findings.
- Process trees and command-line records.
- Authentication and session logs.
- Endpoint network events and relevant firewall or proxy logs.
- File-access audit records.
- SIEM alerts and analyst notes.
- Records of containment actions and approvals.

Evidence collection should maintain timestamps, source information, and appropriate access controls. Investigators should preserve relevant artifacts before deleting or modifying them whenever feasible.

## 7. Next Investigation Steps

1. Analyze the document and script safely using approved procedures.
2. Determine the process responsible for the external connection.
3. Validate the destination using available network and threat-intelligence evidence.
4. Identify which financial reports were accessed and whether data was transferred.
5. Review authentication events and session activity for signs of account compromise.
6. Search for persistence, additional payloads, and activity on other endpoints.
7. Update the incident classification and impact assessment as evidence develops.
8. Document recovery approval, outstanding risks, and final findings.

## 8. Incident Status

**Assessment:** Suspected security incident requiring investigation.

**Containment:** Recommended actions are documented for the simulated exercise; no live containment was performed as part of this portfolio.

**Investigation:** Open questions remain about script behavior, external communication, potential data exposure, and incident scope.

**Closure criteria:** Close the incident only after the response team has assessed scope and impact, completed necessary remediation and recovery checks, documented remaining risks, and obtained required approvals.

## 9. Key Takeaway

A reliable incident timeline gives the SOC a chronological view of suspicious activity, supports evidence-based decisions, and helps teams coordinate response actions. Analysts should clearly distinguish observed events, interpretations, recommended actions, and unresolved questions.
