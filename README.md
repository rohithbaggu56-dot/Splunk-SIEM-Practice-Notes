# 🔍 Splunk SIEM – Detection Lab

![Splunk](https://img.shields.io/badge/Splunk-000000?style=for-the-badge&logo=splunk&logoColor=white)
![MITRE ATT&CK](https://img.shields.io/badge/MITRE_ATT%26CK-FF0000?style=for-the-badge)

Hands-on Splunk log analysis using SSH, DNS, Apache, and Cloudflare log sources. Built SPL queries to detect attack patterns and created dashboards for ongoing monitoring across multiple log types.

---

## 🖥️ Log Sources Analyzed

| Source | What It Shows |
|---|---|
| SSH logs | Authentication events, brute force attempts, source IPs |
| DNS logs | Query frequency, top queried domains, potential C2 patterns |
| Apache logs | Web requests, client errors, server errors, top URIs |
| Cloudflare logs | WAF blocks, WAF challenges, web traffic by geography |

---

## 📂 What Was Built and Detected

---

### 🔴 DNS Log Analysis & C2 Detection

Analyzed DNS query logs to identify high-frequency domain queries that could indicate C2 beaconing behavior.

**SPL query — top queried domains by count across 1,200 DNS events:**

```spl
index=dns_lab
| stats count by query
| sort -count
```

**Results showing top queried domains — google.com and printer.local both at 139 queries, followed by example.com at 137:**

<img width="1920" height="961" alt="Splunk-Dns log-Search" src="https://github.com/user-attachments/assets/aca78ec3-e904-424d-bcaa-114315fd81d1" />

<br>

- Identified printer.local generating the same query volume as google.com which is unusual for a local device
- High-frequency queries to internal hostnames like fileserver.local, router.local, backup.local suggest automated resolution behavior worth investigating
- 📌 MITRE: `T1071.004` DNS · `T1568` Dynamic Resolution

---

### 🔴 SSH Brute Force Detection Dashboard

Built a Splunk dashboard to monitor SSH authentication events and identify brute force patterns across 2,400 total SSH events.

**SSH logins dashboard — 610 failed logins, 572 connections without authentication, failed logins by username and source IP geolocation:**

![Splunk SSH-log-dashboard](https://github.com/user-attachments/assets/84ea7641-f3f2-414a-a43f-60569542490b)

<br>

- 610 failed logins out of 2,400 total SSH events — 25.4% failure rate indicating active brute force activity
- Top targeted usernames: root, backup, alice, admin, test — all common default or guessable accounts
- Top attacking IPs: 83.195.24.226 and 25.47.52.197 each with 13 failed attempts, multiple additional IPs with 10+ attempts
- 572 connections without authentication indicate automated scanners probing the service
- 📌 MITRE: `T1110` Brute Force · `T1110.001` Password Guessing · `T1078` Valid Accounts

---

### 🔴 Apache Web Log Analysis Dashboard

Built a dashboard to monitor web server activity and identify error patterns across 4,000 total web requests.

**Apache logs dashboard — 4,000 total requests, 2,336 successful, 752 client errors, 752 server errors, top requested URIs and source IPs:**

![Splunk Apache-log-dashboard](https://github.com/user-attachments/assets/9f23ca5a-e1db-413c-af62-80473d4b5a45)

<br>

- 752 client errors and 752 server errors — unusually equal ratio worth investigating as a potential scanning pattern
- Top requested URIs visible in dashboard — monitored for directory traversal and SQLi patterns in URI paths
- Traffic concentrated from US-based IP ranges based on geographic visualization
- 📌 MITRE: `T1190` Exploit Public-Facing Application · `T1046` Network Service Scanning

---

### 🔴 Cloudflare WAF Log Analysis Dashboard

Analyzed Cloudflare logs to monitor WAF blocking behavior and identify attack traffic patterns across 2,000 total requests.

**Cloudflare logs dashboard — 914 successful responses, 285 WAF challenges, 377 WAF blocks, top requested URIs and geographic traffic map:**

![Splunk Cloudflare-log-dashboard](https://github.com/user-attachments/assets/543ddbf5-e83c-4feb-9c55-13a2b3816b28)

<br>

- 377 WAF blocks out of 2,000 requests — 18.85% block rate indicating significant malicious traffic volume
- Top requested URI `/comments.php?m=...%3Cscript%3E` shows URL-encoded script tag — confirmed XSS attempt blocked by WAF
- 285 WAF challenges suggest additional suspicious but not definitively malicious traffic being flagged
- Traffic predominantly from US-based sources based on geographic map
- 📌 MITRE: `T1059.007` JavaScript · `T1190` Exploit Public-Facing Application

---

## 📁 Repository Structure

```
Splunk-SIEM-Practice-Notes/
├── dashboards/
│   ├── ssh-logins-dashboard.png
│   ├── apache-logs-dashboard.png
│   └── cloudflare-logs-dashboard.png
└── queries/
    └── dns-top-queries.png
```

---

⬅️ [Back to SOC Home Lab](https://github.com/rohithbaggu56-dot/Home-SOC-Lab-Detection-Log-Analysis) · [Back to Portfolio](https://github.com/rohithbaggu56-dot)
