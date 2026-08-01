# Case Study: fatturapagamento.click — Live Phishing Infrastructure Analysis

**Date:** August 1, 2026
**Author:** Abdullah Hassan
**Type:** Phishing — Aruba impersonation
**Target:** Italian-speaking users
**Status at discovery:** ONLINE

---

## The Phishing Page

**URL:** `https://fatturapagamento.click/loading/`

A fake Aruba "Area Clienti" (Customer Area) login page designed to steal Aruba account credentials. Confirmed on PhishTank as Submission #9493515 with 100% community agreement.

---

## WHOIS

- **Registered:** 2026-07-27 (5 days before discovery)
- **Expires:** 2027-07-27
- **Status:** client transfer prohibited
- **Nameservers:** augustus.ns.cloudflare.com / laura.ns.cloudflare.com

---

## DNS

- **A Record:** fatturapagamento.click → 185.95.156.79
- **TTL:** 300 seconds (suspicious — very short)
- **Owner:** MyAcct LTD / AS209101

---

## IP Reputation

**GreyNoise:** Not Observed — no mass scanning detected. Targeted delivery only.

**AbuseIPDB:** 0 reports. 0% confidence of abuse. Clean reputation.

**Criminal IP:** No results. Unknown to their threat intelligence database.

---

## Infrastructure Fingerprinting

### Censys
- OS: Debian Linux
- 15 open services including full email stack
- Tags: LOGIN_PAGE, REMOTE_ACCESS, WAF
- Forward DNS reveals co-hosted domain clusters

### Shodan
- Location: Frankfurt am Main, Germany
- Organization: MyAcct LTD
- ISP: AEZA International LTD / AS210644
- Port 53 DNS resolver name: www.backup-exodus.com
- Port 443 SSL cert issued for: payment-invoice.click

### FOFA
- Port 25 SMTP banner: `220 www.backup-exodus.com ESMTP Postfix (Debian/GNU)`

---

## URLScan.io

- 5 IPs contacted across 3 countries
- 6 HTTP transactions
- 10,000+ similar pages found on different IPs and domains
- Outgoing link exposed: `https://185.95.156.79:10000/` — Virtualmin admin panel

---

## VirusTotal

- Score: 10/92 vendors flagged as malicious
- Detections: Phishing (alphaMountain.ai, BitDefender, Cluster25, ESET, Fortinet, G-Data, Gridinsoft, SOCRadar, VIPRE) / Malware (Sophos)

**Redirection chain:**
```
https://fatturapagamento.click/loading/
  → https://fatturapagamento.click/.submit/
    → https://www.youtube.com/
```

---

## Passive DNS — AlienVault OTX

- fatturapagamento.click → 185.95.156.79 (2026-07-28 to 2026-07-31) — AS211936 rackdog llc, Bulgaria
- payment-invoice.click → 185.95.156.79 (2026-07-19) — AS211936 rackdog llc, Bulgaria

---

## Full Domain Cluster — VirusTotal Relations (20 Domains)

**payment-invoice.click cluster (July 19)**
- payment-invoice.click — 3/91
- www.payment-invoice.click — 4/91
- admin.payment-invoice.click — 0/91
- mail.payment-invoice.click — 0/91
- webmail.payment-invoice.click — 0/91

**membership-premium.info cluster (July 25)**
- membership-premium.info — 0/91
- www.membership-premium.info — 0/91
- admin.membership-premium.info — 0/91
- mail.membership-premium.info — 0/91
- webmail.membership-premium.info — 0/91

**fatturapagamento.click cluster (July 27)**
- fatturapagamento.click — 8/91
- www.fatturapagamento.click — 5/91
- admin.fatturapagamento.click — 0/91
- mail.fatturapagamento.click — 0/91
- webmail.fatturapagamento.click — 0/91

**backup-exodus.com cluster (July 28)**
- backup-exodus.com — 11/91
- www.backup-exodus.com — 7/91
- admin.backup-exodus.com — 6/91
- mail.backup-exodus.com — 6/91
- webmail.backup-exodus.com — 6/91

---

## Certificate Transparency — crt.sh

All 4 certificates issued on 2026-07-27 (same day as domain registration):
- Cloudflare TLS Issuing ECC CA 4
- Google Trust Services CN=WE1
- Let's Encrypt CN=YR1 (x2)

---

## MXToolbox

- 185.95.156.79 checked against 60 email blacklists
- Result: 0/60 listed
- Clean mail reputation — phishing emails would bypass spam filters

---

## Attacker OPSEC Failures

1. Virtualmin panel left public on port 10000
2. Short TTL (300s) drew immediate attention
3. All 4 campaigns hosted on one IP — full infrastructure exposed in single pivot
4. SMTP banner leaked backup-exodus.com
5. Multi-CA certificates issued simultaneously flagged in crt.sh
6. ETag fingerprint `13255-656ecbe3ae000` enables kit hunting on Shodan
7. DNS resolver name exposed www.backup-exodus.com

---

## Attack Flow

```
Phishing Email (via backup-exodus.com SMTP)
  → fatturapagamento.click/loading/ (fake Aruba login)
    → Credentials POSTed to /.submit/
      → Victim redirected to YouTube
```

---

##  Featured Medium Article

**How I Traced a Fake Aruba Payment Portal Back to Its Infrastructure Using 12 Free OSINT Tools**

🔗 https://medium.com/@H3NRYB41T/how-i-traced-a-fake-aruba-payment-portal-back-to-its-infrastructure-using-12-free-osint-tools-1dfe398bc7f5
