# Active Directory Home Lab — AK Technologies

## Project Overview

This project documents the design and configuration of a Windows Server 2022 Active Directory home lab for **AK Technologies**, a fictional organization. The lab simulates common IT support and junior systems administration responsibilities, including domain setup, user and group management, workstation enrollment, Group Policy, departmental file sharing, access control, and PowerShell automation.

The environment was built in **Oracle VirtualBox** using a Windows Server 2022 domain controller and a Windows 10 Pro client. The project focuses on practical administration and verification rather than enterprise-scale production deployment.

## Lab Environment

| Component | Configuration |
| --- | --- |
| Virtualization | Oracle VirtualBox |
| Domain controller | **DC01** — Windows Server 2022 |
| Domain | `ad.aktech.test` (NetBIOS: `AKTECH`) |
| DC01 host-only IP | `192.168.56.10/24` |
| Domain services | Active Directory Domain Services (AD DS) and DNS |
| Domain-joined workstation | **CLIENT01** — Windows 10 Pro |
| CLIENT01 host-only IP | `192.168.56.20/24` |
| Network | VirtualBox host-only network (`192.168.56.0/24`) for lab connectivity, with NAT for internet access |
| Administration tools | ADUC, Group Policy Management, PowerShell, Windows networking and firewall tools |

## Work Completed

### 1. Windows Server and Active Directory Setup
- Configured DC01 with a static IP address and installed **Active Directory Domain Services (AD DS)** and **DNS**.
- Promoted DC01 to a domain controller and created the `ad.aktech.test` forest/domain.
- Established the organizational structure for the fictional company.

### 2. Organizational Units, Users, and Security Groups
- Created an `AKTechnologies` OU with departmental user OUs for **IT, Finance, HR, Sales, Operations, Executive, and Design**, plus separate locations for groups, servers, workstations, and disabled users.
- Created user accounts and practiced user administration, including password resets, account management, and an offboarding workflow.
- Configured departmental **Global Security Groups** (for example, `GG_IT_Staff` and `GG_Design_Staff`) and **Domain Local Groups** for resource access (for example, `DL_Design_Modify`).
- Used the **AGDLP** access model: **Accounts → Global Groups → Domain Local Groups → Permissions**.

### 3. Domain-Joined Client
- Installed and configured **CLIENT01** with Windows 10 Pro.
- Configured CLIENT01 to use DC01 for DNS, joined it to `ad.aktech.test`, and placed the computer in the appropriate Workstations OU.
- Tested domain connectivity, name resolution, and domain-user sign-in using `AKTECH\Shana.Karan`.

### 4. Group Policy and Workstation Security
- Created and linked Group Policy Objects (GPOs), including:
  - **`GPO_Workstations_Screenlock`** — configured a five-minute inactivity lock setting.
  - **`GPO_Workstations_Firewall`** — configured a scoped inbound ICMPv4 echo-request rule permitting requests from DC01.
  - **`GPO_Users_CompanyPortal`** — deployed an AK Technologies portal shortcut to users.
  - **`GPO_Users_DepartmentDriveMapping`** — mapped the Design departmental share to drive **S:** for the relevant user group.
- Configured domain account lockout policy settings through the Default Domain Policy.
- Used `gpupdate` and `gpresult` on CLIENT01 to check policy application, and performed connectivity checks relevant to the firewall configuration.

### 5. Departmental File Shares and Access Control
- Created departmental folders under `C:\CompanyShares`, including **Design, Finance, IT, and Sales**.
- Configured NTFS permissions for departmental **Domain Local Modify** groups, removed broad general-user access from the parent folder, and retained administrative/system access.
- Published SMB shares such as `\\DC01\design` and `\\DC01\finance`.
- Tested access from CLIENT01 while signed in as a Design user: the Design share was accessible, while access to the Finance share was denied.
- Configured and verified the mapped **Design (S:)** network drive.

### 6. PowerShell Administration and Automation
- Queried Active Directory users, security groups, and OUs using `Get-ADUser`, `Get-ADGroup`, and `Get-ADOrganizationalUnit`.
- Created and configured a test account (**Alex Morgan**) through PowerShell, including setting a password, enabling the account, and adding it to `GG_IT_Staff`.
- Built a CSV-driven employee onboarding workflow to create **five fictional employee accounts**, place them in departmental OUs, assign Global Security Groups, and require a password change at first login.
- Verified account creation, enabled status, and group memberships.
- Exported an Active Directory user inventory to **`AD-UserReport.csv`** with names, usernames, account status, departments, and distinguished names.

### 7. Validation and Evidence
- Validated the domain configuration, employee accounts, and Global Security Groups using PowerShell.
- Reviewed applied user and computer GPOs on CLIENT01 with `gpresult`.
- Verified departmental share access restrictions and reused earlier screenshots as evidence.
- Documented the setup and results with screenshots throughout the lab.

## Key Skills Demonstrated

- Windows Server 2022 administration and Active Directory Domain Services
- DNS configuration and Windows domain joining
- Organizational Unit design and account lifecycle management
- Role-based access control using Global and Domain Local security groups
- Group Policy configuration and troubleshooting
- NTFS and SMB share permission management
- Windows Firewall rule configuration and network troubleshooting
- PowerShell administration, CSV-based onboarding, and reporting
- Technical validation and documentation



## Project Outcome

The lab provided hands-on experience with the core administrative workflows found in Windows-based enterprise environments: provisioning users and workstations, assigning permissions, deploying policies, controlling departmental access, automating repetitive tasks, and verifying configuration through PowerShell and client testing.
