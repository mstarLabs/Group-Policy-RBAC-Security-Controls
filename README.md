# Group Policy, RBAC, and Security Controls

## Project Overview

This repository documents the implementation of Group Policy, Role-Based Access Control (RBAC), and centralized Windows security controls within the Enterprise Identity Security Lab.

Building upon the Enterprise Network Architecture, Enterprise Firewall Platform, and Active Directory Domain Services repositories, this repository extends centralized identity into centralized policy enforcement, endpoint security, administrative control, and enterprise authorization.

Rather than documenting Group Policy configuration in isolation, this repository demonstrates how enterprise organizations use Active Directory Organizational Units (OUs), security groups, Group Policy Objects (GPOs), and NTFS permissions to standardize workstation configuration, enforce least privilege, delegate administrative responsibilities, and centrally manage enterprise security policies.

This repository emphasizes enterprise policy management, security baselines, Role-Based Access Control (RBAC), least-privilege administration, policy validation, and implementation evidence.

---

## Role Within the Enterprise Identity Security Lab

The Group Policy, RBAC, and Security Controls repository represents the fourth architectural layer of the Enterprise Identity Security Lab.

It implements the centralized policy management, enterprise security baselines, and role-based authorization required to consistently secure Windows systems and support downstream identity and security services.

This repository is responsible for documenting:

- Group Policy Object (GPO) implementation
- Organizational Unit policy assignment
- Role-Based Access Control (RBAC)
- Active Directory security group design
- Enterprise security baselines
- Administrative restrictions
- Endpoint security configuration
- NTFS authorization
- Policy validation
- Enterprise policy implementation evidence

Network architecture, firewall policy, Active Directory deployment, authentication services, DNS, and directory administration remain the responsibility of the Enterprise Network Architecture, Enterprise Firewall Platform, and Active Directory Domain Services repositories.

---

## Design Objectives

The Group Policy, RBAC, and Security Controls implementation was designed around the following enterprise policy and security objectives:

- Centralize Windows security configuration through Group Policy.
- Implement Role-Based Access Control (RBAC).
- Enforce least-privilege administrative practices.
- Standardize enterprise security baselines across managed endpoints.
- Separate administrative responsibilities through Organizational Units.
- Apply enterprise security controls aligned with NIST SP 800-53 guidance.
- Manage resource authorization through Active Directory security groups.
- Provide the centralized policy foundation for future identity and security services.

---

## Architecture

The Group Policy, RBAC, and Security Controls repository depends on the enterprise identity infrastructure established by the Active Directory Domain Services repository and the underlying network and communication services provided by the Enterprise Network Architecture and Enterprise Firewall Platform repositories.

Rather than introducing new identity services, this repository extends the existing identity platform by implementing centralized policy management, enterprise security baselines, administrative controls, and Role-Based Access Control (RBAC) across enterprise systems.

The following relationship defines the responsibility boundary between the repositories:

| Repository | Responsibility |
|------------|----------------|
| Enterprise Network Architecture | Defines network topology, addressing, trust boundaries, and communication requirements |
| Enterprise Firewall Platform | Implements routing, DHCP, NAT, and firewall policies required to support enterprise services |
| Active Directory Domain Services | Implements centralized identity, authentication, DNS, directory services, and enterprise administration |
| Group Policy, RBAC, and Security Controls | Implements centralized policy management, enterprise security baselines, endpoint configuration, and role-based authorization |

---

## Security Framework Alignment

| NIST SP 800-53 Control | Enterprise Implementation |
|-------------------------|---------------------------|
| AC-2, AC-3 | Role-Based Access Control using Active Directory Security Groups |
| AC-6 | Least Privilege enforced through Group Policy |
| AU-8 | Interactive Logon Banner |
| CM-2 | Standardized Windows Configuration Baseline |

---

## Identity Organizational Structure

The Organizational Unit (OU) hierarchy established by the Active Directory Domain Services repository provides the administrative boundaries used to scope Group Policy throughout the Enterprise Identity Security Lab.

Department-specific Organizational Units separate Human Resources and Sales identities while dedicated computer Organizational Units enable workstation-specific policy assignment and consistent endpoint configuration.

This design supports centralized policy management, administrative delegation, policy inheritance, security filtering, and future expansion of enterprise identity and security services.

> **Implementation Evidence:** Organizational Unit structure

![OU_Structure](Documentation/OU_Structure.png)

---

## Role-Based Access Control (RBAC)

Role-Based Access Control (RBAC) provides the enterprise authorization model used throughout the Enterprise Identity Security Lab.

