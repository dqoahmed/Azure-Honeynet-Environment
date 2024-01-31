
# Setting up a cloud Honeynet environment in Azure Microsoft

## Introduction

In the prevous project I have deployed and created all the resourses needed in order to run the honey-net environment. In this project, I will perposefully configure our honey-net security system in the virtual machines, network resource groups and other end points to be vulnurable and exposed to the internet where all inbound traffic is able to jsut easly come throuth our network. I'll Run the insecure environment for 48 hours and then capture the analytics that the Security Information and Event Management (SIEM) system generates. After that ill apply security controls to harden the environment. I will be using the following security metrics to compare the before and after of the honey-net environment.

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Honey-Net evnvironment components

In the previouse project, I have set up the Azure environment consisting of the following components:

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


## Azure Sentinal alerts (SIEM)

 analytics rules that define suspicious activity to trigger alerts 

![image](https://github.com/dqoahmed/Azure-Honey-Net-Proj/assets/156861134/53cec3ba-ea9a-4867-a407-74bac55388f5)

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

## Attack maps after hardening
after hardening the honey-net environment, attack maps didn't show any.

## Results of the system after hardenening

![image](https://github.com/dqoahmed/Web-Development/assets/156861134/2db16381-434c-4158-a391-e6b64a12e5b0)



## Summary:

The project involves setting up a cloud honeynet environment in Microsoft Azure. It includes creating essential resources such as virtual machines, key vaults, and storage. Azure Active Directory, log analytics, and a Security Information and Event Management (SIEM) system (Microsoft Sentinel) are configured.

The virtual network architecture comprises a Virtual Network (VNet), Network Security Group (NSG), and three virtual machines (2 Windows, 1 Linux). The goal is to establish a comparative analysis between the secure and insecure states of the environment.

Components like Azure Key Vault, Azure Storage Account, and Microsoft Defender are integrated. Users with specific roles are created in Azure Active Directory, following the principle of least privilege. Log Analytics workspace is set up as a central log repository, and Microsoft Sentinel is configured for security threat detection.

Logs are enabled for various components, including Azure Active Directory, subscription-level activities, and resource-level activities for storage and key vault. Analytics rules are created to trigger alerts for suspicious activities, such as consecutive failed logins.

The project aims to observe, analyze, and secure the environment, ultimately enhancing its resilience and security posture. It is part one of a two-part project
