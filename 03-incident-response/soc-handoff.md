# Remote SOC Incident Handoff

## 1. Handoff Details

- **Organization:** Northstar Financial Services (fictional)
- **Incident ID:** NS-2026-001
- **Priority:** High — provisional assessment
- **Incident Type:** Suspected malicious document execution and possible account compromise
- **Affected User:** Alex (`alex@northstar.com`)
- **Affected Resource:** Finance Quarterly Reports
- **Current Status:** Investigation and remediation required
- **Handoff Purpose:** Transfer investigation context, outstanding tasks, and response priorities
- **Environment:** Simulated security scenario; no live incident investigated

## 2. Situation Summary

An invoice-themed email was followed by a Word document opening, PowerShell execution, script activity, an external network connection to `185.44.91.12`, and access to Finance Quarterly Reports.

A simulated SIEM alert was generated at 3:02 PM. At 3:11 PM, Alex denied intentionally opening the document.

The event sequence suggests a likely security incident. The script's behavior, the destination's reputation, possible identity compromise, and the scope of any data exposure remain unconfirmed.

## 3. Key Timeline

| Time | Event |
|---|---|
| 2:47 PM | Invoice-themed email received |
| 2:50 PM | `Invoice_10482.docx` opened |
| 2:50 PM | `WINWORD.EXE` launches `powershell.exe` |
| 2:52 PM | `invoice.ps1` executes |
| 2:55 PM | Script contacts `185.44.91.12` |
| 3:01 PM | Finance Quarterly Reports accessed |
| 3:02 PM | SIEM alert generated |
| 3:11 PM | User denies intentionally opening the document |

The scenario does not specify a timezone or provide raw event records.

## 4. Immediate Priorities

The receiving analyst or incident response team should:

1. Confirm whether the affected endpoint has been isolated.
2. Verify whether active sessions have been revoked if identity compromise is suspected.
3. Confirm that relevant evidence has been preserved.
4. Review the script, process tree, and associated endpoint alerts.
5. Investigate the external destination using available network and threat-intelligence data.
6. Determine which financial reports were accessed and whether data was transferred.
7. Search for related activity across other accounts and devices.
8. Escalate according to the organization's incident severity procedures.

**Important:** These are handoff tasks, not confirmation that the actions have already been completed.

## 5. Evidence and Data Sources to Review

| Evidence Source | Investigation Goal |
|---|---|
| Original email and attachment | Establish the sender, delivery method, and file details |
| EDR process telemetry | Reconstruct Word, PowerShell, and script execution |
| Script contents and file metadata | Determine what the script actually did |
| Network and firewall logs | Validate the external connection and identify related activity |
| Microsoft Entra sign-in logs | Investigate suspicious authentication and account activity |
| File-access audit logs | Identify which financial reports were accessed |
| SIEM alerts and analyst notes | Correlate detections and document prior decisions |

Access to these sources depends on the tools, permissions, and logging available in the environment.

## 6. Known Facts vs. Unknowns

### Known within the simulated scenario

- A suspicious invoice-themed email was received.
- A Word document was opened.
- Word launched PowerShell.
- A script executed.
- An external IP address was contacted.
- Finance Quarterly Reports were accessed.
- A SIEM alert was generated.
- The user denied intentionally opening the document.

### Still unknown

- Whether the document and script are confirmed malicious.
- What actions the script performed.
- Whether credentials or sessions were compromised.
- Whether data was copied or exfiltrated.
- Whether persistence or lateral movement occurred.
- Whether additional users or endpoints were affected.
- Whether proposed containment actions have been completed and validated.

Do not report an unconfirmed hypothesis as an established finding.

## 7. Communication and Escalation

The receiving analyst should:

- Acknowledge the handoff and confirm ownership of outstanding tasks.
- Maintain the incident ID across related notes and updates.
- Record significant findings with timestamps and evidence sources.
- Communicate material changes in severity or scope promptly.
- Escalate possible sensitive-data exposure to the appropriate response and data-protection teams.
- Record actions, approvals, results, and remaining risks in the incident record.

For remote collaboration, updates should be concise, factual, and understandable without requiring the next analyst to repeat the initial investigation.

## 8. Handoff Acceptance Checklist

- [ ] Incident ID and current priority reviewed.
- [ ] Timeline and key process relationships reviewed.
- [ ] Containment status verified rather than assumed.
- [ ] Evidence sources identified and preservation status checked.
- [ ] Outstanding investigation questions assigned.
- [ ] Escalation requirements reviewed.
- [ ] Next update or follow-up point documented.

## 9. Next Update

The next update should summarize:

- New evidence and what it establishes.
- Current containment and investigation status.
- Any change to severity or scope.
- Outstanding tasks and assigned owners.
- Risks that require leadership or incident response attention.

The update time should be recorded using the organization's standard timezone convention.

## 10. Handoff Summary

**Current assessment:** Likely security incident involving suspicious document and script execution, external communication, and access to sensitive financial reports.

**Primary risk:** Potential compromise of an endpoint or user account and possible exposure of financial information.

**Next priority:** Verify containment, preserve evidence, analyze script behavior, and determine whether sensitive data or additional systems were affected.

**Status limitation:** This handoff is a simulated portfolio artifact. It does not establish that live systems were contained or that an actual SOC shift change occurred.
