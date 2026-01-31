## 📊 Splunk SIEM Practice & Detection Notes  
(Hands-on SOC Analyst Learning)

This section documents my hands-on Splunk practice using real-world style log datasets.  
The focus was on **log ingestion, investigation, detection logic, and dashboard creation**, similar to tasks performed by a SOC Analyst (L1).



## ℹ️ About Splunk (Context)

Splunk is a SIEM platform used by SOC teams to collect, search, analyze, and visualize logs from multiple sources.

In this repository, Splunk was used to:
- Ingest logs from SSH, DNS, HTTP, and Cloudflare sources
- Perform investigation using SPL searches
- Identify suspicious patterns and brute-force behavior
- Visualize security events using dashboards
- Support SOC-style detection and alert triage workflows

**Core Components Used:**
- **Forwarder:** Sends log data to Splunk
- **Index:** Stores and organizes ingested data
- **Search Head:** Used to search, analyze, and build dashboards

This repository focuses on hands-on analysis and detection rather than theoretical explanations.


---
## 🎯 Objective

- Practice SOC-style log investigation using Splunk
- Understand behavior of different log sources (SSH, DNS, HTTP, Cloudflare)
- Detect suspicious activity and brute-force patterns
- Build dashboards to visualize security events
- Develop an alert triage and investigation mindset

---

## 🛠️ Environment Setup

- **SIEM:** Splunk Enterprise (Ubuntu & Windows)
- **Log Sources:**
  - SSH authentication logs
  - Apache HTTP access logs
  - DNS logs (JSON format)
  - Cloudflare HTTP & WAF logs
- **Operating Systems:**
  - Windows (Event Viewer)
  - Linux (Ubuntu / Kali)
- **Data Source:** Simulated lab datasets, TryHackMe, and Haxcamp practice logs

---

## 🔍 What I Practiced & Analyzed

### 🔐 SSH Log Analysis
- Analyzed successful and failed SSH login attempts
- Identified brute-force behavior based on:
  - Multiple failed logins from same IP
  - Attempts against common usernames (`root`, `admin`, `test`)
- Investigated:
  - Source IPs
  - Targeted usernames
  - Authentication failure patterns
- Built SPL queries to:
  - Count failed attempts per IP
  - Detect abnormal login activity

**SOC takeaway:**  
Learned how brute-force attacks appear in logs and how to identify attacker IOCs.

---

### 🌐 DNS Log Analysis
- Ingested DNS logs in JSON format into Splunk
- Analyzed:
  - Most queried domains
  - Internal vs external DNS requests
  - DNS record types (A, AAAA, CNAME, PTR)
- Detected:
  - High-frequency domain queries
  - Failed DNS resolutions
  - Suspicious domain patterns

**SOC relevance:**  
DNS logs help detect malware callbacks, beaconing, and suspicious network activity.

---

### 🌍 HTTP & Apache Log Analysis
- Analyzed Apache HTTP access logs
- Investigated:
  - Total web requests
  - Client errors (400 - 499) and server errors (500 - 599)
  - Suspicious URLs and abnormal request volume
- Practiced identifying:
  - Scanning behavior
  - Reconnaissance attempts
  - Potential web attack patterns

---

### 🛡️ Cloudflare Log Analysis
- Analyzed Cloudflare HTTP and WAF logs
- Investigated:
  - WAF challenges and blocked requests
  - IPs triggering security rules
  - High-risk traffic patterns
- Built dashboards to visualize:
  - Allowed vs blocked traffic
  - Malicious IP distribution
  - Global request behavior

**SOC relevance:**  
Helped understand perimeter security, WAF protections, and web attack mitigation.

---

## 📈 Dashboards Created

- **SSH Login Dashboard**
  - Successful vs failed logins
  - Top attacking IPs
  - Brute-force detection patterns
![Splunk SSH-log-dashboard](https://github.com/user-attachments/assets/d3b850fd-4fb6-423e-af73-f5b3449b511e)

    
- **Apache Logs Dashboard**
  - Request volume
  - Error distribution
  - Client IP behavior
    ![Splunk Apache-log-dashboard](https://github.com/user-attachments/assets/fb70e1a2-ff21-4ef7-90db-dc27c2bd114c)

- **Cloudflare Logs Dashboard**
  - WAF blocks and challenges
  - Malicious traffic sources
  - Geographic attack visibility
    ![Splunk Cloudflare-log-dashboard](https://github.com/user-attachments/assets/5b30069b-8824-4cf5-b7b2-09c578ebec96)


Dashboards were used to quickly understand security events without manually reviewing raw logs.

---

## 🧠 Investigation Mindset Practiced

Followed SOC-style investigation workflow:

1. Initial alert or suspicious observation  
2. Log filtering and correlation  
3. Pattern identification  
4. IOC extraction (IP, domain, username)  
5. Impact assessment  
6. Decision: False Positive vs True Threat  

---

## 🧪 Tools & Technologies Used

- Splunk Enterprise
- SPL (Search Processing Language)
- Linux log analysis (SSH, auth logs)
- Windows Event Logs
- DNS & HTTP protocol analysis
- SOC investigation workflows

---

## 📌 Key Learnings

- Logs tell a story; dashboards help reveal it faster
- SSH brute-force attacks follow recognizable patterns
- DNS analysis is powerful for detecting hidden threats
- Visualization improves SOC efficiency
- Splunk is a core tool for detection and investigation

---
🔗 **Navigation**  
⬅️ [Back to Portfolio](https://github.com/rohithbaggu56-dot)
---
