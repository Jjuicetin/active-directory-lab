# Domain Setup

### Objectives
The objectives in this section is to configure and promote the first Windows Server 2022 instance as a domain controller to create the Active Directory forest int.justy.com

### System Information
| Hostname | IP Address | Subnet Mask | Default Gateway | Preferred DNS | Domain Name
| --- | --- | --- | --- | --- | --- |
| WINSERVER2022 | 10.0.2.15 | 255.255.255.0 | 10.0.2.2 | 10.0.2.15 | int.justy.com |

### Prerequisites
Before we begin promoting our virtual machine to a domain controller, we must:

* Have NAT Network configured on VirtualBox. (10.0.2.0/24)
* Server has a static IP address
* Able to ping other VMs and gateways
* Windows Server is up-to-date.

### Step 1
1. Open Server Manager -> Local Server
2. Under Computer Name, click change.
3. In this instance the computer name was changed to WINSERVER2022. Once a computer becomes a domain controller, its name becomes part of the domain's infrastructure. Changing it afterward is complex and risky. It can break replication, DNS records, and trust relationships.

   > This is the Local Server dashboard. Click on the name and press change to change your computer's name. 
![local server dashboard](https://github.com/user-attachments/assets/d6083dbc-e8f3-44fc-8522-5a1c3d3e2d34)

   
### Verification
![getaddomain verification](https://github.com/user-attachments/assets/0f936ece-3fd9-4183-b21c-a484c5a5f9b1)
![dhcpscope verificaiton](https://github.com/user-attachments/assets/87106d6a-e643-4558-9147-f91b56418c4f)
![getwindowfeaturead verification](https://github.com/user-attachments/assets/1ab560a2-e5d1-43fa-bb88-ce607e68f472)

### Some Issues that Occurred and how I Fixed it

### Lesson Learned
* internal use domains should have int after the domain name as the ones without it are generally used for public use.

#### Rename Computer
1. Open S
