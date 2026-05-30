# Active Directory & Client VM Lab Setup
  
## Overview
This repository contains a comprehensive, step-by-step walkthrough for building a functional Active Directory (AD) environment from scratch using two virtual machines. This project demonstrates core identity management, network configuration, and systems administration skills essential for IT and cybersecurity roles. Additionally, this project opens the doors to anyone looking to gain hands-on, practical experience in Active Directory and Windows Server.

## Infrastructure Architecture
The lab environment consists of two primary components configured within an isolated virtual network:

1. **Domain Controller (DC):** Running Windows Server 2019, hosting Active Directory Domain Services (ADDS), and acting as the DNS server for the local domain.
2. **Client Workstation:** Running Windows 10, configured with a static internal IP, and successfully joined to the newly created domain.

## Key Skills Demonstrated
* **Virtual Networking:** Configuring internal/host-only networks to ensure isolated, secure communication between VMs.
* **Windows Server Management:** Installing and promoting Windows Server to a Domain Controller.
* **DNS Configuration:** Setting up internal DNS forwarding and resolution.
* **User & Asset Management:** Creating Organizational Units (OUs), creating domain user accounts, and joining workstations to the domain.

### Prerequisites [Direct Download Links]  
[Oracle Virtualbox](https://www.virtualbox.org/wiki/Downloads) (Version 7.2.8 r173730)  
[Windows 10 Media Creation Tool](https://go.microsoft.com/fwlink/?LinkId=2265055)  
[Windows Server 2019](https://go.microsoft.com/fwlink/p/?LinkID=2195167&clcid=0x409&culture=en-us&country=US)  
*Host Software stability may vary*

<details>
  
<summary>Click to expand guide</summary>  
  
## Installation

1. Download Windows Server 2019, Windows Media Creation Tool, and Oracle Virtualbox. Keep them in an easy-acess directory.
  
| Files     | Description |
| ------------- | ------------- |
| MediaCreationTool_22H2.exe  | Windows 10 ISO |
| VirtualBox-7.2.8-173730-Win.exe  | Hypervisor |
| 17763.3650.221105-1748.rs5_release_svc_refresh_SERVER_EVAL_x64FRE_en-us.iso | Windows Server 2019 ISO |  
  
2. Open the Windows Media Creation tool, run through setup, and leave all options default.  
<img width="401" height="356" alt="ADHL-1" src="https://github.com/user-attachments/assets/28af53e7-2818-4134-8d07-cf8e54f2ae7e" />
  
2A. Create an ISO File, unless you're porting it to another PC, or not using a virtual machine.  
<img width="401" height="356" alt="ADHL-2" src="https://github.com/user-attachments/assets/4eed3808-7860-4309-a4a5-6f8a5295c17d" />  

3. Install Virtualbox, leave all options default. After install and when prompted, choose expert mode. If expert mode is not shown go to File > Preferences > Expert Mode (from the menu popup)    
  
<img width="415" height="420" alt="ADHL-3" src="https://github.com/user-attachments/assets/5e6ba048-ecef-4804-be95-26fd1346082b" />   
  
3A. If it says "Invalid Settings Detected" hover over the message to see what the problem is. You may have to manually create the "Default Machine Folder."
  
  
4. Click "New" and the "ISO Image" drop down to select your Windows Server 2019 ISO. Verify your Window matches the screenshot below. We will be skipping guest additions.
  
<img width="502" height="350" alt="ADHL-4" src="https://github.com/user-attachments/assets/dbad6faf-d5b8-4ef2-801d-8df6edcea448" />



















   
</details>