Rather than assigning permissions directly to individual user accounts, authorization is delegated through Active Directory security groups. This approach centralizes permission management, supports least-privilege administration, simplifies auditing, and enables consistent access control as users join, move between, or leave departments.

The following user-to-group assignments document the authorization model implemented within the Enterprise Identity Security Lab.

Stored in `Documentation/GroupMemberships.csv`

| User       | Groups                                  |
|------------|-----------------------------------------|
| Lab Admin  | Domain Users, Administrators            |
| Sales Test | Domain Users, Sales_ReadAccess          |
| HR Test    | Domain Users, HR_ReadOnly               |

The following implementation demonstrates how user identities inherit authorization through security group membership.

> **Implementation Evidence:** Sales security group membership

![SG_Sales_Memebers](Documentation/SG_Sales_Memebers.png)

This implementation demonstrates the enterprise practice of assigning permissions to security groups rather than individual user accounts.

---

## Resource Authorization

Resource authorization within the Enterprise Identity Security Lab is implemented by combining Active Directory security groups with NTFS Access Control Lists (ACLs).

Rather than assigning permissions directly to individual user accounts, access is granted to security groups representing organizational roles. This approach centralizes authorization, simplifies permission management, supports least-privilege administration, and ensures consistent access control as users join, move between, or leave departments.

The following authorization assignments demonstrate how departmental resources are protected through centralized group-based access control.

**Sales Folder**:
- Location: `C:\Shares\Sales`
- Group: `Sales_ReadAccess`
- Access: Read-only

**HR Folder**:
- Location: `C:\Shares\HR`
- Group: `HR_ReadAccess`
- Access: Read-only

> **Configuration Evidence:** Sales share permissions

![Sales_Share_Permissions](Documentation/Sales_Share_Permissions.png)

> **Configuration Evidence:** NTFS security permissions

![Sales_Share_Security](Documentation/Sales_Share_Security.png)

This implementation demonstrates how centralized identity integrates with resource-level authorization. By combining Active Directory security groups with NTFS permissions, access decisions remain consistent, auditable, and scalable while supporting enterprise least-privilege principles.

---

## Group Policy Implementation

Group Policy Objects (GPOs) provide the centralized policy enforcement mechanism used throughout the Enterprise Identity Security Lab.

Building upon the Organizational Unit hierarchy established within Active Directory Domain Services, Group Policy enables enterprise administrators to consistently apply security baselines, administrative restrictions, and workstation configuration across managed systems without requiring manual endpoint configuration.

The following Group Policy Objects demonstrate how centralized policy is applied to departmental users and enterprise workstations.

| Group Policy Object | Linked Organizational Unit | Purpose |
|----------------------|----------------------------|---------|
| SalesUsers-DesktopRestrictions | Sales_Users | Restricts administrative utilities for Sales users |
| HRUsers-DesktopRestrictions | HR_Users | Restricts administrative utilities for Human Resources users |
| Login Banner | Domain / Computers | Displays the enterprise interactive logon banner |

### Policy Configuration

The implemented Group Policy configuration includes the following enterprise security controls:

- Interactive logon banner
- Control Panel restrictions
- Registry Editor restrictions
- Command Prompt restrictions
- Department-specific policy targeting through Organizational Units

> **Configuration Evidence:** Group Policy Management Console

![GPMC_Structure](Documentation/GPMC_Structure.png)

> **Implementation Evidence:** Enterprise interactive logon banner

![Login Banner](Documentation/Logon_Banner.png)

The implemented Group Policy Objects demonstrate how centralized policy enforcement integrates with Active Directory Organizational Units to provide consistent workstation configuration, administrative restrictions, and enterprise security baselines across managed systems.

---

## Security Design

The security design of the Enterprise Identity Security Lab combines centralized identity, policy enforcement, and resource authorization to provide consistent security controls across managed Windows systems.

Rather than relying on individual workstation configuration, security policies are centrally managed through Group Policy, Active Directory security groups, Organizational Units, and NTFS permissions. This layered approach simplifies administration while supporting least-privilege access, administrative separation, and standardized security baselines.

The implementation applies the following enterprise security principles:

- Centralized policy management
- Role-Based Access Control (RBAC)
- Least-privilege administration
- Administrative separation
- Standardized Windows security baselines
- Organizational Unit–based policy targeting
- Centralized resource authorization using Active Directory security groups

Administrative privileges remain restricted to authorized administrators while standard users receive only the policies and permissions required for their organizational role. This design reinforces least privilege, improves administrative consistency, and establishes a scalable security model that supports future identity and access management capabilities.

---

## Policy Engineering

The policy implementation was developed incrementally to reflect how enterprise environments typically evolve from foundational identity services to centralized policy enforcement and authorization.

