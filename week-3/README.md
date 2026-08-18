# Week 3 — Threat Actor Intelligence

## What I Learned This Week

| Day | Technique |
|-----|-----------|
| Day 15 | Actor Selection — Choosing SideWinder APT based on personal relevance and reporting volume |
| Day 16 | Victimology — Mapping 12 years of targeting across Pakistan, South Asia, and maritime infrastructure |
| Day 17 | Infrastructure History — Nine hosting providers, shared IPs, domain clustering across five reports |
| Day 18 | Operational Behavior — Attack chain analysis from spearphishing to StealerBot in-memory execution |
| Day 19 | Financial Ecosystem — State-sponsored resource assessment, hosting provider rotation patterns |
| Day 20 | Attribution Assessment — Medium confidence India-nexus assessment with documented gaps |
| Day 21 | Weekly Investigation #3 — SideWinder APT full infrastructure and actor profile |

---

## Week 3 Case Study

**Actor:** SideWinder APT
**Aliases:** Rattlesnake · T-APT-04 · RAZOR TIGER · APT-C-17 · Hardcore Nationalist
**MITRE ID:** G0121
**Suspected Origin:** India (medium confidence)
**Active Since:** 2012
**Status:** Active — profile last updated July 31, 2026

### Key Findings
- 12-year operation targeting Pakistan as primary victim from day one
- Compromised NEPRA — Pakistan's national power regulator — and hosted malware on their own web server
- Under five hours to replace detected malware — actively monitored vendor detections in real time
- Built Pakistan Standard Time check into malware — only infected Pakistani systems (T1480 Execution Guardrails)
- AntiBot script filtered researchers by IP, OS, browser, hardware, GPU, screen size, and timezone
- Nine hosting providers across ten months — LeaseWeb, DigitalOcean, AWS, Cloudflare, Hetzner, and more
- Fake institutions built with complete infrastructure: nameservers, mail servers, payload delivery, multiple subdomains
- Shared IPs between fia-gov.org and customs-lk.org confirmed same operator ran Pakistan and Sri Lanka campaigns simultaneously
- WarHawk C2 on DigitalOcean still alive with community score -56 at time of investigation
- 22 MITRE ATT&CK techniques documented across the full operation

### Target Sectors
- Pakistani government ministries and federal agencies
- Pakistani military organizations and defense contractors
- Pakistani critical infrastructure — NEPRA, PTCL, SNGPL
- South Asian nuclear facilities — Rooppur Nuclear Power Plant, Bangladesh
- Maritime infrastructure along the Red Sea shipping corridor
- Diplomatic missions across Africa, Middle East, and Asia

### Tools Used
VirusTotal · MITRE ATT&CK · Kaspersky Securelist · Zscaler ThreatLabz · Group-IB · BlackBerry Research · The Hacker News

---

## Files

- [case-study-sidewinder.md](./case-study-sidewinder.md) — Full actor profile and investigation
- [iocs.txt](./iocs.txt) — All indicators of compromise
- [attck-mapping.md](./attck-mapping.md) — Full MITRE ATT&CK technique mapping

--

## Medium Post

[SideWinder APT Faked Pakistan's Government Websites for 12 Years and Replaced Detected Malware in Under Five Hours](https://medium.com/@H3NRYB41T/sidewinder-apt-faked-pakistans-government-websites-for-12-years-and-replaced-detected-malware-in-ea16137488eb)
