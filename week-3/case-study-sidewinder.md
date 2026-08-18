# Case Study: SideWinder APT — Full Threat Actor Profile

**Date:** August 2026
**Author:** Abdullah Hassan
**Actor:** SideWinder APT (G0121)
**Type:** Nation-State APT — Suspected India-nexus
**Target:** Pakistan (primary) · South Asia · Maritime Infrastructure · Nuclear Facilities
**Active Since:** 2012
**Status:** Active as of July 2026

---

## Actor Overview

| Field | Value |
|---|---|
| MITRE ID | G0121 |
| Aliases | Rattlesnake · T-APT-04 · RAZOR TIGER · APT-C-17 · Hardcore Nationalist |
| Suspected Origin | India (medium confidence) |
| Active Since | 2012 |
| Primary Target | Pakistan — government, military, critical infrastructure |
| Secondary Targets | Nepal, Sri Lanka, Afghanistan, Bangladesh, Egypt, UAE, Djibouti |
| Custom Tools | StealerBot · WarHawk · SideWinder.AntiBot.Script |
| Frameworks | Cobalt Strike · Koadic |

---

## Source Reports

- Kaspersky Securelist — March 2025 (maritime and nuclear expansion)
- Kaspersky Securelist — May 2022 (server-based polymorphism)
- Zscaler ThreatLabz — October 2022 (WarHawk backdoor)
- Group-IB Threat Intelligence — February 2023 (phishing infrastructure)
- BlackBerry Research — 2022 (infrastructure mapping)

---

## Victimology

### Primary Targets — Pakistan
- Ministry of Finance
- NADRA — National Database and Registration Authority
- FIA — Federal Investigation Agency
- NEPRA — National Electric Power Regulatory Authority
- Fauji Foundation
- Canteen Stores Department (military)
- Askari Bank (military community bank)
- PTCL — Pakistan Telecommunication Company
- SNGPL — Sui Northern Gas Pipelines
- Pakistan Air Force
- Sindh Police
- NTC — National Telecommunication Corporation
- Pakistan COVID Portal / NCOC

### Expansion Targets — 2024
- Rooppur Nuclear Power Plant — Bangladesh
- Nuclear energy agencies — South Asia
- Port authorities along Red Sea shipping corridor
- Egypt — Suez Canal logistics
- Djibouti — Red Sea port
- Diplomatic missions — Algeria, Saudi Arabia, Uganda, Rwanda, Turkey, Bulgaria

---

## The NEPRA Attack — September 2022

SideWinder APT compromised NEPRA's official website and hosted a malicious ISO file directly on their web server.

- **Lure:** ISO named to match a real Cabinet Division advisory
- **Payload:** WarHawk backdoor
- **Second stage:** Cobalt Strike via KernelCallbackTable injection into notepad.exe
- **Guardrail:** Pakistan Standard Time check (UTC+5) — terminated if timezone did not match
- **Technique:** T1480 Execution Guardrails

---

## Complete Attack Chain

```
Spearphishing Email (DOCX attachment)
  → Remote Template Injection → RTF file download
    → CVE-2017-11882 exploitation (7-year-old exploit, still effective in 2024)
      → mshta.exe (T1218.005) → HTA file download
        → JavaScript Loader Stage 1
            RAM check: terminate if < 950MB (sandbox filter)
          → JavaScript Loader Stage 2
              .NET framework enumeration
              Environment variables set
              Base64-encoded Downloader Module decoded
            → Downloader Module
                WMI queries for 137 security product process names
                Kaspersky detected → alternate execution path
                → Module Installer
                  → Backdoor Loader (DLL sideloading — T1574.001)
                    Legitimate signed app: propsys.dll / vinstrace.dll /
                    JetCfg.dll / policymanager.dll / winmm.dll /
                    xmllite.dll / UxTheme.dll (changed constantly)
                    → StealerBot (loaded into memory — never on disk)
                        Modules available to operator:
                        ├── Live Console (remote command execution)
                        ├── Token Grabber (authentication tokens)
                        ├── Keylogger
                        ├── File Stealer
                        ├── Screenshot Grabber
                        ├── RDP Credential Stealer
                        ├── Credential Phisher
                        └── UAC Bypass
```

---

## WarHawk Modules

| Module | Function |
|---|---|
| Download and Execute | Pull additional payloads from C2 |
| Command Execution | Run system commands from operator |
| File Manager InfoExfil | Recursively enumerate all drives |
| UploadFromC2 | Receive files pushed by operator |

---

## Victim Filtering — Three Layers

**Layer 1 — AntiBot Script (phishing stage)**
Checked: IP geolocation · OS · browser user agent · hardware concurrency · GPU specs · screen size · UTC timezone offset · headless browser detection
If check failed → redirect to legitimate government website

**Layer 2 — RAM Check (JavaScript loader)**
If system RAM < 950MB → terminate
Filters out most sandbox environments

**Layer 3 — Pakistan Standard Time Check (WarHawk Cobalt Strike loader)**
If timezone ≠ UTC+5 → terminate immediately
Only Pakistani systems infected

---

