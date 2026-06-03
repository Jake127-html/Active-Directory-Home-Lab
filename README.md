[![Run Lab](https://img.shields.io/badge/Run_Lab-Deployment_Guide-blue?style=for-the-badge&logo=virtualbox&logoColor=white)](docs/lab-deployment-guide.md)
  
<a name="top"></a>
<p align="right"><a href="#bottom">⬇️ Bottom of page</a></p>  
  
# Active Directory & Client VM Lab Setup

## Overview
This repository contains a comprehensive, step-by-step walkthrough for building a functional Active Directory (AD) environment from scratch using virtual machines. This project demonstrates core identity management, network configuration, and systems administration skills essential for IT and cybersecurity roles. It serves as a practical, hands-on guide for anyone looking to gain experience with Windows Server administration and network topology containment.

## Infrastructure Architecture
The lab environment consists of two primary components configured within an isolated virtual network to simulate a secure corporate perimeter:

| Asset / Role | Hostname (Recommended) | Operating System | Network Configuration | Core Services |
| :--- | :--- | :--- | :--- | :--- |
| **Domain Controller** | `dc-01` | Windows Server 2019 | Static IP (`10.10.10.10`) | AD DS, DNS |
| **Client Workstation** | `wk-01` | Windows 10 Pro | Static IP (`10.10.10.11`) | Domain Member |

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

<a name="bottom"></a>  
  
<p align="right"><a href="#top">⬆️ Top of page</a></p>  
