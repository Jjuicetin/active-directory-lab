# Domain Controller Replication

### Overview
This section documents the configuration and verification of Active Directory (AD) replication between two domain controllers within the int.justy.com domain.

### Objective

* Ensure directory data is synchronized between DC1 and DC2.
* Validate replication topology and health.
* Simulate redundancy for production-like reliability.

### Promote DC2 to Domain Controller
On your Server Manager > Local Server's Dashboard, click on your computer name to bring up system properties. Click change > toggle on "Member of" and enter your domain name. In this instance, it will be int.justy.com
<br><br>
![join domain](https://github.com/user-attachments/assets/7c5df0f1-72f6-45fd-8c81-9fffa8136faf)

Launch Server Manager → Add Roles and Features.

Install Active Directory Domain Services (AD DS).

Chose “Add a domain controller to an existing domain”.

Specified domain: int.justy.com.

Verify and enable replication from DC1

Restart machine to finish promotion.

### Verify Replication
Run these commands in both domain controllers in PowerShell.
* repadmin /replsummary > gives you a summary of AD replication health across all DCs. Useful to identify which DC is causing issues.
* repadmin /showrepl > shows inbound replication info for one specific domain controller
* dcdiag /test:replications check the replication between your domain controllers
<br><br>
![replsummary](https://github.com/user-attachments/assets/ccd2924b-c062-49a0-b09c-28546cc470ee)

![showrepl](https://github.com/user-attachments/assets/262d1738-793d-467c-bbb7-df04007b6fa9)

![dcdiag](https://github.com/user-attachments/assets/a1698b05-b462-4b0f-9f7d-356ed70ae4ef)

  You should be seeing Replication status = 0 fails and Inbound & outbound connections established between DC1 and DC2

*** Notes
DNS on DC2 should point to DC1’s (WINSERVER2022) IP (10.0.2.15) as its Preferred DNS, and to itself (10.0.2.51) as Alternate DNS.
