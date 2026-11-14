# Evidence index — 17 supplied screenshots

These are **screenshots from the actual personal lab**. They are retained with the user's original figure numbers, with one double `.png` extension corrected. A few historic screenshot filenames do not accurately describe the visible fields; the descriptions below are based on the image contents and are consistent with the completed technical report.

| Figure/file | What the image actually demonstrates |
|---|---|
| [Figure_01_Wazuh_Dashboard.png](../Screenshots/Figure_01_Wazuh_Dashboard.png) | Wazuh main dashboard and SOC monitoring overview. |
| [Figure_02_Active_Windows_Agent.png](../Screenshots/Figure_02_Active_Windows_Agent.png) | Windows-SOC-Agent, ID 001, Active in Wazuh. |
| [Figure_03_Sysmon_Process_Creation.png](../Screenshots/Figure_03_Sysmon_Process_Creation.png) | Windows Event Viewer showing Sysmon process activity; Event ID 1. |
| [Figure_04_Wazuh_Sysmon_Alerts.png](../Screenshots/Figure_04_Wazuh_Sysmon_Alerts.png) | Sysmon-related Wazuh Threat Hunting alerts. |
| [Figure_05_Security_Alert_Investigation.png](../Screenshots/Figure_05_Security_Alert_Investigation.png) | SecEdit.exe process execution, PowerShell parent command and hash evidence (Rule 92066). |
| [Figure_06_Alert_Root_Cause_Analysis.png](../Screenshots/Figure_06_Alert_Root_Cause_Analysis.png) | Correlated PowerShell event with wazuh-agent.exe as parent. |
| [Figure_07_Failed_Login_Event_4625.png](../Screenshots/Figure_07_Failed_Login_Event_4625.png) | Windows Event Viewer Event ID 4625 for controlled failed logon. |
| [Figure_08_Wazuh_Failed_Login_Detection.png](../Screenshots/Figure_08_Wazuh_Failed_Login_Detection.png) | Wazuh Rule 60122, level 5, identifying failed authentication. |
| [Figure_09A_Failed_Login_Event_Details.png](../Screenshots/Figure_09A_Failed_Login_Event_Details.png) | Wazuh rule classification fields (Rule 60122, level 5) and failed-logon description. |
| [Figure_09B_Wazuh_Authentication_Alert.png](../Screenshots/Figure_09B_Wazuh_Authentication_Alert.png) | Wazuh Event ID 4625 fields and SOC-Lab-Test target username. |
| [Figure_10_Wazuh_File_Creation_Detection.png](../Screenshots/Figure_10_Wazuh_File_Creation_Detection.png) | Wazuh FIM Rule 554 for test.txt creation. |
| [Figure_11_Wazuh_File_Modification_Detection.png](../Screenshots/Figure_11_Wazuh_File_Modification_Detection.png) | Wazuh FIM Rule 550 for test.txt modification, alongside creation event. |
| [Figure_12_File_Integrity_Hash_Comparison.png](../Screenshots/Figure_12_File_Integrity_Hash_Comparison.png) | Realtime FIM event showing changed MD5, SHA-1, SHA-256 and file size. |
| [Figure_13_Custom_Wazuh_Detection_Rule.png](../Screenshots/Figure_13_Custom_Wazuh_Detection_Rule.png) | Rule 100101 firing after Notepad execution. |
| [Figure_14A_Custom_Rule_Alert.png](../Screenshots/Figure_14A_Custom_Rule_Alert.png) | Notepad process path, command line, executable hash and parent process (despite the filename). |
| [Figure_14B_Notepad_Process_Details.png](../Screenshots/Figure_14B_Notepad_Process_Details.png) | Sysmon process metadata confirming Event ID 1 (despite the filename). |
| [Figure_14C_Sysmon_Process_Creation.png](../Screenshots/Figure_14C_Sysmon_Process_Creation.png) | Custom Rule 100101 description, level, group and timestamp (despite the filename). |

## Important filename notes

- `Figure_09A` mainly shows **Wazuh rule classification**; `Figure_09B` shows **Event 4625 and the username**. Their legacy filenames can imply the reverse.
- `Figure_14A` shows **Notepad executable/process details**, `Figure_14B` shows **Sysmon event metadata**, and `Figure_14C` shows **custom rule metadata**. The descriptions above reflect actual contents.
- Figure 11 originally had the accidental filename extension `.png.png`; it is included as `.png`.

The full report references the same figure numbers and provides more detailed captions.
