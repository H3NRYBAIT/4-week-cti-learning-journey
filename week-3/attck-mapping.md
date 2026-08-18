# MITRE ATT&CK Mapping — Week 3 SideWinder APT Investigation

**Actor:** SideWinder APT (G0121)
**Techniques Documented:** 22

---

| Technique ID | Name | Evidence |
|---|---|---|
| T1566.001 | Spearphishing Attachment | DOCX lure files delivered via email to Pakistani government employees |
| T1566.002 | Spearphishing Link | Links to attacker-controlled servers for template injection |
| T1221 | Template Injection | DOCX called out to remote server for RTF file on open |
| T1203 | Exploitation for Client Execution | CVE-2017-11882 — Microsoft Office memory corruption — still exploited in 2024 |
| T1218.005 | System Binary Proxy Execution: Mshta | mshta.exe used to download and execute malicious HTA file |
| T1574.001 | DLL Side-Loading | Backdoor Loader installed via legitimate signed Windows applications |
| T1574.013 | KernelCallbackTable Injection | Cobalt Strike injected into notepad.exe via KernelCallbackTable |
| T1027 | Obfuscated Files or Information | Heavily obfuscated JavaScript loader with substitution algorithm |
| T1480 | Execution Guardrails | Pakistan Standard Time check — terminated outside UTC+5 |
| T1547.001 | Boot or Logon Autostart Execution | Persistence established via registry run keys |
| T1059.001 | PowerShell | Used in loader stages |
| T1059.005 | Visual Basic | VBA macros in lure documents |
| T1059.007 | JavaScript | Two-stage obfuscated JavaScript loader |
| T1041 | Exfiltration Over C2 Channel | StealerBot exfiltrated credentials and files via C2 |
| T1083 | File and Directory Discovery | File Manager InfoExfil module — recursive drive enumeration |
| T1057 | Process Discovery | Downloader Module checked 137 security product process names |
| T1518.001 | Security Software Discovery | WMI queries identified installed security products |
| T1082 | System Information Discovery | /api/set_agent system fingerprinting — hardware, OS, environment |
| T1033 | System Owner/User Discovery | Victim profiling before payload deployment |
| T1036.005 | Masquerading: Match Legitimate Resource Name | DLL names changed constantly — propsys.dll, winmm.dll, UxTheme.dll |
| T1119 | Automated Collection | StealerBot File Stealer and Screenshot Grabber modules |
| T1020 | Automated Exfiltration | Stolen data automatically sent to C2 |

---

## Victim Filtering Techniques (not in standard ATT&CK)

| Filter | Stage | Purpose |
|---|---|---|
| IP geolocation check | AntiBot Script — phishing page | Block non-Pakistani visitors |
| OS and browser check | AntiBot Script | Block researchers and sandboxes |
| GPU and hardware check | AntiBot Script | Identify virtual environments |
| Screen size check | AntiBot Script | Identify sandbox displays |
| UTC timezone offset | AntiBot Script | Confirm Pakistani timezone |
| RAM threshold < 950MB | JavaScript Loader | Terminate in sandbox environments |
| Pakistan Standard Time UTC+5 | WarHawk Cobalt Strike loader | Hard geographic filter — T1480 |