## Infrastructure Analysis

### Hosting Providers (May 2022 — March 2023)
- LeaseWeb → DigitalOcean → Amazon
- Confluence Networks (parallel track)
- HZ Hosting → Hetzner → parked
- Liteserver Holding
- CloudLayer8 → GhostNet → Unified Layers
- Hostinger
- M247
- EDIS GmbH → parked

### Key IPs

**146.190.235.137** — WarHawk C2
- ASN: AS14061 DigitalOcean
- Community score: -56
- Communicating files: ASUS Update Setup (55/70) · RtkNGui.exe (51/70)

**2.56.245.21** — Phishing server
- ASN: AS213250 ITP-Solutions GmbH, Germany
- Current detections: 0/91 (infrastructure rotated — passive DNS is the evidence)
- Passive DNS: 10 fake Pakistani government subdomains Feb–Jul 2022

**3.239.29.103** — Shared C2
- Resolved: fia-gov.org · customs-lk.org · nadra-pk.org · mofa-pk.org · sngpl.org.pk · nationalhelpdesk.pk
- Shared IP confirms same operator ran Pakistan and Sri Lanka campaigns simultaneously

### Domain Naming Convention
- [institution].pakgov.net
- [agency]-gov.org
- [service].govpk-mail.net
- [institution]-pk.org

### FIA-gov.org Infrastructure
- 8 subdomains: ns1 · ns2 · mail · update · ww1 · ww12 · pia (layering PIA lure)
- IP rotation: AWS Aug 2022 → Cloudflare May 2023

### finance.pakgov.net
- 16 sibling domains confirmed on same two IPs
- Migration: 2.56.245.21 (May 2022) → 99.83.154.118 (Jan 2023)
- Detection: 14/91 vendors

---

## Detection Evasion — Key Findings

**Under five hours to replace detected malware**
SideWinder monitored vendor detections in real time. When tools were flagged, modified versions were generated within five hours. Persistence techniques and file paths changed when behavioral detections triggered.

**Server-based polymorphism**
Documented by Kaspersky May 2022. Attribution indicators they had previously relied on disappeared, making the cluster harder to link with confidence.

**Legitimate binary abuse**
DLL sideloading using legitimate signed Windows applications — names changed constantly across campaigns.

**StealerBot never on disk**
Loaded entirely into memory from an encrypted file. Invisible to file-based scanners.

---

## Attribution Assessment

**Confidence:** Medium

**Supporting evidence:**
- Consistent targeting of Pakistan, Nepal, Sri Lanka, Afghanistan — countries where India has documented geopolitical intelligence interests
- Operational patterns consistent with Indian Standard Time in timestamp analysis
- State-level resources: 92+ IPs, hundreds of phishing domains, nine hosting providers, custom modular implant
- Targeting objectives (nuclear facilities, military, foreign ministries) aligned with state intelligence collection

**Complicating factors:**
- Kaspersky stated attribution indicators disappeared in May 2022
- No public government indictment naming individuals
- No HUMINT corroboration in public reporting
- Sophisticated false flag operations technically possible

**Professional statement:** Medium confidence India-nexus state-sponsored threat actor based on geopolitical targeting alignment, operational patterns, and resource indicators. Attribution confidence would increase with HUMINT corroboration or government indictment.

---

## Intelligence Gaps

- Specific Indian government agency directing operations not identified
- Full scope of successful compromises unknown — only attempted attacks documented publicly
- Infrastructure reuse or tooling overlap with SideCopy, Donot Team, Bitter — assessed possible, not confirmed
- Current 2025–2026 active infrastructure not fully mapped in public reporting

---

## Attacker OPSEC Failures

1. **Victim filter became a fingerprint** — Pakistan Standard Time check instantly attributable to Pakistan-targeting actor
2. **Infrastructure reuse exposed full operation** — shared IPs between fia-gov.org and customs-lk.org linked two campaigns in one pivot
3. **Recognizable domain patterns** — [institution].pakgov.net pattern enables crt.sh alerts catching new domains pre-campaign
4. **Parallel campaigns on shared servers** — running multiple country campaigns on same IP gave analysts connection across all of them
5. **Rotation pattern itself became a fingerprint** — changing nine hosting providers in ten months is itself anomalous and identifiable

---

## Attack Flow

```
Spearphishing email to Pakistani government employee
  → Employee opens DOCX (recognizable lure — real institution content)
    → Remote Template Injection → RTF → CVE-2017-11882
      → mshta.exe → HTA → JavaScript loader
        → RAM check · security product check · timezone check
          → Backdoor Loader via DLL sideloading
            → StealerBot in memory
              → Selective module deployment by operator
                → Credentials · files · screenshots exfiltrated
                  → C2 beacon continues until detected or mission complete
```

---

## Featured Medium Article

**SideWinder APT Faked Pakistan's Government Websites for 12 Years and Replaced Detected Malware in Under Five Hours**

🔗 https://medium.com/@H3NRYB41T/sidewinder-apt-faked-pakistans-government-websites-for-12-years-and-replaced-detected-malware-in-ea16137488eb
