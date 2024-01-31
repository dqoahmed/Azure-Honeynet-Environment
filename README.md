# Azure Honey-net 
# Setting up a Honeynet environment in Azure Microsoft

## Introduction
 In this project, my objective is to establish a cloud honeynet Environment within Microsoft Azure, encompassing the creation of essential resources such as virtual machines, key vaults, and storage. Subsequently, I will configure Azure Active Directory, implement log analytics, and integrate a Security Information and Event Management (SIEM) system.

The project involves the creation of user accounts with specific permissions, linking all resources to a centralized log repository within the log analytics workspace, facilitating log ingestion. This integrated system will then be connected to the SIEM to enable the triggering of alerts and generation of attack maps on the incident observation and investigation dashboard.

This is a part one (setting up the environment ) of a two part projec. The ultimate aim is to conduct a comparative analysis between the secure and insecure states of the environment, thereby enhancing its overall resilience and security posture.

Also, I installed SQL Server in Windows VM as another end point for people to attack. I exposed our network with the intent to observe our logs and secure them later. Then I added     another attack VM with separate network, location and resource group and installed SQL to attack the other VMs in order to generate and observe logs and then secure the environment for comparison.


## Honey-Net evnvironment components
The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

## Network resource group
 I configured the network resource group for both VMs to be vulnerable by modifying the inbound security rules on the network security group to accept anty traffic. 
 
   ![image](https://github.com/dqoahmed/Web-Development/assets/156861134/092b7c80-9481-4a53-ac05-3e95ac6b17a2)
  ![image](https://github.com/dqoahmed/Web-Development/assets/156861134/581e5a81-b1e5-431c-aa79-6f1a3d9e9e4d)

  
 ## Windows Firewall Defender
   Windows host firewall defender has been disabled
  ![image](https://github.com/dqoahmed/Web-Development/assets/156861134/d82415c0-bc3f-4644-9eff-b8c0c8bfeeed)


## sentinal alerts
after creating analytics rules that define suspicious activity to trigger alerts 
![image](https://github.com/dqoahmed/Azure-Honey-Net-Proj/assets/156861134/cc64781d-3cc7-48cd-95bd-d242c6b977dc)

 	**I run insecure Environment for 24 hours to capture analytics.**
     Two days after creating sentinel analytic rules, there are plenty of incidents reported. 
 	
 ![image](https://github.com/dqoahmed/Web-Development/assets/156861134/e933f61e-e16f-4f31-aa1b-c6c8a2d86f79)

  
## Trigerring alerts

 I generated high risk alerts by triggering AAD Brute force success, malware Outbreak(with a fake malware file), windows host firewall tampering, possible privilege escalation by viewing key Vault secret password and performing excessive password resets.

  ![image](https://github.com/dqoahmed/Web-Development/assets/156861134/01e975e5-1ada-4edf-898b-dccde21d85ab)


## Incident mapping and ivestigation 
 Another Visual representation of incidents in the investigation pannel
 
 ![image](https://github.com/dqoahmed/Web-Development/assets/156861134/81ef900b-44d9-4856-aa03-327854c554eb)
 ![image](https://github.com/dqoahmed/Web-Development/assets/156861134/16009069-f598-4aec-8f13-770ec66b4975)


## Attack maps before security controls are applied  

![image](https://github.com/dqoahmed/Web-Development/assets/156861134/5aa7ead7-4db9-463d-88f5-38c170b97d5b)
![image](https://github.com/dqoahmed/Web-Development/assets/156861134/f88a614f-fb98-4793-80c9-b3753ad37d09)
![image](https://github.com/dqoahmed/Web-Development/assets/156861134/a1c35147-6630-4cdc-8284-125926ae2cfa)

## The system events Before Hardening 
			
![image](https://github.com/dqoahmed/Web-Development/assets/156861134/9b32107e-e498-4570-8170-ee9132407c66)



## Apply security controls to harden the invironment

Hardened the Network resource group inbound security rules to filter out traffic

![image](https://github.com/dqoahmed/Web-Development/assets/156861134/095f5ae5-3720-429a-889f-6289261d35ed)

![image](https://github.com/dqoahmed/Web-Development/assets/156861134/e7473a73-a079-4e54-abf7-c0e7061517a1)

 ## Windows Firewall Defender
 
Updated the network security rules for virtual machine in the windows host firewall in response to the Brute force which were vulnerable and open to all of the internet traffic.

![image](https://github.com/dqoahmed/Web-Development/assets/156861134/ba6e61f8-34b8-4ab2-a7af-9484e2215ed5)


## Results of the system after hardenening

![image](https://github.com/dqoahmed/Web-Development/assets/156861134/2db16381-434c-4158-a391-e6b64a12e5b0)




  Setting up log analytics workspace which is a central log repository or log container for all applications and infrastructure which helps you collect, monitor, analyze, and query data.
  
  ![image](https://github.com/dqoahmed/Azure-Honey-Net-Proj/assets/156861134/f2f457b7-f45e-4e23-9c58-f56ecba0ee003f)

## Creating Microsoft Sentinel (SIEM) and uploading a watch-list

  Azure Sentinel is a Microsoft SIEM, that aids in detecting, investigating, and responding to security threats across enterprises. With advanced data collection, detection, seamless integration, and robust incident response tools.
  Now creating Microsoft Sentinel and connecting it to log analytics workspace. 

  ![image](https://github.com/dqoahmed/Azure-Honey-Net-Proj/assets/156861134/8986b80b-9ffb-4e91-8987-811cb1cec727)
  ![image](https://github.com/dqoahmed/Azure-Honey-Net-Proj/assets/156861134/03f8ee29-2bcc-419b-94f9-c4acbc538d33)

 

## Microsoft Defender
   Enabling Microsoft defender for cloud which allows us to collect all event logs from vms, subscriptions to forward them to the central repository log analytics workspace.
   ![image](https://github.com/dqoahmed/Azure-Honey-Net-Proj/assets/156861134/5cf2b470-8d8c-4759-8f4c-752b39a3e63f)

 
## Enabling log collection for VMs and network security groups

  Enabling flow logs for both Linux and Windows network security groups to forward log data to the central log workspace.
  
 ![image](https://github.com/dqoahmed/Azure-Honey-Net-Proj/assets/156861134/58a11530-3d6b-4443-a669-13b55383a92a)
 ![image](https://github.com/dqoahmed/Azure-Honey-Net-Proj/assets/156861134/0f219196-28b9-42dc-84c5-7926bb3c9610)
 
 ## Setting up logs for Azure Active Directory
 
  Setting up logs for Azure Active Directory will help us forward logs to the Log Analytics Workspace. After enabling audit and sign-in log for AAD, I’ll create a user, assign roles and play around with it to show audit log in Log    a analytics Workspace.
  
  ![image](https://github.com/dqoahmed/Azure-Honey-Net-Proj/assets/156861134/4cec27d0-9447-4c4b-800c-fca4d822cc63)
  ![image](https://github.com/dqoahmed/Azure-Honey-Net-Proj/assets/156861134/ddb26204-c7d6-4fc7-a003-90f6f122c92b)


 ## Enabling Loging and monitoring at the subscription level for the activity log
 
  Activating Loging and monitoring in the Azure monitor to export event activities that happen in the resources such as creating, deleting, and changing and who performed to log analytics workspace. I’ll create and delete resource 
  groups  to generate logs in the log analytics workspace. 
  
 ![image](https://github.com/dqoahmed/Azure-Honey-Net-Proj/assets/156861134/f4eb06ab-3dbb-4d09-b36c-4ba2d5df5d78)
 ![image](https://github.com/dqoahmed/Azure-Honey-Net-Proj/assets/156861134/c3401d2e-a03f-448a-a928-92d7e1b6bcb0)


## Enabling Loging and monitoring at the Resource level for storage and key vault

 Activating log collection for storage and key vault through diagnostics as part of our resources. I’ll upload a file to a container in the storage and edit then create secret passwords and view the passwords in the key vault to         generate logs in the log analytics.

![image](https://github.com/dqoahmed/Azure-Honey-Net-Proj/assets/156861134/c74e43f1-5ad3-43ee-9392-f8220a6fdaf5)
![image](https://github.com/dqoahmed/Azure-Honey-Net-Proj/assets/156861134/1b2c84f6-3c5f-48c4-9bd8-ecc7d6aaba26)
![image](https://github.com/dqoahmed/Azure-Honey-Net-Proj/assets/156861134/1ab6f5fb-c29b-4fe9-896f-e7632660d4ab)


## Sentinel

Building maps for VM authentication failures and network malicious flow in the workbook.
![image](https://github.com/dqoahmed/Azure-Honey-Net-Proj/assets/156861134/39647db5-e054-442a-afcb-332bb4caab52)


creating analytics rules that define suspicious activity to trigger alerts. This example rule gets triggered when 10 consecutive failed logins occur on windows VM
![image](https://github.com/dqoahmed/Azure-Honey-Net-Proj/assets/156861134/cc64781d-3cc7-48cd-95bd-d242c6b977dc)

Imported the rest of the analytics rules as a file
![image](https://github.com/dqoahmed/Azure-Honey-Net-Proj/assets/156861134/53cec3ba-ea9a-4867-a407-74bac55388f5)


## Summary:

The project involves setting up a cloud honeynet environment in Microsoft Azure. It includes creating essential resources such as virtual machines, key vaults, and storage. Azure Active Directory, log analytics, and a Security Information and Event Management (SIEM) system (Microsoft Sentinel) are configured.

The virtual network architecture comprises a Virtual Network (VNet), Network Security Group (NSG), and three virtual machines (2 Windows, 1 Linux). The goal is to establish a comparative analysis between the secure and insecure states of the environment.

Components like Azure Key Vault, Azure Storage Account, and Microsoft Defender are integrated. Users with specific roles are created in Azure Active Directory, following the principle of least privilege. Log Analytics workspace is set up as a central log repository, and Microsoft Sentinel is configured for security threat detection.

Logs are enabled for various components, including Azure Active Directory, subscription-level activities, and resource-level activities for storage and key vault. Analytics rules are created to trigger alerts for suspicious activities, such as consecutive failed logins.

The project aims to observe, analyze, and secure the environment, ultimately enhancing its resilience and security posture. It is part one of a two-part project
