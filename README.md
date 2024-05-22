## BUILDING A LIVE SOC + HONEYNEY IN AZURE
This project demonstrates setting up and configuring a honeynet in Microsoft Azure. It includes creating virtual machines, configuring security settings, deploying a SQL database, and integrating Microsoft Sentinel for security monitoring and incident response.

![322930551-ca6ef315-dcbf-4176-b90f-c46a6bbf0459](https://github.com/sharpleynate/azure-soc-honeynet/assets/114451775/58958953-aa52-478b-ad4f-33a9e8d8027a)

## Step 1: Environment Setup
To begin, I initiate the setup by creating two virtual machines: one running on a Windows operating system and the other on Linux. These virtual machines are strategically placed within the same resource group, ensuring efficient management and allocation of resources. This approach facilitates streamlined monitoring, maintenance, and resource utilization across both platforms.

![Screenshot 2024-05-21 064824](https://github.com/sharpleynate/azure-soc-honeynet/assets/114451775/55970e93-5656-40fc-87c6-fabe5ff48f89)

## Step 2: Adjusting Network Security Groups (NSGs)
After deploying both VM instances, I proceed to the inbound security rules, specifically the Network Security Group (NSG), to remove the Remote Desktop Protocol (RDP) port restriction in order to gather information. I opt to allow 'any' inbound traffic temporarily, thereby opening up both Windows and Linux VMs to potential vulnerabilities. This decision grants unrestricted access to incoming traffic, which may pose security risks but enables comprehensive data collection and analysis.

![Screenshot 2024-05-21 070404](https://github.com/sharpleynate/azure-soc-honeynet/assets/114451775/a572a69c-bd69-45f6-b639-1db69627a2fa)

## Step 3: Disabling Windows Firewall
I start by pinging the public IP of my Windows VM to verify whether the firewall is still enabled. Upon confirming its status, I proceed to disable the firewall. This action is taken to ensure unhindered communication and accessibility to the Windows VM, facilitating seamless interaction and troubleshooting as needed.

![Screenshot 2024-05-21 070652](https://github.com/sharpleynate/azure-soc-honeynet/assets/114451775/3bd230c2-94c6-42ba-8a1d-6ccaa6a61b3e)

## Step 4: Accessing Windows VM via Remote Desktop
I achieve this by accessing the Windows VM through Remote Desktop. This remote connection enables me to interact with the VM's desktop interface directly, allowing me to make necessary adjustments, such as disabling the firewall, in a convenient and efficient manner.

![Screenshot 2024-05-21 070936](https://github.com/sharpleynate/azure-soc-honeynet/assets/114451775/a4ce7bd3-e1e5-4f59-b9eb-aa9c4504cb82)

## Step 5: Disabling Windows Firewall via Advanced Settings
I proceed to access the Advanced Windows Defender Firewall settings on the Windows VM to disable the firewall entirely. By doing so, I intentionally expose the VM to potential threats from the internet, removing any protective barriers that the firewall previously provided. This action is taken for specific testing or troubleshooting purposes, acknowledging the heightened vulnerability of the system to external risks.

![Screenshot 2024-05-21 071441](https://github.com/sharpleynate/azure-soc-honeynet/assets/114451775/83390ca4-6183-45db-a4e0-6cca8c103e9d)

## Step 6: Setting up SQL Database
After setting up the SQL database, configuring default settings and permissions, and assigning the current profile, I proceed with the installation process. Next, I download SQL Server Management Studio (SSMS) and configure it accordingly, as outlined in the provided Microsoft Learn documentation. Additionally, I navigate to the registry editor and make the necessary adjustments in the specified registry location to enable the desired functionality.

![Screenshot 2024-05-21 191159](https://github.com/sharpleynate/azure-soc-honeynet/assets/114451775/3ef47491-c57d-40fd-ab0a-e67a7e26bacc)

## Step 7: Enabling SQL Edit Functionality
To enable the edit function of SQL, I execute the command in the command prompt:

auditpol /set /subcategory:"application generated" /success:enable /failure:enable

Following this, I launch SQL Server Management Studio and log in using the sa (System Administrator) or admin account. Within SSMS, I access the properties of the Windows VM and configure security options. Specifically, I enable the feature to log both failed and successful logins for enhanced monitoring and auditing purposes.

![Screenshot 2024-05-21 191159](https://github.com/sharpleynate/azure-soc-honeynet/assets/114451775/69cb447f-d5ce-4913-98ae-9f7d1af1eb07)

## Step 8: Simulating Unauthorized Access
With deliberate intent, I enter incorrect credentials, both username and password, when attempting to log in to the SQL Server. This action is performed to simulate a failed login attempt, allowing for testing of the system's response to unauthorized access and validating the effectiveness of the configured security measures, such as auditing and logging of login attempts.

![Screenshot 2024-05-21 191249](https://github.com/sharpleynate/azure-soc-honeynet/assets/114451775/323d1f65-29e4-4f51-a58d-e681e1fee502)

## Step 9: Monitoring Failed Login Attempts
Upon entering the incorrect credentials for SQL Server, Event Viewer promptly notifies me of the failed login attempt. This notification serves as an essential alert, indicating that the security measures configured within the system are functioning as intended, effectively capturing and recording unauthorized access attempts for further analysis and mitigation.

![Screenshot 2024-05-21 191445](https://github.com/sharpleynate/azure-soc-honeynet/assets/114451775/62278f4d-deaa-41f7-bdc9-eea112a44de0)

## Step 10: Security Testing on Linux VM
With everything configured correctly on the Windows side, I shift my focus to the Linux VM. First, I conduct a ping test to verify connectivity, which yields a successful result. With confirmation of network connectivity, I proceed to establish an SSH (Secure Shell) connection to the Linux VM from my Windows VM. This allows me to securely access the command-line interface of the Linux VM, enabling further configuration and management tasks as needed.

![Screenshot 2024-05-21 191803](https://github.com/sharpleynate/azure-soc-honeynet/assets/114451775/8924e44f-63f1-44f1-b028-3938d60bc977)

## Step 11: Setting up Attack VM
Having established our SQL database, along with the virtual machines (Linux and Windows) and intentionally weakened the Network Security Groups (NSGs), we move on to the next phase by setting up an attack VM. This specialized virtual machine is specifically designed and configured to simulate various cyber attacks, providing a controlled environment for testing the effectiveness of our security measures and identifying potential vulnerabilities within our system.

![Screenshot 2024-05-21 192958](https://github.com/sharpleynate/azure-soc-honeynet/assets/114451775/f46f8e88-1b49-417e-9be2-f858d2e1ff6a)

## Step 12: Testing Unauthorized Access from Attack VM
From my attack VM, I initiate a Remote Desktop Protocol (RDP) session to my Windows VM. In this session, I deliberately input fake login credentials to simulate an unauthorized access attempt. This action allows me to monitor the logs generated from the interaction between my attacker VM and Windows VM, providing valuable insights for later analysis.

Subsequently, I download SQL Server Management Studio (SSMS) on my attack VM and attempt to sign in to the Windows VM using incorrect credentials. This intentional misuse of credentials further simulates a potential security breach, enabling me to assess how effectively the system detects and responds to such unauthorized login attempts originating from the attacker VM.

![Screenshot 2024-05-22 030007](https://github.com/sharpleynate/azure-soc-honeynet/assets/114451775/f07342b7-a588-442c-8b0d-560332a42f75)

## Step 13: Testing Unauthorized Access on Linux VM
Continuing with the testing, I establish an SSH connection from my attacker VM to my Linux VM using fake credentials. This action replicates a scenario where an unauthorized user attempts to gain access to the Linux system using invalid login information. By doing so, I can analyze the system logs to observe how the Linux VM handles and logs such unauthorized access attempts, further strengthening our understanding of the system's security posture and potential vulnerabilities.

![Screenshot 2024-05-22 030348](https://github.com/sharpleynate/azure-soc-honeynet/assets/114451775/5da57673-b54b-433c-9988-d1e933321d82)

## Step 14: Analyzing Logs and Incidents
Returning to my Windows VM, I initiate another Remote Desktop session to conduct further investigation. Within the Windows Event Viewer, specifically in the application and security tabs, I analyze the logs to identify and review the attempted logons that were triggered during the simulated attacks from the attacker VM. By examining these logs, I can gain valuable insights into the nature of the attempted intrusions, their origin, and any potential security implications for the system. This analysis aids in understanding the effectiveness of the implemented security measures and informs any necessary adjustments or enhancements to bolster the system's defenses against future attacks.

![Screenshot 2024-05-22 031554](https://github.com/sharpleynate/azure-soc-honeynet/assets/114451775/439db97f-e680-4bc5-bdfa-6fd2aca0f97c)

## Step 15: Analyzing Linux Authentication Logs
Switching from the VMs to my main desktop, I utilize the terminal to SSH into my Linux VM for further analysis. Navigating to the appropriate directory with the command cd /var/log, I access the logs where authentication-related information is stored.

To specifically focus on password-related logs, I execute the command cat auth.log | grep password. This command filters the contents of the authentication log (auth.log) to display only entries containing the keyword "password", allowing me to pinpoint and scrutinize relevant log entries related to authentication attempts on the Linux VM. This meticulous examination provides valuable insights into any unauthorized access attempts and aids in assessing the effectiveness of the security measures implemented on the Linux system.

![Screenshot 2024-05-22 031954](https://github.com/sharpleynate/azure-soc-honeynet/assets/114451775/9a0bf533-cda8-4a8c-a0f4-63194139fa5a)

## Step 16: Enhancing Monitoring Capabilities
Observing numerous attempted logon attempts from various sources, I recognize the importance of robust log management and analysis. To enhance our monitoring capabilities and gain deeper insights into system activities, I proceed to create a Log Analytics workspace.

This workspace will serve as a centralized hub for collecting, analyzing, and visualizing log data from multiple sources, including our virtual machines. By consolidating logs in a single location and leveraging advanced analytics tools, we can effectively detect anomalies, identify security threats, and generate actionable insights to strengthen our overall cybersecurity posture.

![Screenshot 2024-05-22 034934](https://github.com/sharpleynate/azure-soc-honeynet/assets/114451775/64120274-5345-4754-8892-a485333e28c9)

## Step 17: Setting up Microsoft Sentinel
After setting up the Log Analytics workspace, I proceed to create a Microsoft Sentinel instance within the RG-lab resource group. Within Sentinel, I create a new watchlist named "geoip." This watchlist is designed to store geographical IP information for analysis and correlation with incoming log data.

To populate the "geoip" watchlist, I upload a pre-configured GeoIP CSV file containing relevant geographical data associated with IP addresses. This data will enable Sentinel to enrich log entries with geographic information, facilitating enhanced threat detection and response capabilities by correlating IP addresses with their corresponding geographical locations.

![Screenshot 2024-05-22 041449](https://github.com/sharpleynate/azure-soc-honeynet/assets/114451775/21771994-2a12-4623-83cc-eb2539701625)

## Step 18: Configuring Microsoft Defender for Cloud
Continuing with the setup, I proceed to configure Microsoft Defender for Cloud. Within Defender for Cloud, I enable protection for servers and SQL Servers across our virtual machines. In the data collection tab, I ensure that all relevant events are enabled to provide comprehensive visibility into system activities.

Additionally, I configure SQL Server designation within the Defender plan to specifically tailor the protection measures for our SQL databases. To ensure continuous monitoring and analysis of security events, I enable continuous export, allowing for the seamless transfer of security data to external monitoring and analysis tools for further investigation and response.

![Screenshot 2024-05-22 050223](https://github.com/sharpleynate/azure-soc-honeynet/assets/114451775/c12dd7e8-3817-4626-9c61-2342a411f097)

## Step 19: Configuring Data Collection Rulesets
To facilitate comprehensive logging and monitoring, I create a storage account within the RG-Lab resource group. In this storage account, I configure flow logs to capture network traffic data from both the Windows and Linux VMs.

Next, I successfully configure data collection rulesets to retrieve logs from both Windows and Linux environments. Within the data source settings, I add new rulesets specifically tailored for Windows event logs and Linux syslogs. These rulesets define the parameters for collecting and forwarding log data from the respective operating systems to the storage account for centralized storage and analysis.

![Screenshot 2024-05-22 050701](https://github.com/sharpleynate/azure-soc-honeynet/assets/114451775/3d70141b-090f-423c-94e1-84870070c21e)


## Step 20: Customizing Workbooks
I delete existing default workbooks to replace with customized ones focused on:

**Windows Security Events**
![Screenshot 2024-05-22 081712](https://github.com/sharpleynate/azure-soc-honeynet/assets/114451775/a5651711-893f-4035-9495-48978509bc88)

**Malicious Network Flows**
![Screenshot 2024-05-22 081355](https://github.com/sharpleynate/azure-soc-honeynet/assets/114451775/5fbe984b-26e7-4141-aabe-13e997ed66ed)

**SQL Server Authentication Attempts**
![Screenshot 2024-05-22 081630](https://github.com/sharpleynate/azure-soc-honeynet/assets/114451775/5a54f1f3-0113-426f-9bd1-9bd73623ff23)

**Linux SSH Authentication Failures**
![Screenshot 2024-05-22 082010](https://github.com/sharpleynate/azure-soc-honeynet/assets/114451775/8f9841c8-c290-481f-9f5a-2e55f44bfbb8)

These workbooks visualize relevant security events, enriched with geographic information, to aid in threat detection and response.

## Step 21: Importing Sentinel Analytics Rules
Continuing by importing the Sentinel-Analytics-Rules(KQL Alert Queries).json file into the analytics section for further analysis and enhancement of our detection capabilities.

![Screenshot 2024-05-22 082909](https://github.com/sharpleynate/azure-soc-honeynet/assets/114451775/a1910d40-516d-4107-817c-2c6d66f1e641)

## Step 22: Testing Security Measures
I conduct a test simulation for Failed logon attempts, revealing an average of 24 alerts per day. Additionally, I initiate an investigation within the Incidents tab to delve deeper into the detected security incidents.

![Screenshot 2024-05-22 083126](https://github.com/sharpleynate/azure-soc-honeynet/assets/114451775/a82fa73b-ea22-4c52-af8c-eb34991d75ed)

## Step 23: Incident Response and Hardening
Entering the Analytics responses section, I engage in incident response activities, prioritizing patching to address vulnerabilities identified during the investigation. Noticing vulnerabilities in the Linux security groups, I promptly adjust the network settings for both Linux and Windows VMs to limit access to 'My IP address' only. This proactive measure aims to mitigate risks associated with attempted brute-forcing or unauthorized RDP access, bolstering the overall security posture of the environment.

![Screenshot 2024-05-22 083508](https://github.com/sharpleynate/azure-soc-honeynet/assets/114451775/9cbbf8cb-cb70-47d9-9def-21b60580fe14)

## Step 24: Metrics Before and After Hardening
### **Before Hardening**

| Start Time: 2024-05-21

| Metric | Count |
| --- | --- |
| SecurityEvent | 7833 |
| Syslog | 725 |
| SecurityAlert | 3 |
| SecurityIncident | 23 |
| AzureNetworkAnalytics_CL | 273 |

### **After Hardening**

| Stop Time: 2024-05-22

| Metric | Count |
| --- | --- |
| SecurityEvent | 4523 |
| Syslog | 3 |
| SecurityAlert | 0 |
| SecurityIncident | 0 |
| AzureNetworkAnalytics_CL | 0 |

### **Percentage Change in Metrics**

| Metric | Before Hardening | After Hardening | Percentage Change (%) |
| --- | --- | --- | --- |
| SecurityEvent | 7394 | 4523 | -38.83% |
| Syslog | 725 | 3 | -99.59% |
| SecurityAlert | 4 | 0 | -100% |
| SecurityIncident | 8 | 0 | -100% |
| AzureNetworkAnalytics_CL | 249 | 0 | -100% |

## Step 25: Conclusion 
This project demonstrates the setup of a live SOC and honeynet in Azure, involving virtual machine deployment, security configuration, and incident response integration. Through deliberate security testing and monitoring, we showcased the effectiveness of implemented measures, emphasizing the importance of proactive security practices in cloud environments.
