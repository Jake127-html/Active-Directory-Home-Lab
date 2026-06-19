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

1. Open server manager like how we pinned it to the taskbar earlier, navigate to Tools > Active Directory Users and Computers. Expand Enterprise.com and Right Click > New Organizational Unit > Make sure protect from accidental deletion is enabled! And name each OU as follows:

```
Enterprise.com
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

Note: LHO is directly under the Domain.

<img width="522" height="204" alt="ADHL-60" src="https://github.com/user-attachments/assets/0da43af0-56ba-4e60-9612-cb2e6249f396" />  
  



  
<img width="397" height="907" alt="ADHL-59" src="https://github.com/user-attachments/assets/a1cc71ff-dffa-4080-96f8-bf475ed68408" />  

2. We're going to create our first batch of users. Open Users > Admin Users > Right Click > New > User > Create 2 Admin Users of your choice. The name can be anything but the logon names must be in the format of firstname.lastname(larry.bird, tim.cook, michael.jackson) & flast(first name initial and last name(lbird, tcook, mjackson.)
  
**Note**: Verify NO boxes are check marked.  The password must be at least 11 characters following NIST standards.
  
  
<img width="437" height="377" alt="ADHL-61" src="https://github.com/user-attachments/assets/fbc0f7f5-d086-4452-aa02-25401012f604" />

<img width="432" height="377" alt="image" src="https://github.com/user-attachments/assets/4a120bc9-cc07-4ed8-a81a-8cf884cc471a" />

Now do the same thing for the other user directories and make 3-4 users per.


<img width="940" height="456" alt="image" src="https://github.com/user-attachments/assets/93f2e43b-20a7-4655-8506-b7c5fc2cd64c" />








<a name="bottom"></a>  
  
<p align="right"><a href="#top">⬆️ Top of page</a></p>  

