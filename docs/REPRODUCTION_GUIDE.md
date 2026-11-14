# Reproduction guide (own isolated lab only)

## Environment

- VMware Workstation; Ubuntu Server 24.04.5 LTS Wazuh VM
- Wazuh all-in-one Manager, Indexer and Dashboard (tested with Wazuh 4.14.10)
- Recommended Wazuh VM: **4 vCPUs, 8 GB RAM, at least 50 GB usable disk space**
- Windows 11 endpoint with Wazuh agent and Microsoft Sysmon
- Reachable private networking between Windows and the Ubuntu Wazuh server

Official resources: [Wazuh documentation](https://documentation.wazuh.com/current/) · [Microsoft Sysmon](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon)

## Overview

1. Install Ubuntu Server as a VMware VM, update packages, and confirm disk capacity (`df -h /`).
2. Use the **current official Wazuh all-in-one installation instructions** for the chosen supported version. Complete the indexer, server and dashboard setup.
3. Enroll your **own** Windows endpoint through Wazuh Dashboard → Agent Management → Deploy new agent; confirm `Active`.
4. Install Sysmon on Windows. Add the Sysmon `eventchannel` `<localfile>` snippet from `Configurations/windows_agent_config_snippet.xml` inside the **existing** Wazuh agent `<ossec_config>`.
5. Restart the Windows Wazuh agent service and verify Sysmon Event ID 1 in Event Viewer and corresponding Wazuh alerts.
6. Create the dedicated monitored folder and add the realtime FIM `<directories>` line to the existing `<syscheck>` block; restart the agent.
7. Use the controlled tests below. Examine the Wazuh alerts and compare them to source Windows events.
8. Copy the local Wazuh rule **group** from [`local_rules.xml`](../Configurations/local_rules.xml) into the server's `/var/ossec/etc/rules/local_rules.xml`, making sure groups are not nested. Test rule syntax and restart manager.

### Basic verification commands

**Ubuntu Wazuh VM:**

```bash
sudo systemctl is-active wazuh-manager
sudo systemctl is-active wazuh-indexer
sudo systemctl is-active wazuh-dashboard
sudo /var/ossec/bin/wazuh-analysisd -t
```

**Windows PowerShell (Administrator):**

```powershell
Get-Service WazuhSvc
Get-Service Sysmon64
```

## Safe validation scenarios

### A. Failed logon, localhost only

Use a nonexistent lab test account and a dummy password, not a real account. In **Command Prompt** on the owner-controlled Windows device:

```cmd
net use \\127.0.0.1\IPC$ /user:%COMPUTERNAME%\SOC-Lab-Test "DUMMY_TEST_PASSWORD"
```

An authentication failure can produce Windows Security Event ID 4625. Verify in Event Viewer, then in Wazuh (e.g. query `data.win.system.eventID: "4625"`). The test in this portfolio produced Wazuh Rule 60122 (level 5).

### B. File creation + modification

On Windows PowerShell:

```powershell
New-Item -ItemType Directory -Force -Path 'C:\SOC-Lab\Monitored'
Set-Content -Path 'C:\SOC-Lab\Monitored\test.txt' -Value 'Initial SOC security monitoring test'
Add-Content -Path 'C:\SOC-Lab\Monitored\test.txt' -Value 'Modified file for SOC integrity monitoring test'
```

Check Wazuh File Integrity Monitoring Events for `added` and `modified`. In this lab they produced Rules 554 and 550 respectively. File hashes change after modification.

### C. Benign custom process detection

Copy the `soc_lab` group into Wazuh Manager's `local_rules.xml`, verify rule syntax:

```bash
sudo /var/ossec/bin/wazuh-analysisd -t
sudo systemctl restart wazuh-manager
```

On Windows, launch `notepad.exe`, then query Wazuh Threat Hunting: `rule.id: 100101`.

### D. Alert investigation

Review Wazuh Rule 92066 (if observed in your environment), correlate process GUID with Sysmon Event ID 1, inspect process image, command line, parent executable and user context. **Do not assume** every environment will generate the same benign alert.

## Troubleshooting learned during build

- A VMware disk can be large while the mounted Ubuntu root filesystem is small due to LVM allocation. Check `lsblk` and `df -h /` before installation.
- Partial installations can leave packages or running services; check manager/indexer/dashboard status and package logs before retrying.
- Wazuh custom `<group>` elements belong at the top level in `local_rules.xml`, not nested inside another `<group>`.
- `runas` may fail before producing an authentication event. Confirm Event ID 4625 in Windows logs rather than assuming the command caused one.
- Detection dashboards surface **alerts**, which may not include every raw Sysmon event.

## Ethical boundary

Use only your own computer or an explicitly authorized test VM. Do not run authentication tests against any external address or production system.
