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

## 📌 Table of Contents
* [1. Infrastructure Architecture](#1-infrastructure-architecture)
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

### Note: If, at any point, your cursor inside a Machine dissapears and nothing you do brings it back, either power off the machine, or send the shut down signal.

## Step-by-Step Deployment Guide

<a name="phase-1"></a>
<p align="right"><a href="#phase-2">⬇️ Next phase</a></p>  

### Phase 1: Preparing the Installation Media

1. Open the **Windows Media Creation tool**, run through the initial setup prompt, and accept the default license terms.  
<img width="401" height="356" alt="ADHL-1" src="https://github.com/user-attachments/assets/28af53e7-2818-4134-8d07-cf8e54f2ae7e" />
  
2. When prompted, select **Create installation media (ISO file)**. This ensures the hypervisor can mount the operating system installer directly as a virtual disc image.  
<img width="401" height="356" alt="ADHL-2" src="https://github.com/user-attachments/assets/4eed3808-7860-4309-a4a5-6f8a5295c17d" />  

<a name="phase-2"></a>
  
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

<a name="phase-3"></a>

### Phase 3: Initial Boot(Client configuration)

8. Before the first boot, we must go into the settings and **disable the Network Adapter**. This forces Windows to skip signing signing in to a Microsoft account, instead we opt to create a local account.
  
<img width="578" height="331" alt="ADHL-10" src="https://github.com/user-attachments/assets/677d5e93-abb9-4373-9d0a-e05629f6c070" />

9. **Leave as default, next.**
   
<img width="313" height="237" alt="ADHL-11" src="https://github.com/user-attachments/assets/cb32f891-870e-46b2-9831-33ddd580545e" />

10. We do not have a **product key**, so we will choose that option.

<img width="322" height="232" alt="ADHL-12" src="https://github.com/user-attachments/assets/e3cfbacd-01c4-4a12-97f4-7bdfa8800c41" />

11. **This is important**. We must install Windows 10 Pro to have the ability to connect to our dc-01 server.

<img width="323" height="234" alt="ADHL-13" src="https://github.com/user-attachments/assets/424b6103-29e0-4825-93b1-ce7b3ba35740" />

12. We will install **Windows only**.

<img width="323" height="245" alt="ADHL-14" src="https://github.com/user-attachments/assets/b504fd31-d453-4489-8db3-cbd19a0ec139" />

13. **Leave as default, next.**

<img width="326" height="245" alt="ADHL-15" src="https://github.com/user-attachments/assets/9a1ea1ea-936b-4a49-9cb6-372f87b3ce0c" />

15. Windows will now Install, it will take a while. Grab a coffee and let it do its' thing.

<img width="323" height="243" alt="ADHL-16" src="https://github.com/user-attachments/assets/d061cd6c-e1bc-4a92-99b4-05c43cc32895" />

15. Choose your region, this does not impact lab functionality.

<img width="520" height="341" alt="ADHL-17" src="https://github.com/user-attachments/assets/82305e10-284a-4bea-88dc-63d292234d1d" />

16. Choose your keyboard layout.

<img width="513" height="340" alt="ADHL-18" src="https://github.com/user-attachments/assets/55a25e87-4a52-4955-81b9-37fe99a21fe7" />

17. Skip or add a layout.

<img width="511" height="336" alt="ADHL-19" src="https://github.com/user-attachments/assets/cf2b8874-e998-49d5-a86b-af6a37888710" />


18. **This is important.** You must select "I don't have Internet." 

<img width="515" height="240" alt="ADHL-20" src="https://github.com/user-attachments/assets/4b1d369f-2d7a-4b20-b7ec-0453b5b53a59" />

If that option is not available, you must disable the NIC. You can do this buy shutting down the machine through **File > Close > Power off the machine**. Once the machine is powered down open the settings cog just like Phase 3 step 8, navigate to Network, and disable the NIC. This **will not** restart the entire process**, you will be brought back to the screen at Phase 3: Step 8.

<img width="517" height="388" alt="ADHL-21" src="https://github.com/user-attachments/assets/f869472f-9028-4a20-a065-1f74000035a6" />

19. **Continue with limited setup again**.

<img width="516" height="388" alt="ADHL-22" src="https://github.com/user-attachments/assets/e2cd6984-edf9-4259-9bd9-c2653f678630" />

20. Set the name of your local account.

<img width="515" height="339" alt="ADHL-23" src="https://github.com/user-attachments/assets/6dd4ca37-d2a5-444a-8d9e-457574e2e133" />

21. Set the **SECURE** password of your local account. I will be following NIST standards. Example: Spouse Truck Mars Gallop https://pages.nist.gov/800-63-3/sp800-63b.html

<img width="512" height="335" alt="ADHL-24" src="https://github.com/user-attachments/assets/cb5a00f9-b36e-4c51-bfcb-f44ccd0cd193" />

22. Answer 3 **security questions** that you know by heart.

<img width="513" height="338" alt="ADHL-25" src="https://github.com/user-attachments/assets/15da8d27-7583-40d5-9dc6-78c165af3a80" />

23. Turn **all of this off**, then accept.

<img width="512" height="338" alt="ADHL-26" src="https://github.com/user-attachments/assets/87973d9f-ca31-4112-bf97-9f9be474d4c2" />

24. **Decline this.**

<img width="513" height="388" alt="ADHL-27" src="https://github.com/user-attachments/assets/262d092d-ff4f-4ae5-83b5-0844cfc2dacd" />

25. Let it do its' thing for a few minutes.

<img width="512" height="383" alt="ADHL-28" src="https://github.com/user-attachments/assets/3354471f-4988-4c07-96f4-dfbdcdc9720b" />

26. We are now *done with our client work station. Fully shut down the machine.

<img width="513" height="384" alt="ADHL-29" src="https://github.com/user-attachments/assets/76f6f467-ff33-4628-86af-051fa7088e0f" />

<a name="phase-4"></a>

### Phase 4: Initial Boot(Domain configuration)

27. Before starting dc-01, disable the NIC just like we did in Phase 3: step 8.

28. Start dc-01, click **next and "Install**."
<img width="508" height="385" alt="ADHL-30" src="https://github.com/user-attachments/assets/77cd05d7-e0cf-4417-a540-81a953b55e96" />

29. **This is important.** Select Windows Server 2019 Standard Evaluation (**Desktop Experience**.) Then, next.

<img width="513" height="386" alt="ADHL-31" src="https://github.com/user-attachments/assets/0c91e71e-8182-49ad-870c-7fb3429d996a" />

30. **Accept the terms**, then next.

<img width="511" height="382" alt="ADHL-32" src="https://github.com/user-attachments/assets/87e51866-33b8-4960-b362-90187805fb6e" />

31. Choose **Custom: Install Windows Only (advanced)**

<img width="508" height="383" alt="ADHL-33" src="https://github.com/user-attachments/assets/dccebf94-cf48-4326-bb4b-75b2c243b287" />

32. Verify you see only **one drive**, next.

<img width="511" height="336" alt="ADHL-34" src="https://github.com/user-attachments/assets/455976ce-83bd-465d-89f6-583dd5f1ebd9" />

33. Let it do its' thing for a few minutes.

<img width="520" height="386" alt="ADHL-35" src="https://github.com/user-attachments/assets/67e446c7-2703-475f-be74-6f1ecbe3e844" />

Note: **After installation** I actually ran into a crash and hit "OK" to terminate the program. Then, I was able to start the machine with no problem.

34. We will now **set the Administrator password.** However, once our Active Directory Domain is set up in the future, we will not be utilizing a single Administrator account for management of our Domain. This is in line with two major Information Security concepts Principle of Least Privelage, and Seperation of Duties. This is also called hardening, and will be in a seperate guide.

<img width="510" height="383" alt="ADHL-36" src="https://github.com/user-attachments/assets/fd5691fe-3aa9-49ea-a060-c66ca17a781c" />

Note: If you are using the minimum allocated resources you may experience sudden and severe lag on the following login screen and Desktop. This is normal, and will dissipate shortly. 

35. To login we have three options. 1.) On your keyboard press Ctrl(Host key combo) + Del. Ctrl is the default Host key combo. You can change this in **File > Preferences > Input > Virtual Machine > Host Key Combo** 2.) **Input > Keyboard > Insert Ctrl-Alt-Delete** 3.) **Input > Keyboard > Soft Keyboard > Click on Ctrl + Alt + Delete (Not backspace)** If your keyboard does not have the ability to press these key combos, you should change your Host Key combo. 

