# Conditional Access and MFA Policy Design

## 1. Purpose

This document describes proposed identity-protection policies for Northstar Financial Services, a fictional financial services organization.

The goal is to reduce the risk of unauthorized account access by combining multi-factor authentication (MFA), sign-in risk evaluation, device security, and least privilege.

**Project type:** Simulated security policy design  
**Platform:** Microsoft Entra ID concepts  
**Status:** Proposed policies; not deployed in a live tenant

## 2. Policy 1 — Require MFA

**Objective:** Reduce the risk of unauthorized access if a password is stolen.

**Proposed policy:**
- Require MFA for employee access to company resources.
- Require strong authentication for privileged administrator accounts.
- Use approved authentication methods.
- Monitor repeated MFA failures and unexpected authentication prompts.

**Expected result:** A stolen password alone should not normally be sufficient to access protected resources.

**Limitation:** MFA reduces risk but does not eliminate it. Attackers may still exploit stolen sessions, compromised devices, or MFA fatigue.

## 3. Policy 2 — Investigate Unfamiliar Sign-Ins

**Scenario:** An employee signs in from an unfamiliar device or unusual location.

**Proposed response:**
- Evaluate the sign-in context and available risk signals.
- Require MFA or stronger authentication when appropriate.
- Restrict or block access when the sign-in is assessed as high risk, according to approved policy.
- Alert the security team when the activity is suspicious.

**Expected result:** Unusual authentication activity receives additional scrutiny before access is granted.

**Important:** An unfamiliar location alone does not prove an account is compromised. Travel, VPN use, and legitimate device changes should be considered.

## 4. Policy 3 — Protect Privileged Accounts

**Objective:** Reduce the risk of administrative account compromise.

**Proposed controls:**
- Use separate administrator and everyday user accounts.
- Require MFA for privileged access.
- Limit administrative roles to authorized personnel.
- Monitor role assignments and privileged activity.
- Use just-in-time access where supported and appropriate.
- Review administrative permissions regularly.

**Expected result:** A compromised everyday account should not automatically provide administrative control over the environment.

## 5. Policy 4 — Device Security

**Objective:** Reduce the risk of access from compromised or unmanaged devices.

**Proposed controls:**
- Require compliant devices for sensitive resources where business requirements permit.
- Evaluate device health and sign-in risk.
- Restrict access from devices that fail required security checks.
- Provide an approved exception process for legitimate business needs.

**Expected result:** Sensitive company resources are better protected from devices that do not meet security requirements.

## 6. Example Sign-In Scenario

**User:** Jordan  
**Activity:** Successful sign-in from an unfamiliar device in another country  
**Additional context:** Jordan denies the activity and reports no travel.

**Analyst response:**
1. Review sign-in timestamps, IP address, location, device details, and authentication results.
2. Verify the activity with Jordan through an approved communication channel.
3. If compromise is suspected, revoke active sessions and restrict the account.
4. Review authentication changes and resources accessed.
5. Preserve logs and document the investigation.
6. Restore access only after the account is secured and appropriate checks are complete.

## 7. Monitoring Requirements

The SOC should monitor for:

- Repeated failed sign-ins followed by success
- Sign-ins from unusual locations or devices
- Unexpected MFA denials or suspicious MFA activity
- Changes to authentication methods
- New privileged role assignments
- Unusual activity after a successful sign-in
- Repeated access attempts against sensitive resources

Multiple related signals should be evaluated together rather than treating one unusual event as proof of compromise.

## 8. Validation Plan

In a live environment, these policies should be tested using approved test accounts and documented scenarios.

Validation should confirm that:
1. MFA is required for the intended users and resources.
2. Privileged accounts receive stronger protection.
3. Risk-based restrictions behave as intended.
4. Legitimate users retain necessary access.
5. Security alerts are generated for the scenarios the policies are designed to detect.
6. Exceptions are documented, approved, and reviewed.

## 9. Conclusion

Conditional Access and MFA help protect identities by evaluating authentication context and enforcing access requirements. Combined with least privilege, device security, monitoring, and incident response, these controls reduce the risk and potential impact of account compromise.
