# Active Directory & Client VM Lab Setup
  
## Overview
This repository contains a comprehensive, step-by-step walkthrough for building a functional Active Directory (AD) environment from scratch using two virtual machines. This project demonstrates core identity management, network configuration, and systems administration skills essential for IT and cybersecurity roles.

## Infrastructure Architecture
The lab environment consists of two primary components configured within an isolated virtual network:

1. **Domain Controller (DC):** Running Windows Server, hosting Active Directory Domain Services (ADDS), and acting as the DNS server for the local domain.
2. **Client Workstation:** Running Windows 10/11, configured with a static internal IP, and successfully joined to the newly created domain.

## Key Skills Demonstrated
* **Virtual Networking:** Configuring internal/host-only networks to ensure isolated, secure communication between VMs.
* **Windows Server Management:** Installing and promoting Windows Server to a Domain Controller.
* **DNS Configuration:** Setting up internal DNS forwarding and resolution.
* **User & Asset Management:** Creating Organizational Units (OUs), creating domain user accounts, and joining workstations to the domain.
