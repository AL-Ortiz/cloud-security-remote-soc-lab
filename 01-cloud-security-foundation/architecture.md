# Cloud Security Architecture

## 1. Project Overview

This document describes the proposed cloud security architecture for Northstar Financial Services, a fictional organization with approximately 500 employees.

**Project type:** Simulated architecture and security design  
**Cloud platform:** Microsoft Azure concepts  
**Objective:** Separate environments, restrict unnecessary access, and reduce the impact of a compromised account or system.

This architecture is a design exercise and does not represent a live Azure deployment.

## 2. Network Design

The proposed Azure Virtual Network uses the address space `10.0.0.0/16`.

| Network Segment | Address Range | Purpose |
|---|---|---|
| Development | `10.0.1.0/24` | Development systems and testing |
| Production | `10.0.2.0/24` | Production applications and services |
| Security | `10.0.3.0/24` | Security monitoring and investigation resources |

## 3. Security Principles

### Network Segmentation

Development, production, and security resources are separated into different subnets. Network security rules should restrict traffic between them unless a documented business requirement exists.

### Least Privilege

Users and systems should receive only the access necessary to perform their assigned responsibilities.

### Defense in Depth

The architecture combines identity controls, network restrictions, endpoint monitoring, and data protection. No single control should be relied upon to prevent every attack.

### Monitoring

Authentication activity, administrative changes, suspicious endpoint processes, unusual outbound connections, and sensitive file access should be logged and reviewed.

## 4. Access Restrictions

- Developers should not receive unnecessary administrative access to production systems.
- HR data should be accessible only to authorized personnel and approved services.
- Security analysts should have the permissions needed to investigate alerts without automatically receiving full administrative access.
- Cloud administrators should use separate privileged accounts and stronger authentication controls.
- Temporary elevated access should be used when appropriate and removed when no longer needed.

## 5. Example Network Security Rules

| Source | Destination | Proposed Rule |
|---|---|---|
| Development | Production | Deny by default unless approved access is required |
| Development | Approved development services | Allow only required traffic |
| Security | Authorized monitored systems | Permit only necessary investigation and monitoring traffic |
| Internet | Internal resources | Block unsolicited inbound traffic unless explicitly required and protected |

These are proposed policies. Actual rules would need to be implemented and tested in Azure.

## 6. Risks Addressed

- Unauthorized access to production systems
- Excessive permissions
- Lateral movement between network segments
- Exposure of sensitive financial information
- Insufficient visibility into suspicious activity

## 7. Validation Plan

In a live deployment, the design should be validated by confirming that:

1. Network security rules enforce the intended separation.
2. Unauthorized development-to-production traffic is blocked.
3. Users cannot access resources outside their assigned permissions.
4. Security logs capture relevant authentication and network activity.
5. Approved business traffic continues to function.

## 8. Conclusion

Network segmentation and least privilege reduce unnecessary access and help limit the potential impact of a compromised system. These controls should be combined with identity security, endpoint monitoring, and continuous review.
