# Security Incident Remediation Plan

## 1. Project Overview

- **Organization:** Northstar Financial Services (fictional)
- **Incident ID:** NS-2026-001
- **Incident Type:** Suspected malicious document execution and possible account compromise
- **Priority:** High — provisional assessment
- **Status:** Proposed remediation plan
- **Environment:** Simulated cloud and endpoint security scenario

This plan outlines remediation activities intended to address the weaknesses identified during the simulated incident, reduce the likelihood of recurrence, and improve the organization's ability to detect and respond to similar threats.

No production systems were changed as part of this portfolio exercise.

## 2. Remediation Objectives

1. Contain confirmed malicious activity and determine the scope of the incident.
2. Restore affected systems and accounts to a trusted state.
3. Reduce the risk of malicious document and script execution.
4. Strengthen identity and access controls.
5. Improve visibility into endpoint, network, and sensitive-data activity.
6. Validate improvements and document remaining risks.

## 3. Prioritized Remediation Actions

| Priority | Area | Recommended Action | Validation |
|---|---|---|---|
| Immediate | Endpoint | Isolate the affected device when appropriate and investigate suspicious processes | Confirm containment and review subsequent endpoint activity |
| Immediate | Identity | Revoke sessions and investigate account activity if compromise is suspected | Review authentication logs and verify authorized access |
| Immediate | Data protection | Investigate access to Finance Quarterly Reports | Establish which files were accessed and whether data was transferred |
| High | Email security | Improve suspicious-attachment detection and quarantine | Test approved phishing simulations and review detection results |
| High | Endpoint security | Detect unusual Office-to-PowerShell execution and suspicious scripts | Validate detection against controlled test activity |
| High | Network security | Investigate the external destination and restrict confirmed malicious communication | Review relevant network logs and test the approved rule |
| High | Access control | Review permissions for sensitive financial resources | Confirm access is limited to authorized roles |
| Medium | Identity security | Review MFA, Conditional Access, and session-management policies | Test expected sign-in scenarios |
| Medium | Monitoring | Correlate identity, endpoint, network, and file-access events | Confirm relevant events are available for investigation |
| Medium | Awareness | Provide targeted phishing-awareness training | Track completion and review reporting behavior |

Priorities should be reassessed as the scope and impact of the incident become clearer.

## 4. Identity and Access Remediation

### Recommended actions

- Reset credentials if compromise is suspected or confirmed.
- Revoke active sessions and investigate potentially compromised tokens.
- Require multifactor authentication and review Conditional Access policies.
- Apply least-privilege access to sensitive financial resources.
- Review privileged roles and remove unnecessary permissions.
- Investigate unusual sign-ins and changes to authentication methods.

### Validation criteria

- The affected user can authenticate using approved security controls.
- Unnecessary sessions have been revoked.
- Permissions match the user's job responsibilities.
- Relevant identity events are available for monitoring.

MFA reduces account-takeover risk but does not eliminate it. Identity controls should be combined with session monitoring and endpoint security.

## 5. Email and Endpoint Remediation

### Recommended actions

- Preserve and analyze the suspicious email and document.
- Quarantine confirmed malicious files and remove malicious artifacts after evidence preservation.
- Review the script's behavior and determine whether it created additional files or persistence.
- Improve detection of suspicious Office-to-PowerShell process relationships.
- Review endpoint protection status and update security controls as appropriate.
- Investigate whether other endpoints received or executed the same file.

### Validation criteria

- Confirmed malicious artifacts are contained or removed.
- The affected endpoint passes the required security checks.
- Detection logic identifies relevant suspicious behavior in an authorized test.
- Similar activity is searched for across the environment.

PowerShell should not simply be disabled everywhere. It is used for legitimate administration, so controls should target risky execution patterns and unauthorized behavior.

## 6. Network and Data Protection Remediation

### Recommended actions

- Investigate the external destination using available network and threat-intelligence evidence.
- Restrict confirmed malicious destinations through approved controls.
- Review outbound connections associated with the suspicious script.
- Apply network segmentation to limit unnecessary communication between development and production systems.
- Review permissions for Finance Quarterly Reports.
- Enable appropriate audit logging for sensitive-file access.
- Investigate potential downloads, copying, or external transfers.

### Validation criteria

- Confirmed malicious communication is blocked where appropriate.
- Required application traffic continues to function.
- Sensitive-file access is limited to authorized users and services.
- Investigators can retrieve relevant audit records.
- Data exposure findings are documented, including any unresolved questions.

An external IP address should not be blocked solely because it is unfamiliar. Decisions should be supported by investigation and operational context.

## 7. Monitoring and Detection Improvements

Recommended detection opportunities include:

- Office applications launching PowerShell unexpectedly.
- Suspicious script execution or unusual command-line arguments.
- Script activity followed by external network communication.
- Unusual access to sensitive financial reports.
- Unexpected sign-ins or authentication changes.
- Similar indicators appearing on multiple endpoints.
- Changes to security policies or privileged permissions.

Correlating multiple signals can provide stronger evidence than relying on one isolated alert.

## 8. Remediation Ownership

The following ownership model is proposed for the fictional organization.

| Team | Responsibility |
|---|---|
| SOC | Investigate alerts, correlate evidence, document findings, and monitor for recurrence |
| Endpoint Security / IT | Isolate and recover affected devices; maintain endpoint protections |
| Identity / Cloud Security | Investigate account activity, review access, and strengthen identity controls |
| Network Security | Investigate connections and implement approved network restrictions |
| Data Owners | Validate legitimate access requirements and help assess potential data exposure |
| Security Leadership | Approve significant response decisions and accept or escalate remaining risk |

Actual responsibilities would depend on the organization's structure and incident response policy.

## 9. Success Criteria

Remediation should not be considered complete until the response team verifies that:

- The incident scope and known impact have been documented.
- Confirmed malicious activity has been contained and addressed.
- Affected accounts and endpoints have been restored to a trusted state.
- Relevant sensitive-data access has been reviewed.
- Required security controls are functioning.
- Detection and monitoring improvements have been tested where feasible.
- Outstanding risks have been assigned to an owner.
- Closure has been approved according to organizational procedures.

## 10. Remaining Risks

Even after remediation, potential risks may remain if:

- The script's complete behavior cannot be established.
- Audit logs are missing or incomplete.
- Credentials or sessions may have been compromised.
- Similar activity occurred on systems without adequate telemetry.
- Sensitive-data exposure cannot be ruled out.

These limitations should be documented rather than assuming that the absence of evidence proves the absence of compromise.

## 11. Key Takeaway

Effective remediation addresses the immediate incident and the underlying security weaknesses. By combining identity controls, endpoint detection, network segmentation, data-access monitoring, and validation, an organization can reduce future risk and improve incident response readiness.

This plan is a simulated portfolio artifact, not evidence of remediation performed in a live environment.
