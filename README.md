# Building a SOC + Honeynet in Azure (Live Traffic)
![Cloud Honeynet / SOC](https://i.imgur.com/ZWxe03e.jpg)

## Introduction

In this project, I build a mini honeynet within Azure, aggregating log data from different sources into a Log Analytics workspace. This workspace serves as the foundation for Microsoft Sentinel, enabling the creation of attack maps, alert triggering, and incident generation. To assess security, I captured metrics in the unsecured environment for 24 hours, implemented security controls to harden the environment, measured metrics for an additional 24 hours, and present the outcomes below. The metrics we will show are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/aBDwnKb.jpg)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/YQNa9Pp.jpg)

The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were originally deployed, exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources are deployed with public endpoints visible to the Internet; aka, no use for Private Endpoints.

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint

## Attack Maps Before Hardening / Security Controls

![Screenshot (273)](https://github.com/babsthetechguy/Cyber-Course/assets/150613649/1483f738-3e37-42da-a4c6-295bc65b423a)
![Screenshot (272)](https://github.com/babsthetechguy/Cyber-Course/assets/150613649/b80c84d8-b553-4b44-9c86-a60256b4c9da)
![Screenshot (270)](https://github.com/babsthetechguy/Cyber-Course/assets/150613649/cb419367-f82d-4be1-aefa-009052e80690)
![Screenshot (271)](https://github.com/babsthetechguy/Cyber-Course/assets/150613649/2ff8da7a-7ea5-4862-aacf-afb55b9ada19)


## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2024-02-01 18:17:43
Stop Time 2024-02-02 18:17:43

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 27257
| Syslog                   | 2818
| SecurityAlert            | 8
| SecurityIncident         | 241
| AzureNetworkAnalytics_CL | 3941

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2024-02-04 07:48
Stop Time	2023-03-05 07:48

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 4220
| Syslog                   | 127
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.
