<div align="center">

# 30-Day Cyber Threat Intelligence Program

*A self-directed journey from zero to threat analyst — one investigation at a time.*

[![Status](https://img.shields.io/badge/Status-Week%203%20Complete-brightgreen?style=for-the-badge)](.)
[![Tools](https://img.shields.io/badge/Tools-13%20Free%20OSINT-blue?style=for-the-badge)](.)
[![Method](https://img.shields.io/badge/Method-Passive%20OSINT%20Only-orange?style=for-the-badge)](.)

</div>

---

## What Is This?

This repository documents my **30-day self-study Cyber Threat Intelligence (CTI) program** — a structured curriculum where I investigate real, live threat infrastructure every week using only free, passive OSINT tools.

No simulations. No CTF labs. **Real phishing domains. Real malware infrastructure. Real threat actors.**

Every week ends with a full investigation write-up published on Medium and documented here with IOCs, techniques, and findings.

---

## Progress

| Week | Focus Area | Days | Status | Case Study | Write-up |
|------|------------|------|--------|------------|----------|
| **Week 1** | Infrastructure Intelligence | 1–7 | ✅ Complete | fatturapagamento.click | [Read on Medium](https://medium.com/@H3NRYB41T/how-i-traced-a-fake-aruba-payment-portal-back-to-its-infrastructure-using-12-free-osint-tools-1dfe398bc7f5) |
| **Week 2** | Malware Intelligence | 8–14 | ✅ Complete | Lumma Stealer C2 Network | [Read on Medium](https://medium.com/@H3NRYB41T/the-fake-odyssey-2026-download-was-malware-and-it-led-me-to-a-live-lumma-stealer-c2-network-0d614664ef12) |
| **Week 3** | Threat Actor Intelligence | 15–21 | ✅ Complete | SideWinder APT | [Read on Medium](https://medium.com/@H3NRYB41T/sidewinder-apt-faked-pakistans-government-websites-for-12-years-and-replaced-detected-malware-in-ea16137488eb) |
| **Week 4** | Intelligence Production | 22–30 | ⏳ Pending | — | — |

---

## Full 30-Day Curriculum

<details>
<summary><b>Week 1 — Infrastructure Intelligence</b> ✅</summary>

| Day | Topic | Status |
|-----|-------|--------|
| Day 1 | Infrastructure Pivoting | ✅ |
| Day 2 | Certificate Intelligence | ✅ |
| Day 3 | Web Fingerprinting | ✅ |
| Day 4 | Shodan & Censys | ✅ |
| Day 5 | DNS Intelligence | ✅ |
| Day 6 | Infrastructure Clustering | ✅ |
| Day 7 | Weekly Investigation #1 — fatturapagamento.click | ✅ |

**What I built:** Mapped a live 4-domain phishing campaign from a single URL to full infrastructure exposure — including the attacker's open admin panel.

[View Week 1 Files](./week-1/)

</details>

<details>
<summary><b>Week 2 — Malware Intelligence</b> ✅</summary>

| Day | Topic | Status |
|-----|-------|--------|
| Day 8  | Malware Ecosystem | ✅ |
| Day 9  | Config Extraction | ✅ |
| Day 10 | Campaign Clustering | ✅ |
| Day 11 | Malware Timeline | ✅ |
| Day 12 | Infrastructure Reuse | ✅ |
| Day 13 | ATT&CK Profiling | ✅ |
| Day 14 | Weekly Investigation #2 — Lumma Stealer C2 Network | ✅ |

**What I built:** Traced three unrelated malware samples to a single C2 IP hosting 73 rotating domains and 111 confirmed samples — delivered inside fake movie torrents, fake VPN software, and fake antivirus tools.

[View Week 2 Files](./week-2/)

</details>

<details>
<summary><b>Week 3 — Threat Actor Intelligence</b> ✅</summary>

| Day | Topic | Status |
|-----|-------|--------|
| Day 15 | Actor Selection | ✅ |
| Day 16 | Victimology | ✅ |
| Day 17 | Infrastructure History | ✅ |
| Day 18 | Operational Behavior | ✅ |
| Day 19 | Financial Ecosystem | ✅ |
| Day 20 | Attribution Assessment | ✅ |
| Day 21 | Weekly Investigation #3 — SideWinder APT | ✅ |

**What I built:** Full threat actor profile of SideWinder APT — 12 years of Pakistani government impersonation, 22 ATT&CK techniques, 9 hosting providers, nuclear facility targeting, and under-5-hour malware replacement documented.

[View Week 3 Files](./week-3/)

</details>

<details>
<summary><b>Week 4 — Intelligence Production</b> ⏳</summary>

| Day | Topic | Status |
|-----|-------|--------|
| Day 22 | Intel Requirements | ⏳ |
| Day 23 | Collection Planning | ⏳ |
| Day 24 | Strategic Report | ⏳ |
| Day 25 | Operational Report | ⏳ |
| Day 26 | Threat Hunting Plan | ⏳ |
| Day 27 | Detection Engineering | ⏳ |
| Day 28 | Final Investigation | ⏳ |
| Day 29 | Portfolio Review | ⏳ |
| Day 30 | Advanced Tool Deep-Dives | ⏳ |

[View Week 4 Files](./week-4/)

</details>

---

## Tools Arsenal

> All tools are **100% free**. All investigations use **passive OSINT only** — no active exploitation, no unauthorized access.

| Category | Tools |
|----------|-------|
| Phishing Intel | PhishTank, urlscan.io |
| Malware & URL Analysis | VirusTotal, AlienVault OTX, MalwareBazaar, Any.run |
| Domain & DNS | WHOIS, crt.sh, MXToolbox |
| Internet Scanning | Shodan, Censys, FOFA |
| IP Reputation | AbuseIPDB, GreyNoise, Criminal IP |
| Threat Actor Intel | MITRE ATT&CK, Kaspersky Securelist, Zscaler ThreatLabz, Group-IB |

---

## Investigation Highlights

**Week 1 — fatturapagamento.click**
> One phishing URL. One IP. Four campaigns. Twenty domains. Admin panel wide open on port 10000.

- Single IP hosting 4 simultaneous phishing campaigns
- 20 domains mapped from a single pivot
- 0/60 email blacklists — clean reputation, ready to deliver
- 10,000+ similar phishing pages found on urlscan.io

[Read on Medium](https://medium.com/@H3NRYB41T/how-i-traced-a-fake-aruba-payment-portal-back-to-its-infrastructure-using-12-free-osint-tools-1dfe398bc7f5) · [Case Study](./week-1/case-study-fatturapagamento.md) · [IOCs](./week-1/iocs.txt)

---

**Week 2 — Lumma Stealer C2 Network**
> A fake Odyssey 2026 torrent. Three samples. 73 domains. 111 malware samples. One IP.

- Imphash pivot linked 464 samples across 3 malware families
- 73 .cyou domains all registered via Dynadot in batch sessions
- Delivered inside fake movie torrents, fake VPN software, fake antivirus tools
- 10 ATT&CK techniques documented from behavioral analysis alone

[Read on Medium](https://medium.com/@H3NRYB41T/the-fake-odyssey-2026-download-was-malware-and-it-led-me-to-a-live-lumma-stealer-c2-network-0d614664ef12) · [Case Study](./week-2/case-study-lumma-stealer.md) · [IOCs](./week-2/iocs.txt)

---

**Week 3 — SideWinder APT**
> 12 years. Fake government websites. Nuclear facility lures. Malware replaced in under five hours.

- Pakistan Standard Time check hard-coded into malware — only infected Pakistani systems
- NEPRA website compromised — malware hosted on Pakistan's own power regulator server
- 9 hosting providers across 10 months — rotated after every detection
- 22 ATT&CK techniques documented across the full operation

[Read on Medium](https://medium.com/@H3NRYB41T/sidewinder-apt-faked-pakistans-government-websites-for-12-years-and-replaced-detected-malware-in-ea16137488eb) · [Case Study](./week-3/case-study-sidewinder.md) · [IOCs](./week-3/iocs.txt)

---

## Follow Along

[![Medium](https://img.shields.io/badge/Medium-Follow-black?style=for-the-badge&logo=medium)](https://medium.com/@H3NRYB41T)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0077B5?style=for-the-badge&logo=linkedin)](https://linkedin.com/in/abdullah-hassan123)

---

<div align="center">

*All findings are from passive OSINT only.*
*No systems were accessed without authorization.*

</div>