<img width="510" height="385" alt="ADHL-37" src="https://github.com/user-attachments/assets/96aed23f-b105-43cf-911c-1507fe719e85" />

36. Completely shut down Windows or the Machine (**File > Close > Send the shutdown signal**) Do not save the Machine state.

### Phase 5: Server Configuration

37. From the Machines screen where your dc-01 and wk-01 are listed, click the Network menu. All of the icons look the same, it is the third one up, fifth down.

<img width="527" height="473" alt="ADHL-39" src="https://github.com/user-attachments/assets/e176ea0a-3db3-43d8-a137-cf43f46da242" />

38. Click NAT Networks.

<img width="512" height="397" alt="ADHL-40" src="https://github.com/user-attachments/assets/69c4beb3-a3d4-4d95-9887-3a374e7b404e" />

39. Click create and then fill out and verify the following details:  
Name: Enterprise_NAT  
IPv4 Prefix: 10.10.10.0/24  
- [ ] Enable DHCP (Leave unchecked)
  
<img width="928" height="443" alt="ADHL-41" src="https://github.com/user-attachments/assets/67b903a3-5f1c-44e6-9204-e2e44d7357d7" />

40. Navigate back to dc-01 and open **Settings > Network > Adapter 1 >**  
✅ Enable Network Adapter  
Attatched to: NAT Network  
Name: Enterprise_NAT  
Adapter Type: **Ignore**  
Promiscous Mode: Deny  
MAC Address: **Ignore**  
Virtual Cable Connected: ✅  
  
