<div align="center">

#  30-Day Cyber Threat Intelligence Program

*A self-directed journey from zero to threat analyst — one investigation at a time.*

[![Status](https://img.shields.io/badge/Status-Week%201%20Complete-brightgreen?style=for-the-badge)](.)
[![Tools](https://img.shields.io/badge/Tools-13%20Free%20OSINT-blue?style=for-the-badge)](.)
[![Method](https://img.shields.io/badge/Method-Passive%20OSINT%20Only-orange?style=for-the-badge)](.)

</div>

---

##  What Is This?

This repository documents my **30-day self-study Cyber Threat Intelligence (CTI) program** — a structured curriculum where I investigate real, live threat infrastructure every week using only free, passive OSINT tools.

No simulations. No CTF labs. **Real phishing domains. Real malware infrastructure. Real threat actors.**

Every week ends with a full investigation write-up published on Medium and documented here with IOCs, techniques, and findings.

---

##  Progress

| Week | Focus Area | Days | Status | Case Study | Write-up |
|------|------------|------|--------|------------|----------|
| **Week 1** | Infrastructure Intelligence | 1–7 | ✅ Complete | `fatturapagamento.click` | [📖 Read on Medium](https://medium.com/@H3NRYB41T/how-i-traced-a-fake-aruba-payment-portal-back-to-its-infrastructure-using-12-free-osint-tools-1dfe398bc7f5) |
| **Week 2** | Malware Intelligence | 8–14 | 🔄 In Progress | Coming Soon | Coming Soon |
| **Week 3** | Threat Actor Intelligence | 15–21 | ⏳ Pending | — | — |
| **Week 4** | Intelligence Production | 22–30 | ⏳ Pending | — | — |

---

##  Full 30-Day Curriculum

<details>
<summary><b>📁 Week 1 — Infrastructure Intelligence</b> ✅</summary>

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

[→ View Week 1 Files](./week-1/)

</details>

<details>
<summary><b>📁 Week 2 — Malware Intelligence</b> 🔄</summary>

| Day | Topic | Status |
|-----|-------|--------|
| Day 8  | Malware Ecosystem | 🔄 |
| Day 9  | Config Extraction | ⏳ |
| Day 10 | Campaign Clustering | ⏳ |
| Day 11 | Malware Timeline | ⏳ |
| Day 12 | Infrastructure Reuse | ⏳ |
| Day 13 | ATT&CK Profiling | ⏳ |
| Day 14 | Weekly Investigation #2 | ⏳ |

[→ View Week 2 Files](./week-2/)

</details>

<details>
<summary><b>📁 Week 3 — Threat Actor Intel</b> ⏳</summary>

| Day | Topic | Status |
|-----|-------|--------|
| Day 15 | Actor Selection | ⏳ |
| Day 16 | Victimology | ⏳ |
| Day 17 | Infrastructure History | ⏳ |
| Day 18 | Operational Behavior | ⏳ |
| Day 19 | Financial Ecosystem | ⏳ |
| Day 20 | Attribution Assessment | ⏳ |
| Day 21 | Weekly Investigation #3 | ⏳ |

[→ View Week 3 Files](./week-3/)

</details>

<details>
<summary><b>📁 Week 4 — Intelligence Production</b> ⏳</summary>

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

[→ View Week 4 Files](./week-4/)

</details>

---

##  Tools Arsenal

> All tools are **100% free**. All investigations use **passive OSINT only** — no active exploitation, no unauthorized access.

| Category | Tools |
|----------|-------|
|  Phishing Intel | PhishTank, urlscan.io |
|  Malware & URL Analysis | VirusTotal, AlienVault OTX |
|  Domain & DNS | WHOIS, crt.sh, MXToolbox |
|  Internet Scanning | Shodan, Censys, FOFA |
|  IP Reputation | AbuseIPDB, GreyNoise, Criminal IP |

---

##  Week 1 Highlight

> *"One phishing URL. One IP. Four campaigns. Twenty domains. And an admin panel sitting wide open on the public internet."*

**fatturapagamento.click** — A live Aruba impersonation campaign targeting Italian-speaking users, discovered August 1st, 2026.

**Key findings:**
- 🔴 Single IP hosting **4 simultaneous phishing campaigns**
- 🔴 **20 domains** mapped from a single pivot
- 🔴 Attacker's **Virtualmin admin panel exposed** on port 10000
- 🔴 Full email stack (SMTP/POP3/IMAP) via **backup-exodus.com**
- 🔴 **0/60 email blacklists** — clean reputation, ready to deliver
- 🔴 **10,000+ similar phishing pages** found on urlscan.io

[ Full Write-up on Medium]([https://medium.com/@abdullahhassan](https://medium.com/@H3NRYB41T/how-i-traced-a-fake-aruba-payment-portal-back-to-its-infrastructure-using-12-free-osint-tools-1dfe398bc7f5?sharedUserId=H3NRYB41T)) · [📂 Case Study Files](./week-1/case-study-fatturapagamento.md) · [🔴 IOCs](./week-1/iocs.txt)

---

##  Follow Along

I publish a full investigation write-up on Medium at the end of every week.

[![Medium](https://img.shields.io/badge/Medium-Follow-black?style=for-the-badge&logo=medium)](https://medium.com/@H3NRYB41T)

---

<div align="center">

*All findings are from passive OSINT only.*
*No systems were accessed without authorization.*

</div>
