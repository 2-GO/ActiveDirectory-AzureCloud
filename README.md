![what-is-active-directory-and-why-is-it-used](https://github.com/user-attachments/assets/0f3029d9-5013-4e7b-b6da-c2fa2a577e51)
# On-Premise Active Directory Deployed in Azure Cloud
Goal: Implement on-premise active directory within Azure VMs.

## Technology Used
- Microsoft Azure
- Remote Desktop
- Active Directory Domain Services
- PowerShell
- Windows Server
- Windows 11

## Steps and Documentation
1. Setup resources in Azure
2. Ensure connectivity between Client and Domain Controller
3. install Active Directory
4. Create an Admin and Normal user account in Active Directory
5. Join Client VM to your domain (mydomain.com)
6. Setup Remote Desktop for non-admin users on Client VM
7. Create one thousand users using powershell script and login using one of the created users credentials

## 1. Setup Resources in Azure
Establish the foundational infrastructure for an Active Directory environment by deploying a Windows Server 2022 domain controller (AD-DC) and a Windows 10 client machine (AD-Client) within the same Azure Virtual Network. Configure the domain controller with a static private IP address to ensure consistent network addressing for AD services, then verify proper network topology and connectivity between both VMs using Network Watcher to confirm they can communicate within the shared virtual network environment.
![ad_vm](https://github.com/user-attachments/assets/593df934-ae3c-4e90-aeae-560e03cbb654)
![static_DC](https://github.com/user-attachments/assets/28546357-8c93-41fe-bec5-d5f1df169d7a)

## 2. Ensure Connectivity Between Client and Domain Controller
Verify and establish network communication between the client and domain controller by initiating a continuous ping test from Client to DC private IP address. Resolve initial connectivity issues by configuring the Windows Firewall on the domain controller to allow ICMPv4 traffic, demonstrating how local firewall settings can block network communication even when Azure network security groups permit traffic.
![ping_dc](https://github.com/user-attachments/assets/f1dd8d60-dd44-4949-8275-0987037de2bd)
![pingdc_sucess](https://github.com/user-attachments/assets/5075011a-bcf6-4a38-9f48-5526555a554b)

## 3. Install Active Directory
Transform the Windows Server 2022 VM into a functional domain controller by installing Active Directory Domain Services and promoting it to establish a new forest with a custom domain name (mydomain.com). Complete the domain controller promotion process, which requires a system restart, then authenticate using the new domain administrator credentials to verify successful Active Directory installation and begin centralized network authentication services.
![ds_dc](https://github.com/user-attachments/assets/788fd6ca-bb3a-4f41-be5a-bf8b2f54efd7)
![newdomain_dc](https://github.com/user-attachments/assets/8c3115de-a6ea-498a-97d0-c66e38fdd3bc)

## 4. Create Admin and Normal User Account in Active Directory
Organize Active Directory structure by creating dedicated Organizational Units using Active Directory Users and Computers (ADUC). Establish proper administrative delegation by creating a new user account (jojo_admin) and elevating it to Domain Admin privileges, then switch to using this dedicated administrative account for all future domain management tasks.
![org_unit](https://github.com/user-attachments/assets/1ebc5d66-1e7b-483c-a102-a13852970142)
![admin_userdc](https://github.com/user-attachments/assets/842bb8a5-0422-4d2a-8e8e-87e7ae6926c8)
![admin_usergroupdc](https://github.com/user-attachments/assets/1beac8dd-73f5-4e40-899b-3be8c04a7958)

## 5. Join Client VM to Your Domain (mydomain.com)
Configure Client to join the Active Directory domain by setting its DNS to the domain controller’s private IP via the Azure Portal and restarting the VM. Log in to Client using local admin credentials and join it to the domain (mydomain.com), prompting another restart. Verify the successful domain join by confirming Client appears in the “Computers” container in Active Directory Users and Computers (ADUC). For organizational clarity, create a new OU named “_CLIENTS” and move Client into it.
![client_dnschangetodcprivateip](https://github.com/user-attachments/assets/27997a29-7869-4015-aab9-8c3bab0d07cb)
![client_changedomain](https://github.com/user-attachments/assets/ce94d31b-3aed-43b9-996e-0b9b8519d886)
![dc_admin_remotelogin](https://github.com/user-attachments/assets/23a458e6-59c3-456f-b9b6-4f80b30d7bcd)
![client_successful_addtdcserver](https://github.com/user-attachments/assets/6538e813-af4a-4e84-8cff-ecfdda46de2c)

## 6. Setup Remote Desktopfor Non-Admin Users on Client VM
Log into Client as the domain administrator (mydomain.com\jojo_admin) and enable Remote Desktop in the system properties. Grant “Domain Users” group access to Remote Desktop, allowing non-administrative users to remotely log in to Client.
![client_remote_settings](https://github.com/user-attachments/assets/66c50eb5-61b5-4950-b89f-0d689e722168)

## 7. Create One Thousand Users Using PowerShell Script and Login Using One of the Created User Credentials
![SCRIPT_RUNNING](https://github.com/user-attachments/assets/9fa69279-1705-4282-b02e-9e1b47f7027f)
![SCRIPT_USERRESULTS](https://github.com/user-attachments/assets/bfb1c04e-665b-4f64-860f-c25e7b758eb0)
![user_account_loginsuccess](https://github.com/user-attachments/assets/f62e268e-ceb3-4ea3-80e8-1e963a1d066b)


## Summary
This lab demonstrates the end-to-end setup of a basic Active Directory environment in Microsoft Azure. It includes deploying and configuring a domain controller and client machine, ensuring network connectivity, installing and managing Active Directory Domain Services, organizing users and computers using OUs, enabling Remote Desktop access for standard users, and automating bulk user creation via PowerShell. The final result is a functional, cloud-based domain environment that supports centralized authentication and remote access for domain users.