Do the exact same thing for wk-01.  

41. Start dc-01 and login.

42. We will now configure the proper IPv4 Settings. **Right click on the Windows icon > Network Connections > Change Adapter Options > Right click Ethernet > Properties > Double click Internet Protocol Version 4 (TCP/IP)**

<img width="511" height="366" alt="ADHL-42" src="https://github.com/user-attachments/assets/40dfaa33-0ef0-414c-bd92-201feed918ea" />

<img width="1020" height="725" alt="ADHL-43" src="https://github.com/user-attachments/assets/50fdefd9-04cb-4b05-9053-1bb56b8bfb20" />


**Use the following IP address:**
- IP Address: 10.10.10.10
- Subnet Mash: 255.255.255.0
- Default Gateway: 10.10.10.1

**Use the following DNS server addresses**
- Preferred DNS Server: 10.10.10.10

✅ *Validate Settings upon exit!*

43. Now we will set up Active Directory. **If you don't see Server Manager** search for it on the Windows search bar.  
Note: I recommend you pin Server Manager to the task bar so it's easier and faster to access.  

**Manage > Add roles and features**
Only pay attention to the following:  
- Installation type: Role-based or feature-based installation
- Server Roles: A.) Active Directory Domain Services B.) DNS Server
- **Confirmation > Install**
<img width="1018" height="765" alt="ADHL-44" src="https://github.com/user-attachments/assets/f405eace-e74f-4afd-a0fa-de0f51da9d74" />
  
Your window should look as below, and it should say "Configuration required. Install succeeded on WIN-X."

<img width="787" height="704" alt="ADHL-45" src="https://github.com/user-attachments/assets/3b6553f5-4c75-499d-8da1-bbfb509072ef" />

44. In the server manager window there should be a flag with a yellow warning triangle on it. Click it then click "Promote this server to a domain controller."

45. Select "add a new forest" and enter the root domain name of: Enterprise.com

<img width="757" height="552" alt="ADHL-46" src="https://github.com/user-attachments/assets/901c6369-1f83-4bfe-8a3e-893f6964eeae" />

