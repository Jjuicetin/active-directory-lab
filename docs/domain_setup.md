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
* Able to ping other VMs and gateways
* Windows Server is up-to-date.

### Step 1: Renaming PC
1. Open Server Manager -> Local Server
2. Under Computer Name, click change.
3. In this instance the computer name was changed to WINSERVER2022. Once a computer becomes a domain controller, its name becomes part of the domain's infrastructure. Changing it afterward is complex and risky. It can break replication, DNS records, and trust relationships.

   > This is the Local Server dashboard. Click on the name and press change to change your computer's name. 
   ![local server dashboard](https://github.com/user-attachments/assets/d6083dbc-e8f3-44fc-8522-5a1c3d3e2d34)

### Step 2: Configuring Static IP
1. Find your IP address by going into command prompt and typing ipconfig /all
2. Open Network Connections → Ethernet → Properties

   
   ![network connection](https://github.com/user-attachments/assets/a2d44749-0c41-4993-bb62-0854cb2ec6e4)
   <br>
   ![properties](https://github.com/user-attachments/assets/023674c4-5f49-49d5-b991-f9eaafea9ca0)
   <br>
   ![ipv4 section](https://github.com/user-attachments/assets/89bb93ce-6a62-4821-b5ae-fb5bb22db61d)
   <br>
3. Click use the following IP to assign static IP Preffered DNS should point to our primary Domain Controller. 
   <br>
   ![ipv4 static ip](https://github.com/user-attachments/assets/b261a952-5214-4705-9d6f-83fc3a0f5c5e)

### Step 3: Install Active Directory Domain Services (AD DS)
1. Open Server Manager → Add Roles and Features

2. Choose:

* Active Directory Domain Services

* DNS Server

3. Click Next → Install

4. Wait for the installation to complete.

5. Select Internet Protocol Version 4 (TCP/IPv4) → Properties

### Step 4: Promote Server to Domain Controller
1. In Server Manager, click the flag ⚑ notification → “Promote this server to a domain controller.”

2. Choose Add a new forest

3. Set the root domain name: int.justy.com
4. Assign a Directory Services Restore Mode (DSRM) password.
5. Accept defaults for paths and DNS options.
6. Continue → Install.

The server will automatically restart after promotion.

### Step 5: Install and Configure DHCP
1. Open Server Manager → Add Roles and Features
2. Install the DHCP Server role.
3. After installation, open DHCP Management Console.
4. Create a new scope inside IPv4
   <br>
   <img width="421" height="469" alt="image" src="https://github.com/user-attachments/assets/1e1a7621-a795-4389-8e1f-87acde2720e0" />

### Verification
![getaddomain verification](https://github.com/user-attachments/assets/0f936ece-3fd9-4183-b21c-a484c5a5f9b1)
![dhcpscope verificaiton](https://github.com/user-attachments/assets/87106d6a-e643-4558-9147-f91b56418c4f)
![getwindowfeaturead verification](https://github.com/user-attachments/assets/1ab560a2-e5d1-43fa-bb88-ce607e68f472)
<img width="991" height="523" alt="image" src="https://github.com/user-attachments/assets/580cb5af-ae2b-4cdb-8d7e-881b7044f922" />

### Some Issues that Occurred and how I Fixed it
#### NAT instead of NAT Network
At first, the VM network was set up as NAT and not NAT Network. The domain controller and client VM shared the same IP address. I fixed it by changing the network to NAT Network.

#### Can't ping to Client VM
The domain controller could not ping to the Windows 10 Client machine. I used ipconfig and found out that the defualt gateway was blank. Then I enabled ICMP on the client after I found out that it was disabled by default due to security concerns.

### Lesson Learned
* internal use domains should have int after the domain name as the ones without it are generally used for public use.
* Always configure static IP before promoting to a domain controller.
* Use your DC’s IP as the DNS server, never external ones.
* After promotion, the local Administrator becomes the Domain Administrator.
* Save your DSRM password securely — it’s needed for AD recovery.
* A clean AD DS + DNS installation ensures seamless domain joins later.
