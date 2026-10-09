# Role-Based Access Control (RBAC) Matrix

## 1. Purpose

This document defines a proposed role-based access control model for Northstar Financial Services, a fictional organization with approximately 500 employees.

The goal is to apply least privilege, reduce unauthorized access, and separate administrative responsibilities.

**Project type:** Simulated access-control design  
**Platform:** Microsoft Azure and Microsoft Entra ID concepts

## 2. Permission Definitions

| Permission | Meaning |
|---|---|
| None | No access granted |
| Read | View approved information or configurations |
| Modify | Create or change permitted information or configurations |
| Admin | Manage a resource and potentially its permissions |

Actual permissions should be scoped to specific resources and actions rather than relying only on broad role names.

## 3. Proposed Access Matrix

| Group | Employee Apps | Development | Production | HR Data | Security Tools | Azure Administration |
|---|---|---|---|---|---|---|
| Employees | Read | None | None | None | None | None |
| Developers | Read | Modify | None by default | None | None | None |
| Security | Read | Read | Read, where needed | None by default | Modify, as authorized | None by default |
| HR | Read | None | None | Modify, as authorized | None | None |
| Cloud Admins | Admin, as needed | Admin, as needed | Admin, as needed | None by default | Admin, as needed | Admin |

**Important:** This is a conceptual matrix. Production access, security-tool permissions, and administrative duties must be scoped to individual responsibilities. Some analysts may need limited write access to contain threats, but that does not mean every analyst should be a security administrator.

## 4. Least Privilege

Least privilege means users receive only the access needed for their work.

Examples:

- Developers can modify development resources but do not automatically receive production access.
- HR staff can manage approved HR records without access to security administration.
- Security analysts can investigate relevant systems without automatically receiving unrestricted administrative privileges.
- Cloud administrators use elevated permissions only for authorized administrative tasks.

## 5. Separation of Duties

Administrative duties should be separated from ordinary daily activities wherever practical.

Cloud administrators should use separate privileged accounts for administrative tasks. Privileged access should require strong authentication, be monitored, and be reviewed regularly.

## 6. Access Request Scenario

**Request:** A developer requests administrator access to the production database.

**Decision:** Deny broad administrator access by default.

**Reason:** The request exceeds the developer's normal responsibilities and could expose sensitive data or cause accidental changes.

**Alternative:** Determine the specific task and grant the minimum approved permission for the required resource and duration. Any exception should be documented and approved.

## 7. Access Review Process

Access should be reviewed periodically and whenever an employee changes roles or leaves the organization.

The review should check:

1. Whether the user still needs the access.
2. Whether permissions exceed their responsibilities.
3. Whether privileged access is appropriately protected.
4. Whether inactive or unnecessary accounts should be disabled.
5. Whether exceptions have documented approval and expiration dates.

## 8. Conclusion

A well-designed RBAC model helps reduce excessive permissions and limit the damage caused by compromised accounts. Access should be assigned by job responsibility, reviewed regularly, and combined with MFA, Conditional Access, monitoring, and appropriate approval processes.
