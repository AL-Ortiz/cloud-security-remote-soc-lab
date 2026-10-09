# SOC Alert Triage and Investigation

## 1. Project Overview

**Organization:** Northstar Financial Services (fictional)  
**Role:** Simulated Junior Cloud Security Analyst  
**Environment:** Simulated Azure, Microsoft Entra ID, SIEM, and endpoint security tools  
**Status:** Documentation-based exercise; no live security environment was deployed

This document describes a structured approach to reviewing security alerts, determining their priority, gathering supporting evidence, and recommending appropriate next steps.

## 2. Alert Triage Process

When a new alert arrives, the analyst should:

1. **Validate the alert:** Review the alert details, timestamps, affected user or device, and detection logic.
2. **Assess severity:** Consider the sensitivity of the affected resource, potential business impact, and evidence of active compromise.
3. **Gather evidence:** Correlate authentication logs, endpoint activity, network events, and file-access records where available.
4. **Determine confidence:** Assess whether the evidence supports a true positive, false positive, or unresolved finding.
5. **Contain when justified:** Follow the incident response process and authorization requirements to limit further harm.
6. **Document and escalate:** Record findings, actions, outstanding questions, and the next steps for the responsible team.

A single alert should not automatically be treated as proof of compromise. Analysts should evaluate the surrounding evidence and follow organizational procedures.

## 3. Simulated Alert Scenario

**Incident ID:** NS-2026-001  
**Alert Type:** Suspicious Office-to-PowerShell execution  
**Affected User:** Alex (`alex@northstar.com`)  
**Affected Resource:** Finance Quarterly Reports  
**Initial Priority:** High, pending investigation

### Observed Activity

| Time | Event |
|---|---|
| 2:47 PM | Alex receives an invoice-themed email |
| 2:50 PM | `Invoice_10482.docx` is opened |
| 2:50 PM | `WINWORD.EXE` launches `powershell.exe` |
| 2:52 PM | PowerShell executes `invoice.ps1` |
| 2:55 PM | The script communicates with `185.44.91.12` |
| 3:01 PM | Finance Quarterly Reports are accessed |
| 3:02 PM | A SIEM alert is generated |
| 3:11 PM | Alex denies intentionally opening the suspicious document |

These events are simulated for portfolio practice and do not represent a real incident.

## 4. Initial Analysis

### Why the activity is suspicious

- A document-processing application launches PowerShell, which can indicate an attempt to execute commands outside normal document functionality.
- A script runs shortly after the document is opened.
- The script communicates with an external IP address that requires investigation.
- Sensitive financial reports are accessed during the same sequence of activity.
- The user denies intentionally opening the suspicious document.

Together, these events provide stronger evidence than any one event in isolation.

### Initial Assessment

**Classification:** Suspected security incident; likely true positive for suspicious activity.

The evidence supports investigating a potentially malicious document and unauthorized script execution. The available facts do not independently prove that data was exfiltrated or that persistent remote access was established.

## 5. Investigation Questions

The analyst should seek answers to the following:

- Was the email sender legitimate, spoofed, or compromised?
- What did `invoice.ps1` actually execute?
- Was the external IP address contacted by other devices?
- Which files were accessed, and was any data downloaded, copied, or transferred externally?
- Were credentials, authentication tokens, or additional accounts compromised?
- Did the endpoint show signs of persistence or further execution?
- Have similar alerts occurred elsewhere in the environment?

Unknowns should remain explicitly documented until supporting evidence is available.

## 6. Recommended Response

Actions should follow the organization's incident response procedures and be coordinated with authorized responders.

1. Isolate the affected endpoint when appropriate.
2. Revoke active sessions and investigate the user's identity activity.
3. Preserve relevant email, endpoint, authentication, network, and file-access evidence.
4. Quarantine the suspicious document and safely contain the script or related artifacts.
5. Block the external IP address if investigation confirms that blocking is warranted.
6. Review access to sensitive financial reports and investigate possible data exposure.
7. Reset credentials and strengthen authentication if compromise is suspected or confirmed.
8. Monitor for related activity and document the outcome of each action.

Evidence should be preserved before deleting files or making changes that could interfere with investigation.

## 7. True Positive vs. False Positive

**True positive:** The alert identifies genuinely suspicious or malicious activity. In this scenario, the observed execution chain justifies treating the activity as a likely security incident.

**False positive:** The detection identifies activity that is ultimately verified as benign, such as an approved administrative script that matches the detection logic.

**Inconclusive:** There is not enough evidence to determine whether the activity was malicious. The analyst should collect additional evidence or escalate rather than assume either outcome.

## 8. Escalation Criteria

Escalate promptly when evidence suggests:

- Unauthorized access to sensitive financial information.
- Execution of an untrusted script or potentially malicious payload.
- Compromised credentials or authentication sessions.
- Similar activity affecting multiple users or devices.
- Possible data exfiltration, persistence, or continued attacker activity.

High-impact activity should be escalated according to the organization's incident severity and response procedures.

## 9. Documentation Requirements

The case record should include:

- Incident ID, alert source, and timestamps with timezone where available.
- Affected users, devices, accounts, and resources.
- Observed events separated from analyst interpretations.
- Evidence sources and relevant log references.
- Severity, confidence level, and rationale.
- Actions taken, approvals, and outcomes.
- Outstanding questions and assigned follow-up tasks.

## 10. Key Takeaway

Effective SOC triage combines alert validation, evidence correlation, risk assessment, appropriate containment, and clear documentation. Analysts should explain what the evidence supports, identify what remains unknown, and communicate actionable next steps without overstating their conclusions.