46. Next, then create a new password when prompted. This is different then the password we used login to dc-01. It is used for Domain maintnence purposes. Next.

<img width="757" height="555" alt="ADHL-47" src="https://github.com/user-attachments/assets/3462ce9a-5b32-4639-b617-f51e2416c568" />

47. Next, until you see an install button. There will be a bunch of warnings. Ignore these. Install.

<img width="757" height="555" alt="ADHL-48" src="https://github.com/user-attachments/assets/24b62761-6b4f-4b70-ae4f-f7ab988fecc6" />

48. It will prompt you that the computer will restart because Active Directory Domain was installed. The computer will restart and then it will load for a long time on boot.

<img width="757" height="555" alt="ADHL-48" src="https://github.com/user-attachments/assets/9bc49e0c-dd50-4758-8592-d3c97f003edb" />

49. Log back in to dc-01 then open the server manager and then **tools > Group Policy Management + Active Directory Users and Computers**. Pin to the task bar, both of the windows that open, for easier access. Then in tools, open DNS.

50. Right click WIN-XXXX and navigate to "Forwarders".

<img width="750" height="522" alt="ADHL-49" src="https://github.com/user-attachments/assets/587534a4-921a-444c-beb9-a7c19f02e12e" />

51. Click edit, then type in "8.8.8.8" (Google's public DNS) to the blank bar and then click "Ok." It will take a few seconds to verify.

<img width="750" height="527" alt="ADHL-50" src="https://github.com/user-attachments/assets/02eb9028-9709-4873-a885-37ed1fe59b2d" />

### Phase 6: Joining the Domain

52.  We will now run the initial setup of wk-01.
    
53. **Important, run the wk-01 Machine while dc-01 is still running.** This is so we can join wk-01 to the Domain Enterprise.com. Since we completed Phase 5: Step 40, we don't need to change the VirtualBox Adapter 1 settings again.

54. When prompted turn off all privacy settings then accept.

55. You should now be logged in. Just like Phase 5: Step 42, modify the IPv4 to the following manual settings:

<img width="1020" height="772" alt="ADHL-51" src="https://github.com/user-attachments/assets/59e255ab-558e-4635-aa1d-f3b5a0b85335" />

56. In the Windows search bar type "Advanced System Settings" and open the control panel. Go to **Computer name > Change > Domain > ENTERPRISE > set this computer's name to wk-01** Then click "Ok" and enter the credential when prompted. The username is Administrator by default.

<img width="1025" height="765" alt="ADHL-52" src="https://github.com/user-attachments/assets/778003b3-571e-49c7-b58c-daa8f2436c40" />

Once you get the confirmation message you will be prompted to restart multiple times. Restart now to apply changes.  
You will now have the option to login as "Other User" to ENTERPRISE.  

### Phase 7: Creating our first Employee Account

57. We will now go back to dc-01 and open "Active Directory Users and Computers" from our taskbar since we pinned it in Phase 5: Step 43.

58. Double click on "Active Directory Users and Computers" then navigate to **Enterprise.com > Users > Right click > New > User**
Fill out your own version of the following information. To simulate an enterprise setting, your logon name should be in the format of first letter of first name + last name.

<img width="1020" height="765" alt="ADHL-55" src="https://github.com/user-attachments/assets/7c01fa04-b0b6-4f36-a5ea-ca54314c9c1e" />

59. Next, we will set the password. First, uncheck "User must change password at next logon." Then, check "User cannot change password." This reduces human error, as we will assign the user our own password.

60. Remember to write down all passwords or store them in a secure place for only your eyes. Finish, then go back to wk-01.


<img width="1020" height="770" alt="ADHL-56" src="https://github.com/user-attachments/assets/25d93a14-9d0a-4454-bc7a-ae561c4b73ee" />

61. Navigate to "other user" then login to the account we just created. It will load for a few minutes then you will arrive at the desktop.

Congratulations, you now have the foundations of a legit IT deployment in Active Directory at your disposal. 



<a name="bottom"></a>  
  
<p align="right"><a href="#top">⬆️ Top of page</a></p>  
