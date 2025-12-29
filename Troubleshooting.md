# Troubleshooting Log: Wazuh Agent Connectivity Issues

This document outlines the technical challenges encountered during the SIEM deployment and the steps taken to resolve them.

## Issue: Agent Connection Failure (Error 4101)
**Symptom:** After applying the authentication key and Manager IP, the Windows Agent failed to appear as "Active" in the Wazuh Dashboard.

### 1. Log Analysis
Examination of the agent logs at `C:\Program Files (x86)\ossec-agent\ossec.log` revealed the following critical errors:
* `ERROR: Agent version must be lower or equal to manager version (from manager)`
* `WARNING: (4101): Waiting for server reply (not started). Ensure that the manager version is 'v4.14.1' or higher.`

### 2. Root Cause Identification
[cite_start]The Wazuh Manager was deployed using version **4.12**, while the Windows Agent was manually downloaded as the latest stable version (**4.14**)[cite: 1, 3]. Wazuh architecture requires the Manager version to be greater than or equal to the Agent version for successful telemetry synchronization.

### 3. Resolution
1. **Agent Removal:** Performed a full uninstall of the v4.14 Wazuh Agent from the Windows host.
2. [cite_start]**Version Matching:** Downloaded and installed the specific **v4.12.0** MSI package to align with the Manager's deployment[cite: 1].
3. **Re-registration:** Re-applied the authentication key and restarted the service.
4. **Verification:** Confirmed the agent status shifted to **Active** in the dashboard within 60 seconds of the restart.

## Key Takeaway
Always verify version compatibility across the SIEM stack before deployment, particularly when using automated installation scripts for the Manager that may point to specific legacy or stable branches.
