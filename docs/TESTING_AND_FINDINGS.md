# Testing, validation and investigation findings

## 1. SecEdit.exe / PowerShell alert triage

- **Observed:** 8 Wazuh Rule 92066 alerts involving `SecEdit.exe` launched from PowerShell.
- **Activity:** exported Windows security policy using `secedit /export /cfg ...`, inspected `LockoutBadCount`, removed the temporary file.
- **Correlation:** a Sysmon process GUID search identified `wazuh-agent.exe` as PowerShell's parent.
- **Analyst assessment:** **likely legitimate automated security configuration assessment**, not evidence of an intrusion. This assessment is limited to the reviewed process chain.
- **Evidence:** Figures 5 and 6.

## 2. Failed network login detection

- **Test:** attempted SMB/IPC$ authentication against the owner's localhost using a deliberately nonexistent account `SOC-Lab-Test` and dummy password.
- **Windows evidence:** Security Event ID **4625**, logon type **3** (network); `0xC000006D` overall failure, `0xC0000064` unknown username.
- **SIEM detection:** Wazuh Rule **60122**, level **5**, `Logon Failure - Unknown user or bad password`.
- **Disposition:** **controlled simulation; detection successful**, not a real-world attack.
- **Evidence:** Figures 7, 8, 9A, 9B.

## 3. Realtime File Integrity Monitoring (FIM)

- **Monitored path:** `C:\SOC-Lab\Monitored\test.txt`.
- **Create:** Wazuh Rule **554**, level **5**, event `added`.
- **Modify:** Wazuh Rule **550**, level **7**, event `modified` / `Integrity checksum changed`.
- **Size:** 38 bytes before, 87 bytes after.
- **MD5:** `2904700621599e43901b984154aca3ca` → `74b8e087cf45ec71c4feb713d90d1fb5`.
- **SHA-256:** `6224f453758537ad5b43b50c3458e9e2364bd6a1225b72b8dfa197d8bf60b383` → `6863be9f8b28ab96d31bf6668f05d87f99fb4657ac0ab23765ac3ca06b884c30`.
- **Disposition:** **controlled file change; detection successful**.
- **Evidence:** Figures 10, 11, 12.

## 4. Custom detection engineering

- **Source:** Microsoft Sysmon Process Create, Event ID **1**.
- **Rule:** **100101** / level **5** / group `soc_lab,sysmon`.
- **Condition:** child of Wazuh Sysmon parent rule `61603`, executable image ending in `notepad.exe`.
- **Validation:** Wazuh rule syntax validated with `wazuh-analysisd -t`; manager restarted; opening Notepad produced a matching alert.
- **Process details:** Microsoft Windows Notepad package installed under `WindowsApps`; parent process `explorer.exe` in the recorded event.
- **Disposition:** benign validation; the alert is **not malicious by itself**.
- **Evidence:** Figures 13, 14A–14C.

## Scope and limitations

This was a single Windows endpoint with a private Wazuh instance. The tests demonstrate collection, validation and triage skills, not sustained uptime, enterprise-scale coverage, confirmed malware detection, production incident response or professional employment experience.
