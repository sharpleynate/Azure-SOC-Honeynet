Building a Live SOC + Honeynet in Azure
This project demonstrates the creation of a Live Security Operations Center (SOC) and Honeynet in Azure. It involves setting up Windows and Linux virtual machines, configuring them to be vulnerable, and then hardening the environment to improve security. The steps include deploying virtual machines, setting up a SQL database, configuring network security, and monitoring security events using Microsoft Sentinel.

Video Guide
Watch the tutorial on YouTube

Steps
1. Create Virtual Machines
Create two virtual machines (Windows and Linux) in the same resource group.
Creating VMs

2. Configure Network Security Groups (NSGs)
Delete the RDP port inbound rule and allow all inbound traffic to make both machines vulnerable.
NSG Configuration

3. Disable Firewall
Ping the Windows VM public IP to check the firewall status and then disable it via Remote Desktop.
Disabling Firewall

4. Set Up SQL Database
Create and configure a SQL database, then download and set up SQL Server Management Studio (SSMS).
5. Enable SQL Server Auditing
Configure SQL Server to write audit events to the security log and enable auditing using auditpol.
shell
Copy code
auditpol /set /subcategory:"application generated" /success:enable /failure:enable
6. Simulate Attacks
Perform logon attempts with incorrect credentials to generate logs.
Failed Logon

7. SSH into Linux VM
Test connectivity and SSH into the Linux VM from the Windows VM.
8. Set Up Attack VM
Use an attack VM to simulate attacks on the Windows and Linux VMs, tracking the logs from these attacks.
9. Monitor Logs
Use Event Viewer on Windows and SSH on Linux to monitor attempted logons and other activities.
shell
Copy code
cd /var/logs
cat auth.log | grep password
Monitoring Logs

10. Create Log Analytics Workspace and Sentinel
Set up a Log Analytics workspace and Microsoft Sentinel, upload GeoIP data, and enable various security features.
Log Analytics

11. Configure Workbooks and Alerts
Create workbooks and configure alerts for different types of logs (NSG, SQL, SSH).
12. Harden Security
Restrict access to the VMs to only your IP address, enable firewalls, and monitor the environment for suspicious activity.
Harden Security

Metrics Before and After Hardening
Before Hardening
| Start Time: 2024-04-13 13:53:48 | Stop Time: 2024-04-14 13:53:48 |

Metric	Count
SecurityEvent	7394
Syslog	725
SecurityAlert	4
SecurityIncident	8
AzureNetworkAnalytics_CL	249
After Hardening
| Start Time: 2024-05-21 04:20:02 | Stop Time: 2024-05-22 09:12:45 |

Metric	Count
SecurityEvent	4523
Syslog	3
SecurityAlert	0
SecurityIncident	0
AzureNetworkAnalytics_CL	0
Percentage Change in Metrics
Metric	Before Hardening	After Hardening	Percentage Change (%)
SecurityEvent	7394	4523	-38.83%
Syslog	725	3	-99.59%
SecurityAlert	4	0	-100%
SecurityIncident	8	0	-100%
AzureNetworkAnalytics_CL	249	0	-100%
Graph: Percentage Change in Metrics
plaintext
Copy code
Before Hardening (Blue) | After Hardening (Green)
plaintext
Copy code
100% ────────────────────────────────────────────────────────────────────────
 80% ────────────────────────────────────────────────────────────────────────
 60% ────────────────────────────────────────────────────────────
 40% ────────────────────────────────────────────────────────────
 20% ────────────────────────────────────────────────────────────
  0% ────────────────────────────────────────────────────────────
-20% ────────────────────────────────────────────────────────────
-40% ──────────────────────────────────────────
-60% ──────────────────────────────────────────
-80% ──────────────────────────────────────────
-100% ─────────────────────────────────────────
     SecurityEvent      Syslog      SecurityAlert   SecurityIncident  AzureNetworkAnalytics_CL
Conclusion
This project highlights the process of setting up a honeynet in Azure and the importance of hardening your environment to reduce security risks. By simulating attacks and monitoring logs, you can identify vulnerabilities and take corrective actions to enhance security.
