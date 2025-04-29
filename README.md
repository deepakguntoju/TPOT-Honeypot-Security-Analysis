# 🛡️ TPOT Honeypot for Threat Intelligence & Security Analytics on GCP

This project involves the deployment and operation of the [TPOT](https://github.com/telekom-security/tpotce) honeypot platform on **Google Cloud Platform (GCP)**. The goal is to **collect real-world malicious traffic**, analyze threat data using integrated tools like **Suricata**, **Cowrie**, and **Dionaea**, and extract actionable intelligence to improve security posture.

---

## 🎯 Project Objectives

- Deploy a production-grade honeypot in the cloud using TPOT.
- Capture malicious activity targeting exposed services (e.g., SSH, SMB, HTTP).
- Analyze collected data to identify attack patterns, IOCs, and commonly exploited CVEs.
- Correlate findings to MITRE ATT&CK techniques.
- Generate security insights and defense recommendations based on real-world data.

---

## 🔧 Tools & Technologies

| Tool       | Purpose                               |
|------------|---------------------------------------|
| TPOT       | Full-featured honeypot platform       |
| Suricata   | Network-based IDS/IPS                 |
| Cowrie     | SSH and Telnet honeypot               |
| Dionaea    | Malware collection and analysis       |
| Kibana     | Log analysis and visualization        |
| GCP        | Infrastructure hosting(Compute Engine)|
| Docker     | Containerized service deployment      |

---

## 🚀 Deployment Overview

### 1. Infrastructure Setup on GCP
- Provisioned a **Compute Engine VM** with:
  - External IP address (open to common attack ports)
  - Minimum: 4 vCPU, 8GB RAM, 65GB SSD disk
- Enabled required firewall rules for:
  - tcp:22, 23, 80, 81, 135, 443, 445, 1433, 3306, 5432, 5900, 6379, 9200, 64295, 64297
  - udp:69, 623, 5000, 5060

### 2. Installing TPOT
- Cloned the TPOT GitHub repo and followed the [official setup instructions](https://github.com/telekom-security/tpotce).
- Used `./install.sh` with autoinstall configuration.
- Docker containers were automatically initialized with:
  - Suricata, Cowrie, Dionaea, Elasticsearch, Logstash, Kibana

### 3. Services Exposed
- SSH honeypot (via Cowrie)
- SMB, HTTP, FTP emulated via Dionaea
- Suricata for real-time network inspection

---

## 📊 Analysis & Findings

### 🔍 Suricata (Network IDS)
- Top 10 Suricata Alert Signatures
- Most frequent CVEs (e.g., CVE-2018-10561)
- Top attacking IPs and ASNs
- Commonly targeted ports

### 🐚 Cowrie (SSH Honeypot)
- Top attempted usernames: `root`, `admin`, `oracle`
- Repeated password guessing and brute-force login attempts
- Executed post-login commands captured in session logs

### ☣️ Dionaea (Malware Collection)
- Malware payload download attempts
- Exploit attempts on SMB and HTTP ports
- Captured file hashes and metadata (MD5, SHA256)

---

## 🧠 Threat Intelligence Insights

- Attackers originated from a wide range of ASNs, with clusters in specific geographic regions.
- Consistent targeting of weak credentials via SSH brute-force (MITRE ATT&CK T1110).
- Multiple attempts to exploit legacy SMB vulnerabilities (T1210 - Exploitation of Remote Services).
- Collected malware samples indicated botnet command-and-control behavior.

---

## 📸 Visuals & Screenshots

All screenshots are available in the [`/images/`](./images) directory:

- TPOT Dashboard (tpot-dashboard.png)
- Suricata Top Signatures (suricata-alerts.png)
- Cowrie Command Logs (cowrie-ssh.png)
- Dionaea Malware Attempts (dionaea-malware.png)
- Kibana Dashboards (kibana-visualization.png)
- MITRE ATT&CK Mapping (mitre-attack-correlation.png)

---

## 🛠️ Recommendations Based on Findings

- Implement geo-blocking and stricter ingress rules in cloud firewall.
- Monitor and alert on Suricata high-severity events.
- Patch legacy services and remove unused ports (e.g., SMB if not needed).
- Harden SSH configurations (e.g., disable password login, allow only key-based auth).


