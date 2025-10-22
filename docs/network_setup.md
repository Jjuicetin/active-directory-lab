# Network Setup

  ## Objectives
  Establish a virtual network enviroment for Active Directory lab using VirtualBox NAT Network. This will allow domain controllers and client machines to communicate while keeping internet access.

  ### VirtualBox Network Configuration

  | Settings | Values |
  | ------ | ----- |
  | Network Mode | NAT Network |
  | Name | ADLab |
  | Network CIDR | 10.0.2.0/24 |
  | Gateway | 10.0.2.2 |
  | DHCP | Disabled |

 > Pic below is to confirm the connection between the three devices
  
![pinging to confirm network](https://github.com/user-attachments/assets/f2c55d1d-c2cc-4295-914b-ad743a9a3bb3)

### Virtual Machines Overview
This lab contains 3 virtual machines. Two consists of Windows Server 2022 domain controllers and the other hosts Windows 10 Pro for client access and testing.

| Hostname | Role | IP Address | Notes |
| -----| ----- | ----- | ----- |
| WINSERVER2022 | Primary Domain Controller | 10.0.2.15 | DNS + DHCP + AD DS |
| DC2 | Secondary Domain Controller | 10.0.2.51 | Redundancy |
| guestUser | Client PC | 10.0.2.50 | Domain Joined |
