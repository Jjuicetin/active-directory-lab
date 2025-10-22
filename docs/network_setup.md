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


### Virtual Machines Overview
This lab contains 3 virtual machines. Two consists of Windows Server 2022 domain controllers and the other hosts Windows 10 Pro for client access and testing.

| Hostname | Role | IP Address | Notes |
| -----| ----- | ----- | ----- |
| WINSERVER2022 | Primary Domain Controller | 10.0.2.15 | DNS + DHCP + AD DS |
| DC2 | Secondary Domain Controller | 10.0.2.51 | Redundancy |
| guestUser | Client PC | 10.0.2.50 | Domain Joined |


 > Pic below is to confirm the connection between the three devices
  
![pinging to confirm network](https://github.com/user-attachments/assets/f2c55d1d-c2cc-4295-914b-ad743a9a3bb3)

### Lessons Learned + Troubleshooting

* Leaving DHCP enabled in VirtualBox can cause IP conflicts with Windows DHCP service.
* The DNS server must always point to the domain controller, not an external DNS
* Using NAT Network instead of regular NAT allows VM-to-VM communication.

  #### Issues
  Two domain controllers were able to ping each other but not towards the client VM. I knew I had the network setup correctly as it shared the subnet of 10.0.2.0/24. I tried ipconfig /all on the client machine and I found out that it did not have a default gateway. Once I entered the default gateway on the IPV4 adapter inside the control panel, I pinged again but it did not ping to the domain controllers. With more digging, I found out that inbound and outbound ICMP echo rules are disabled by default for security reasons. I entered PowerShell with admin access and entered "Enable-NetFirewallRule -DisplayGroup "File and Printer Sharing"" Once that was done, I tested pinging again and it worked!
  
