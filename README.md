# Project Title

## Overview
This project demonstrates setting up and configuring a mini honeynet in Microsoft Azure. It includes creating virtual machines, configuring security settings, deploying a SQL database, and integrating Microsoft Sentinel for security monitoring and incident response.

## Setup Instructions

### Step 1: Create Virtual Machines
1. Create two virtual machines (one Windows, one Linux) in the same resource group.
2. Configure inbound security rules to allow all traffic, making them intentionally vulnerable.

### Step 2: Disable Firewall on Windows VM
1. RDP into the Windows VM.
2. Disable the Windows Defender firewall to expose the machine to the internet.

### Step 3: Set Up SQL Database
1. Create and configure a SQL database.
2. Download and configure SQL Server Management Studio (SSMS).
3. Enable SQL Server auditing.

### Step 4: Simulate Attacks
1. Use incorrect credentials to attempt logins on both VMs.
2. Check event logs for failed login attempts.

### Step 5: Integrate with Microsoft Sentinel
1. Create a Log Analytics workspace and integrate Microsoft Sentinel.
2. Create watchlists and configure data collection rules.
3. Set up workbooks to visualize and monitor logs and alerts.

## Usage
1. Monitor logs and alerts in Microsoft Sentinel.
2. Perform incident response based on alerts and logs.
3. Harden the environment by applying security controls and monitoring their effectiveness.

## Configuration Details
- **Virtual Machines**: Windows and Linux VMs configured in Azure.
- **SQL Database**: SQL Server configured with auditing enabled.
- **Microsoft Sentinel**: Configured to monitor security events and incidents.

## Visuals
![Screenshot of Virtual Machines](link-to-your-screenshot)
![Screenshot of Sentinel Dashboard](link-to-your-screenshot)

## Conclusion
This project demonstrates the setup and configuration of a mini honeynet in Azure, showcasing how to monitor and respond to security incidents using Microsoft Sentinel.

