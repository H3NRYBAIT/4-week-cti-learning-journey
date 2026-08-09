# MITRE ATT&CK Mapping — Week 2 Lumma Stealer Investigation

| Technique ID | Name | Evidence |
|---|---|---|
| T1204.002 | Malicious File Execution | SETUP.zip delivery, user executes trojanized installer |
| T1027.002 | Software Packing | overlay tag — encrypted payload after PE structure |
| T1497.001 | Virtualization/Sandbox Evasion | detect-debug-environment, checks-bios, long-sleeps |
| T1082 | System Information Discovery | calls-wmi, /api/set_agent fingerprinting in Any.run |
| T1553.002 | Code Signing | Fake cert from vewadis.on — untrusted root |
| T1583.001 | Acquire Infrastructure: Domains | 73 .cyou domains registered via Dynadot in batches |
| T1071.001 | Application Layer Protocol: Web | HTTPS C2 to .cyou domains, ET MALWARE Lumma rule |
| T1555.003 | Credentials from Web Browsers | Chrome and Edge data harvested in Any.run sandbox |
| T1539 | Steal Web Session Cookie | Cookie harvesting documented in Lumma public reports |
| T1041 | Exfiltration over C2 Channel | Data sent via HTTPS POST to C2 domains |
