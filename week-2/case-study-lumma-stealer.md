# Case Study: 64.89.161.173 — Lumma Stealer C2 Infrastructure Analysis

**Date:** August 8, 2026
**Author:** Abdullah Hassan
**Type:** Malware — Lumma Stealer (MaaS)
**Target:** General public via fake movie torrents, fake software, fake antivirus tools
**Status at discovery:** ACTIVE

---

## The Starting Point

**Primary Sample SHA256:** `e08c0890b11d91b7ee58de25cc190e1fdf760d76b6d0821aa2d1f442b43e719a`

Three malware samples with different filenames and detection profiles all resolved to one C2 IP — 64.89.161.173 — through different .cyou domains, all registered the same day, through the same registrar, on the same ASN.

---

## MalwareBazaar

- **Family:** LummaStealer
- **Detections:** 11 vendors
- **File size:** 4,717,920 bytes
- **First seen:** 2026-08-04 19:38:41 UTC
- **Delivery method:** Web download
- **Tags:** LummaStealer, exe, signed, dropped-by-OffLoader
- **Imphash:** 1aae8bf580c846f39c71c05898e57e88 → 464 samples (254 LummaStealer, 125 SalatStealer, 23 ACRStealer)

---

## VirusTotal — Primary Sample

- **Detection:** 45/70 vendors
- **Threat label:** trojan.lumma/infostealer
- **Family labels:** lumma, infostealer, lummac
- **Compiler:** Go 1.25.4, Architecture 386, OS Windows
- **Fake certificate:** vewadis.on — untrusted root (T1553.002)
- **Filenames:** 15.exe, lwq13.exe, pkdydnzrpd.exe, setup.exe

**Behavioral tags:**
- long-sleeps
- detect-debug-environment
- checks-bios
- overlay
- invalid-signature
- calls-wmi
- spreader

---

## Three Samples — Three C2 Domains — One IP

**Sample 1: eja4yagm.exe**
- Hash: 0336bd5693a24cfe3fdc47424340b373e6ec13b0f36ea1afd4418cafe04fccde
- Detection: 37/61
- C2: http://matchny.cyou/ — 401 Unauthorized

**Sample 2: Setup.exe**
- Hash: 033cfdd3dd7e2bebbc1ed5c838676d024628a92f7dac762eb708ba0c8b7b3e35
- Detection: 14/69
- C2: http://bizsmmit.cyou/ — 401 Unauthorized
- Delivered inside: SETUP.zip (18/67 detections)

**Sample 3: nxbbzo20r.exe**
- Hash: 038bdd94f0ca54f607e40c2eb72f9c9225cc09c8d20bf927f190bf5fdc46712d
- Detection: 47/70
- C2: http://trendion.cyou/ — 401 Unauthorized

**Infrastructure map:**
```
eja4yagm.exe  ──►  matchny.cyou   ──►  64.89.161.173
Setup.exe     ──►  bizsmmit.cyou  ──────────────┤
nxbbzo20r.exe ──►  trendion.cyou  ──────────────┘
```

---

## VirusTotal Relations

- 9 contacted domains — 7 .cyou domains registered July 23–24 via Dynadot Inc
- C2 IP: 64.89.161.173 (AS205759 Ghosty Networks LLC)
- 73 .cyou domains resolving to this IP since July 15, 2026
- 111 malware samples confirmed communicating with this IP

**Delivery filenames from communicating files:**
- SETUP.zip — fake software installer
- The Odyssey (2026) 1080p WEBRip.zip — fake movie torrent
- The Odyssey 2160pHD (2026) ENGSubs.zip — fake movie torrent
- House of the Dragon S03E07 1080p.zip — fake TV show torrent
- Amazon Best Books of the Month - July 2026 — fake ebook
- ProtonVPN_v5.1.5_Premium.exe — fake VPN software
- clean_virus.exe — fake antivirus tool

---

## Infrastructure Fingerprinting

### Shodan
- Location: Lincoln, United States
- OS: Linux Ubuntu
- Open ports: 22/SSH (OpenSSH 8.9p1), 80/HTTP (401 Unauthorized)

### Censys
- OS: Canonical Linux
- Network: AS205759 GHOSTYNETWORKS
- Tag: REMOTE_ACCESS
- Services: 22/SSH, 80/HTTP, 27015/VALVE, 27059/VALVE
- Note: Valve gaming ports suggest dual-use server

---

## Any.run Sandbox

**bizsmmit.cyou:**
- Verdict: Malicious activity
- Tags: lumma, stealer
- Listed in Spamhaus DROP
- IDS rule triggered: ET MALWARE Lumma Stealer Victim Fingerprinting Activity
- Destination: 64.89.161.173:80

**trenadne.cyou:**
- API call: /api/set_agent with victim ID and token
- DNS A record resolved to 64.89.161.173
- Canvas fingerprinting detected
- 117 HTTP requests, 159 connections, 124 DNS requests, 5 network threats

---

## VirusTotal — Domain Detection

**trenadne.cyou:**
- Detection: 12/91 vendors
- Registrar: Dynadot Inc
- Age: 15 days at time of analysis
- Vendors: alphaMountain.ai, AlphaSOC, Certego, CRDF, Dr.Web, ESET, Forcepoint ThreatSeeker, Fortinet, SafeToOpen, Seclookup, SOCRadar, VIPRE

---

## Kaspersky OpenTIP

- Trojan-PSW.Win32.Lumma.adyb
- Trojan-PSW.Win32.Lumma.sb
- Trojan-PSW.Stealerc.HTTP.C&C
- PDM:Trojan.Win32.Generic
- Backdoor.Win32.Gsb.gen

PSW = Password Stealer. Backdoor.Win32.Gsb indicates persistent backdoor access beyond credential theft.

---

## Attacker OPSEC Failures

1. Same-day batch domain registration via one registrar — temporal fingerprint in WHOIS
2. All 73 C2 domains on one IP — full infrastructure exposed in single VirusTotal pivot
3. Consistent .cyou TLD across all domains — single DNS detection rule catches entire cluster
4. HTTP 401 on port 80 reveals active backend — should return blank or drop connection
5. Imphash shared across 464 samples — single MalwareBazaar search exposed cross-family cluster

---

## Attack Flow

```
Victim downloads fake torrent / fake software
  → Executes trojanized ZIP contents
    → Malware fingerprints system via /api/set_agent
      → Credentials harvested from Chrome and Edge
        → Data exfiltrated via HTTPS POST to .cyou C2 domain
          → C2 rotates to new domain next day
```

---

## Featured Medium Article

**The Fake Odyssey 2026 Download Was Malware — and It Led Me to a Live Lumma Stealer C2 Network**

🔗 https://medium.com/@H3NRYB41T/the-fake-odyssey-2026-download-was-malware-and-it-led-me-to-a-live-lumma-stealer-c2-network-0d614664ef12
