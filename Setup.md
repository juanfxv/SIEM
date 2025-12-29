# Wazuh SIEM Deployment Guide

This guide details the steps taken to deploy a Wazuh SIEM environment for host-based monitoring.

## Prerequisites
* **Hypervisor:** VMware Workstation.
* **Manager OS:** Ubuntu Server 24.04 LTS.
* **Agent OS:** Windows 11 (Host Machine).
* **Network:** Bridged Adapter configuration.

## Phase 1: Wazuh Manager Installation (Ubuntu)
1. **System Preparation:** Update the Ubuntu environment and install necessary dependencies like `curl` and `gpg`.
2. **Add Wazuh GPG Key:**
   ```bash
   curl -s [https://packages.wazuh.com/key/GPG-KEY-WAZUH](https://packages.wazuh.com/key/GPG-KEY-WAZUH) | sudo gpg --dearmor -o /usr/share/keyrings/wazuh-archive-keyring.gpg

## Phase 2: Wazuh Agent Registration (Windows)
Installation: Download and install the Wazuh Agent MSI package.

Key Generation: On the Ubuntu Manager, run the management utility to generate a unique key for the Windows host:


sudo /var/ossec/bin/manage_agents
Activation: Input the Manager IP and the generated Authentication Key into the Wazuh Agent Manager GUI on the Windows host.

Service Restart: Restart the Wazuh service to finalize the connection.

## Phase 3: Configuring File Integrity Monitoring (FIM)
Edit Configuration: Open C:\Program Files (x86)\ossec-agent\ossec.conf with Administrative privileges.

Define Monitored Directory: Add the following block to the <syscheck> section to monitor a specific test folder in real-time:


<directories realtime="yes">C:\Users\YourName\TestFolder</directories>
Verify Alerts: Create or modify files in the test directory and monitor the "Integrity Monitoring" tab in the Wazuh Dashboard for real-time alerts.
