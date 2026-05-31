# Active Directory & Client VM Lab Setup

## Overview
This repository contains a comprehensive, step-by-step walkthrough for building a functional Active Directory (AD) environment from scratch using virtual machines. This project demonstrates core identity management, network configuration, and systems administration skills essential for IT and cybersecurity roles. It serves as a practical, hands-on guide for anyone looking to gain experience with Windows Server administration and network topology containment.

## Infrastructure Architecture
The lab environment consists of two primary components configured within an isolated virtual network to simulate a secure corporate perimeter:

| Asset / Role | Hostname (Recommended) | Operating System | Network Configuration | Core Services |
| :--- | :--- | :--- | :--- | :--- |
| **Domain Controller** | `lab-dc01` | Windows Server 2019 | Static IP (`172.16.0.1`) | AD DS, DNS |
| **Client Workstation** | `lab-cl01` | Windows 10 Pro | Static IP (`172.16.0.2`) | Domain Member |

## Key Skills Demonstrated
* **Virtual Networking:** Configuring internal/host-only networks to ensure isolated, secure communication between VMs.
* **Windows Server Management:** Deploying Windows Server 2019 and promoting the asset to a functional Domain Controller.
* **DNS Infrastructure:** Setting up internal DNS zones, root hints, and forwarders for local name resolution.
* **Identity & Access Management (IAM):** Structuring Organizational Units (OUs), provisioning domain user accounts, and implementing secure workstation domain-join procedures.

---

## Prerequisites & Lab Assets

### Direct Download Links
* [Oracle VirtualBox Hypervisor](https://www.virtualbox.org/)
* [Windows 10 Media Creation Tool](https://www.microsoft.com/en-us/software-download/windows10)
* [Windows Server 2019 Evaluation ISO](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2019)

### Expected File Matrix
| File Name | Description / Role |
| :--- | :--- |
| `MediaCreationTool_22H2.exe` | Windows 10 Installation Media Builder |
| `VirtualBox-7.2.8-xxxxxx-Win.exe` | Type-2 Hypervisor |
| `17763.3650...SERVER_EVAL_x64FRE_en-us.iso` | Windows Server 2019 Target Image |

---

## Step-by-Step Deployment Guide

### Phase 1: Preparing the Installation Media

1. Open the **Windows Media Creation tool**, run through the initial setup prompt, and accept the default license terms.  
<img width="401" height="356" alt="ADHL-1" src="https://github.com/user-attachments/assets/28af53e7-2818-4134-8d07-cf8e54f2ae7e" />
  
2. When prompted, select **Create installation media (ISO file)**. This ensures the hypervisor can mount the operating system installer directly as a virtual disc image.  
<img width="401" height="356" alt="ADHL-2" src="https://github.com/user-attachments/assets/4eed3808-7860-4309-a4a5-6f8a5295c17d" />  
  
### Phase 2: Hypervisor Configuration
  
3. Install **VirtualBox**, leaving all installation options as default. Upon launching the application, select **Expert Mode** when creating a new virtual machine to gain granular control over resource allocation and hardware mapping. 
  
*(If the Expert Mode toggle is not visible on the main screen, navigate to **File > Preferences**.
  
4. Create a **"New" Virtual Machine** using the button at the top left. Verify your window matches the screenshot below. In this guide we are skipping guest additions.
  
<img width="500" height="350" alt="ADHL-4" src="https://github.com/user-attachments/assets/6d1009c3-71f5-4795-924d-416ea24520ee" />  
  
5. Set the **virtual hardware**. In this guide we will be going with the minimum allocation of resources. The reccomended minimum is 2000MB(2Gb) & 2 CPUs. However, for a greater balance between performance and optimization 4000MB(4Gb) & 4 CPUs should be allocated per Machine. Feel free to set it to anything within YOUR green bar. Exceeding the green bar on your screen will result in your Host System fighting for resources with the Virtual Machine, causing major issues.
  
<img width="1530" height="403" alt="ADHL-5" src="https://github.com/user-attachments/assets/99d5a81e-047a-4b92-9d28-2b4948664e29" />
  
6. **Set the virtual hard disk**. Do not pre-allocate the full size, unless you have extensive storage capacity avaiable. We will be using the VDI (VirtuaBox Disk Image), as it is the simplest and most seamless storage format. *Click finish.*
  
<img width="758" height="345" alt="ADHL-6" src="https://github.com/user-attachments/assets/bccf9baf-c0ed-4c95-a28b-abe5c6b9434d" />
  
7. **Adding the 2nd Machine.** We will name this machine wk-01, which follows the exact same standards at dc-01.

<img width="661" height="155" alt="ADHL-7" src="https://github.com/user-attachments/assets/2e8e2b4c-3843-4146-b1fd-701598da639b" />

<img width="661" height="136" alt="ADHL-8" src="https://github.com/user-attachments/assets/599acf42-4568-49a1-bab1-03aae437fccc" />

<img width="661" height="149" alt="ADHL-9" src="https://github.com/user-attachments/assets/7309eeab-b3d7-44ce-92c2-8f01bc8bf6f9" />

### Phase 3: Initial Boot & OS Initialization

8. 
