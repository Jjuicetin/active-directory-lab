# 🛡️ Active Directory Home Lab (Windows Server 2022)

A simulated enterprise Active Directory environment built using Windows Server 2022 and Windows 10 Pro to practice identity management, networking, Group Policy, file permissions, and IT infrastructure design—following real-world IT best practices.

🎯 Project Purpose

### This lab is designed to:

1. Learn and configure Active Directory Domain Services (AD DS)

2. Build redundant domain controllers for high availability

3. Implement DNS + DHCP in a private domain

4. Create OUs, users, security groups, and GPOs

5. Configure Folder Redirection & network shares

6. Apply NTFS & share permissions

7. Practice IT documentation & infrastructure design

8. Showcase IT administration skills for job readiness and portfolio

## Lab Architecture

### Component	Details
Domain Name: int.justy.com

DC1	Primary Domain Controller (DNS + DHCP)

DC2	Secondary Domain Controller (Redundancy)

Client OS	Windows 10 Pro

Network Mode	VirtualBox NAT Network

IP Scheme	10.0.2.X /24

## Technologies Used
### Category	Tools / Services
Directory Services: Active Directory Domain Services (AD DS)

Networking:	DNS, DHCP, NAT Network

OS:	Windows Server 2022, Windows 10 Pro

Security:	Group Policy, NTFS Permissions

Admin Tools:	PowerShell, Server Manager

Virtualization:	VirtualBox

🚀 Features Implemented

 Active Directory domain: int.justy.com

 Redundant domain controllers (DC1 & DC2)

 DHCP scope for client auto-IP

 DNS integrated with AD

 OU structure (IT, HR, Finance, etc.)

 User and group management

 File server + shared folders (Coming soon...)

 NTFS permissions + Access Control

 Group Policy for security hardening (Coming soon...)

 Folder Redirection for Documents/Desktop (Coming soon...)
