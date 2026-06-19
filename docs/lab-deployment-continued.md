### Lab etc.

[![Return to Part 1](https://img.shields.io/badge/Return_To-Part_1:_Lab_Deployment_Guide-666666?style=for-the-badge&logo=github&logoColor=white)](lab-deployment-guide.md)

<a name="top"></a>
<p align="right"><a href="#bottom">⬇️ Bottom of Page</a></p>  

### Quick Summary

This is part 2 of the lab which covers the post-setup configuration of Active Directory. Including but not limited to NTFS file sharing, Organizational Units by department, groups, Group Policy Objects, and other hardening strategies.

## 📌 Table of Contents
* [1. WIP.../all](#1-infrastructure-architecture)
* [2. Key Skills Demonstrated](#2-key-skills-demonstrated)
* [3. Prerequisites & Lab Assets](#3-prerequisites--lab-assets)
* [4. Deployment Guide](#step-by-step-deployment-guide)
  * [Phase 1: Preparing the Installation Media](#phase-1-preparing-the-installation-media)
  * [Phase 2: Hypervisor Configuration](#phase-2-hypervisor-configuration)
  * [Phase 3: Initial Boot (Client configuration)](#phase-3-initial-bootclient-configuration)
  * [Phase 4: Initial Boot (Domain configuration)](#phase-4-initial-bootdomain-configuration)
  * [Phase 5: Server Configuration](#phase-5-server-configuration)
  * [Phase 6: Joining the Domain](#phase-6-joining-the-domain)
  * [Phase 7: Creating our first Employee Account](#phase-7-creating-our-first-employee-account)

### Note: If, at any point, your cursor inside a Machine dissapears and nothing you do brings it back, either power off the machine, or send the shut down signal. Then log back in, this should fix it. Otherwise, change your pointer method in Settings > System > Pointing Device

## Step-by-step Configuration Guide

### Pre-configuration

Before continuing, take snapshot images of both machines through Machine > Take Snapshot. Label it pre-lab 2 and fill in the description with whatever you like. This is just in case we do something wrong or want to undo changes. We can load up a previous "save" of the Machines.

<a name="phase-1"></a>
<p align="right"><a href="#phase-2">⬇️ Next phase</a></p>  

### Phase 1: OUs

1. Open server manager like how we pinned it to the taskbar earlier, navigate to Tools > Active Directory Users and Computers. Expand Enterprise.com and Right Click > New Organizational Unit > and name each OU as follows:

```
└── 📂 LHO/
    ├── 📂 Computers/
    │   ├── 📂 Branch
    │   ├── 📂 Headquarters
    │   └── 📂 Remote
    ├── 📂 Groups/
    ├── 📂 Servers/
    ├── 📂 Service Accounts/
    └── 📂 Users/
        ├── 📂 Admin_users
        ├── 📂 HR_Users
        ├── 📂 IT_Users
        └── 📂 Sales_Users
```
















<a name="bottom"></a>  
  
<p align="right"><a href="#top">⬆️ Top of page</a></p>  