The initial implementation established Organizational Units and Active Directory security groups to provide the administrative and authorization structure required for centralized management.

Group Policy Objects were then introduced to standardize workstation configuration, apply enterprise security baselines, and enforce administrative restrictions across managed systems.

As the environment matured, Active Directory security groups were integrated with NTFS permissions to extend Role-Based Access Control (RBAC) from identity management to resource authorization.

Finally, policy validation using GPResult confirmed that Group Policy processing, security settings, administrative restrictions, and authorization controls were consistently applied throughout the enterprise environment.

---

## Validation

The Group Policy, RBAC, and Security Controls implementation was validated through functional testing to ensure centralized policy management, authorization, and security controls behaved as expected throughout the enterprise environment.

### Validation Results

| Test | Expected Result | Status |
|------|-----------------|:------:|
| Organizational Unit structure | Policies are linked to the correct Organizational Units | ✅ Passed |
| Security group membership | Users inherit authorization through assigned security groups | ✅ Passed |
| NTFS permissions | Users access only authorized departmental resources | ✅ Passed |
| Shared folder authorization | Departmental shares enforce Role-Based Access Control | ✅ Passed |
| Group Policy processing | Client systems successfully process assigned Group Policy Objects | ✅ Passed |
| Desktop restriction policies | Administrative utilities are restricted for standard users | ✅ Passed |
| Interactive logon banner | Enterprise logon banner displays before user authentication | ✅ Passed |
| GPResult policy validation | Applied Group Policy Objects match the expected configuration | ✅ Passed |

Successful validation confirms that centralized policy management, Role-Based Access Control (RBAC), and enterprise security baselines integrate correctly with Active Directory Domain Services while providing the authorization framework required by future identity services.

### Group Policy Results

The `gpresult_sales.html` report is included within the `Documentation` directory and confirms that the expected Group Policy Objects were successfully processed by the Sales workstation.

> **Validation Evidence:** GPResult policy processing

![Sales_GroupPolicyResults](Documentation/Sales_GroupPolicyResults.png)
---

## Skills Demonstrated

### Enterprise Policy Engineering

- Group Policy Object (GPO) deployment
- Organizational Unit (OU) design and administration
- Active Directory security group management
- Enterprise policy implementation
- Centralized Windows configuration management
- Interactive logon banner implementation
- Enterprise workstation policy administration

### Authorization Engineering

- Role-Based Access Control (RBAC)
- Security group authorization design
- NTFS permission management
- Departmental resource authorization
- Least-privilege policy implementation
- Group-based access administration
- Enterprise authorization validation

### Enterprise Security

- Windows security baseline implementation
- Administrative restriction policies
- Centralized security policy enforcement
- Separation of administrative responsibilities
- Enterprise endpoint hardening
- Security framework alignment

### Documentation

- Enterprise policy documentation
- Group Policy implementation documentation
- Configuration evidence
- Validation documentation
- GPResult policy validation
- Cross-repository architectural references

---

## Related Projects

This repository provides centralized policy management, role-based access control, and enterprise security controls for the Enterprise Identity Security Lab.

| Repository | Architectural Relationship |
|------------|----------------------------|
| **[mstarLabs](https://github.com/mstarLabs/mstarLabs)** | Provides the portfolio architecture, governance standards, repository responsibilities, and modernization workflow for the Enterprise Identity Security Lab. |
| **[Enterprise Network Architecture](https://github.com/mstarLabs/Enterprise-Network-Architecture)** | Defines the network topology, trust boundaries, and communication requirements used by this repository. |
| **[Enterprise Firewall Platform](https://github.com/mstarLabs/Enterprise-Firewall-Platform)** | Implements the routing, firewall policies, and least-privilege communication required for centralized policy management. |
| **[Active Directory Domain Services](https://github.com/mstarLabs/Active-Directory-Domain-Services)** | Provides the centralized identity platform, authentication services, Organizational Units, and directory services required for Group Policy and RBAC. |

The technical repositories listed above demonstrate the enterprise infrastructure that supports centralized policy management and authorization within the Enterprise Identity Security Lab.

---

## Future Enhancements

The Group Policy, RBAC, and Security Controls repository will continue evolving to support additional identity, security, and operational capabilities within the Enterprise Identity Security Lab.

Future architectural requirements include:

- Active Directory Certificate Services
- Hybrid Identity with Microsoft Entra ID
- Identity Automation
- Identity Governance and Administration
- Privileged Access Management
- Centralized Logging/Monitoring and SIEM

As additional enterprise services are introduced, this repository will document enterprise policy management, authorization models, security baselines, and administrative controls required to support them.
