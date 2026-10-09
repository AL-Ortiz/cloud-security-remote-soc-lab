# Security Incident Report

## 1. Incident Details

| Field | Details |
|---|---|
| Organization | Northstar Financial Services (fictional) |
| Incident ID | NS-2026-001 |
| Incident Type | Suspected malicious document execution and possible account compromise |
| Severity | High — provisional assessment |
| Affected User | Alex (`alex@northstar.com`) |
| Affected Resource | Finance Quarterly Reports |
| Detection Source | Simulated SIEM alert |
| Status | Investigation and remediation required |
| Environment | Simulated Azure, Microsoft Entra ID, Microsoft 365, SIEM, and endpoint security tools |
| Report Type | Portfolio exercise — no live incident investigated |

## 2. Executive Summary

A simulated invoice-themed email was followed by a Word document opening, PowerShell execution, script activity, communication with an external IP address, and access to sensitive financial reports.

A SIEM alert was generated at 3:02 PM. At 3:11 PM, the affected user denied intentionally opening the suspicious document.

The sequence indicates a likely security incident involving suspicious document and script execution. The incident has potential implications for endpoint security, identity security, and confidential financial information.

The available evidence does not confirm data exfiltration, persistent remote access, or the full scope of potential compromise. Additional investigation is required to establish the actual impact.

## 3. Incident Timeline

| Time | Event |
|---|---|
| 2:47 PM | Invoice-themed email received |
| 2:50 PM | `Invoice_10482.docx` opened |
| 2:50 PM | `WINWORD.EXE` launches `powershell.exe` |
| 2:52 PM | PowerShell executes `invoice.ps1` |
| 2:55 PM | Script contacts `185.44.91.12` |
| 3:01 PM | Finance Quarterly Reports accessed |
| 3:02 PM | SIEM alert generated |
| 3:11 PM | User denies intentionally opening the document |

The times are from the simulated scenario. The timezone and raw event records were not provided.

## 4. Findings

### Finding 1: Suspicious document execution

The user opened an invoice-themed Word document shortly before Word launched PowerShell.

**Assessment:** The process relationship is suspicious and warrants investigation. The document's contents, origin, and file reputation must be examined to establish whether it was malicious.

### Finding 2: Script execution

PowerShell executed a script named `invoice.ps1`.

**Assessment:** Script behavior must be analyzed to determine whether it downloaded additional files, modified system settings, accessed credentials, or performed other unauthorized actions.

### Finding 3: External network communication

The script contacted `185.44.91.12`.

**Assessment:** The destination and communication require validation using available endpoint, network, and threat-intelligence evidence. An external connection alone does not establish malicious activity.

### Finding 4: Access to sensitive financial reports

Finance Quarterly Reports were accessed after the suspicious process activity.

**Assessment:** Investigators should determine which files were accessed, whether the access was authorized, and whether any data was copied or transferred externally.

## 5. Root Cause Assessment

**Provisional assessment:** The incident likely began when an invoice-themed document was opened, followed by suspicious PowerShell and script execution.

This is a working hypothesis based on the simulated sequence. The original email, document, script contents, and endpoint records would be needed to confirm the initial delivery method and the script's behavior.

## 6. Containment Recommendations

The following actions are recommended for the simulated incident:

1. Isolate the affected endpoint using approved endpoint security controls.
2. Preserve relevant email, endpoint, authentication, network, and file-access evidence.
3. Revoke active sessions if identity compromise is suspected.
4. Quarantine the suspicious document and contain confirmed malicious artifacts.
5. Investigate and block the external destination if evidence warrants blocking.
6. Review access to Finance Quarterly Reports and determine whether other resources were affected.
7. Search for similar activity across other endpoints and accounts.
8. Reset credentials and strengthen authentication if compromise is suspected or confirmed.

These are recommendations for the exercise, not claims that live systems were changed.

## 7. Eradication and Recovery Plan

After collecting and reviewing relevant evidence:

- Remove confirmed malicious artifacts using approved procedures.
- Investigate possible persistence, additional payloads, and lateral movement.
- Validate the endpoint's security status before returning it to normal use.
- Reset affected credentials and revoke sessions when appropriate.
- Restore systems from trusted sources if necessary.
- Confirm that required security controls are functioning.
- Monitor for recurring suspicious activity.
- Document recovery approval and remaining risks.

Evidence should be preserved before deleting artifacts whenever feasible.

## 8. MITRE ATT&CK Considerations

Potential technique mappings include:

- **T1059.001 — PowerShell:** Supported as an investigative mapping by the reported PowerShell execution.
- **T1566.001 — Spearphishing Attachment:** A possible mapping if evidence confirms that the email attachment was used to deliver the malicious file.
- **T1204.002 — Malicious File:** A possible mapping if the document is confirmed malicious and user execution caused the activity.

These mappings are provisional and should be validated against the evidence and the current MITRE ATT&CK framework. Credential theft, persistence, lateral movement, and exfiltration are not established by the available scenario details.

## 9. Preventive Recommendations

### Identity and access
- Require multifactor authentication and appropriate Conditional Access policies.
- Apply least privilege and review access to sensitive financial resources.
- Monitor unusual sign-ins, session activity, and privilege changes.

### Email and endpoint security
- Improve detection and quarantine of suspicious attachments.
- Detect unusual Office-to-PowerShell process relationships.
- Monitor script execution and suspicious child processes.
- Keep endpoint protection and security monitoring enabled and updated.

### Network and data protection
- Review outbound connections associated with suspicious processes.
- Apply network segmentation and restrict unnecessary communication.
- Monitor sensitive-file access and investigate unusual download or transfer patterns.

### Security awareness
- Provide practical phishing-awareness training.
- Establish a clear process for reporting suspicious messages.
- Reinforce prompt reporting without discouraging employees from raising concerns.

## 10. Outstanding Questions

The following questions remain unresolved:

- What did `invoice.ps1` actually do?
- Was the external IP malicious?
- Were credentials or authentication tokens compromised?
- Which financial reports were accessed, and was any data transferred externally?
- Did the activity affect other accounts or devices?
- Was persistence established?
- Were containment and recovery actions effective?

## 11. Final Assessment

The simulated evidence supports treating this as a likely security incident involving suspicious document execution, PowerShell activity, external communication, and access to sensitive financial reports.

The appropriate response is to preserve evidence, contain verified risks, investigate the full scope, and document recovery and lessons learned. Final impact and closure decisions should depend on additional evidence.

## 12. Portfolio Disclaimer

This report was created as a cybersecurity portfolio exercise using a fictional organization and simulated events. No production environment was accessed, no live incident was investigated, and no real containment or remediation actions were performed.
