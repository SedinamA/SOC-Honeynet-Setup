# SOC & Honeynet Setup in Azure (Live Traffic)
![image](https://github.com/SedinamA/SOC-Honeynet-Setup/assets/146953803/651f008c-fbe9-44d8-87d3-44af7f94df19)

## Introduction

During this project, I built a honeynet in Microsoft Azure and ingested log sources from various resources into a Log Analytics Workspace; the logs were then used by Microsoft Sentinel to build attack maps, trigger alerts, and create incidents. I then measured some security metrics in the insecure environment for 24 hours. Once that period( insecure 24 hours) ended I applied some security controls to harden the environment and then measured those same metrics for another 24 hours. Below are the results of the lab project. 
- SecurityEvent (Windows Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Set-up Before Hardening / Security Controls
![image](https://github.com/SedinamA/SOC-Honeynet-Setup/assets/146953803/a237d1d5-d61b-4932-8c32-cdd8093e5fad)

## Set-up After Hardening / Security Controls
![image](https://github.com/SedinamA/SOC-Honeynet-Setup/assets/146953803/94cdb020-cf84-4a36-b358-3c3def79d1b7)

The architecture of the honeynet in Azure consists of the following components:

- Virtual Network
- Network Security Group (NSG)
- Virtual Machines (2 Windows, 1 Linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

# Note
-Metrics Before Hardening:

All resources were originally deployed and  exposed to the internet. The Virtual Machines had both of their Network Security Groups and built-in firewalls wide open. All the other resources were deployed with public endpoints visible to the internet (no use for Private Endpoints).

-Metrics After Hardening:

Network Security Groups were hardened by blocking all traffic with the exception of my admin workstation, and all other resources were protected by tier built-in firewalls as well as Private Enpoints.

## Attack Maps Before Hardening / Security Controls
![image](https://github.com/SedinamA/Vulnerability-Management/assets/146953803/0ebabbc5-b807-4f9d-9be9-98498d9ec069)
![image](https://github.com/SedinamA/Vulnerability-Management/assets/146953803/2f0a3b19-1668-4e88-ab2a-7f8fe931afd2)
![image](https://github.com/SedinamA/Vulnerability-Management/assets/146953803/ed385c9a-a9c2-4927-ad14-7657bfa6bbca)
![image](https://github.com/SedinamA/Vulnerability-Management/assets/146953803/c342327c-0644-45d8-bbc4-68d1c4a58564)





## Metrics Before Hardening / Security Controls

The following table shows the metrics measured in the insecure environment for 24 hours:

Start Time 2024-01-05 13:43:34

Stop Time 2024-01-06 13:43:34


| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 94815
| Syslog                   | 6546
| SecurityAlert            | 7
| SecurityIncident         | 549
| AzureNetworkAnalytics_CL | 27649

## Attack Maps After Hardening / Security Controls

```All map queries returned no results due to no instances of malicious activity during the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics measured in the environment for another 24 hours after security controls were applied:

Start Time 2024-01-07 13:43:07

Stop Time 2024-01-08 13:43:06

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 10848
| Syslog                   | 24
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion
In this project, a mini honeynet was constructed in Microsoft Azure, and log sources were ingested into a Log Analytics workspace. Microsoft Sentinel was then used to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied; these metrics were then measured again after implementing security measures. It is important to note that the number of security events and incidents reduced significantly after the security controls were applied; demonstrating their effectiveness.

