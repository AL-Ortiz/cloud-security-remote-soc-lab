# Cloud Security & Remote SOC Operations Lab

## Project Overview

This project is a simulated cloud security and Security Operations Center (SOC) environment designed to demonstrate skills in cloud security, identity and access management, security monitoring, incident response, and remote SOC operations.

The environment represents Northstar Financial Services, a fictional financial services organization with approximately 500 employees. I approached the scenarios from the perspective of a junior cloud security analyst responsible for investigating alerts, analyzing suspicious activity, recommending security controls, and documenting incidents.

**Project type:** Simulated cybersecurity portfolio lab

**Status:** Core investigation and documentation completed

**Important:** This project uses simulated scenarios and documented designs. It does not represent a production Azure deployment or real security incidents.

## Skills Demonstrated

- Security alert triage and incident investigation
- SIEM and EDR concepts
- Kusto Query Language (KQL)
- Microsoft Azure and Entra ID security concepts
- Role-based access control (RBAC) and least privilege
- Multi-factor authentication (MFA) and Conditional Access
- Network segmentation
- MITRE ATT&CK mapping
- Incident containment and remediation planning
- Evidence preservation and incident timelines
- Remote SOC handoffs and technical documentation

## Simulated Environment

**Organization:** Northstar Financial Services

**Industry:** Financial services

**Size:** Approximately 500 employees

**Cloud platform:** Microsoft Azure concepts

**Identity management:** Microsoft Entra ID concepts

**Security monitoring:** SIEM, Microsoft Sentinel, and EDR concepts

**Analyst role:** Junior Cloud Security Analyst (simulated project role)

## Cloud Security Design

The proposed network uses separate subnets to reduce unnecessary communication between environments.

- Azure Virtual Network: `10.0.0.0/16`
- Development subnet: `10.0.1.0/24`
- Production subnet: `10.0.2.0/24`
- Security subnet: `10.0.3.0/24`

The design incorporates network segmentation, least privilege, RBAC, MFA, Conditional Access, and restricted administrative access.

## Incident Response Case Study

### Incident NS-2026-001

**Incident type:** Suspected account compromise and malicious document execution

**Severity:** Critical

**Affected user:** Alex (`alex@northstar.com`)

**Affected resource:** Finance Quarterly Reports

### Simulated Attack Timeline

| Time | Event |
|---|---|
| 2:47 PM | Alex received an unexpected invoice email |
| 2:50 PM | Invoice document was opened |
| 2:50 PM | Microsoft Word launched PowerShell |
| 2:52 PM | PowerShell executed `invoice.ps1` |
| 2:55 PM | The script contacted external IP `185.44.91.12` |
| 3:01 PM | Finance quarterly reports were accessed |
| 3:02 PM | A Sentinel alert was generated |
| 3:11 PM | Alex denied intentionally opening the document |

These timestamps and events are simulated for educational purposes.

### Investigation Findings

The scenario involved a suspicious invoice attachment, an unusual Word-to-PowerShell process chain, script execution, outbound network communication, and access to sensitive financial files.

The evidence supported treating the incident as a true positive requiring containment and further investigation. Persistent remote access and successful data exfiltration were not confirmed.

### Response Actions

The simulated response included:

- Restricting the affected account and terminating active sessions
- Blocking the suspicious external IP
- Isolating or restricting the affected device
- Quarantining the suspicious document
- Stopping the suspicious script
- Preserving relevant logs and evidence
- Documenting findings and outstanding questions for the next analyst

## Remote SOC Workflow

This project emphasizes the documentation and communication needed for distributed security teams.

Deliverables include incident timelines, triage notes, investigation findings, containment recommendations, a remote SOC handoff, remediation planning, and lessons learned.

The handoff identifies completed actions, unresolved questions, evidence to preserve, and recommended next steps so another analyst can continue the investigation.

## Security Improvements Recommended

- Improve phishing detection and suspicious attachment filtering.
- Alert on suspicious Office-to-PowerShell execution.
- Monitor script execution and unusual outbound network connections.
- Enforce MFA and apply least-privilege access controls.
- Restrict access to confidential financial information.
- Monitor unusual access to sensitive files.
- Improve alert correlation and earlier incident detection.
- Conduct regular access reviews and employee phishing-awareness training.

## Lessons Learned

The incident demonstrates why organizations need defense in depth. A compromised account should not automatically provide unrestricted access to sensitive data.

Combining identity controls, endpoint monitoring, network monitoring, email security, and least privilege can help detect suspicious behavior earlier and reduce the impact of an incident.

## Project Limitations

This is a simulated learning project. Architecture, logs, alerts, and incident details are educational examples rather than evidence from a live production environment. Security recommendations describe proposed controls, not verified deployments.

## Project Outcome

This project demonstrates a documented security workflow spanning cloud security design, identity and access management, alert investigation, incident response, remote analyst communication, remediation, and continuous improvement.
