# 📁 Threat Analysis Overview

This folder contains curated threat intelligence outputs from the TPOT Honeypot deployed on GCP. Each file represents an insight generated from the collected malicious activity targeting the honeypot.

---

## 📊 CSV Reports

### `Attacker AS_N - Top 10.csv`
Lists the top 10 autonomous systems (ASNs) from which malicious traffic originated. Useful for identifying ISP-level threat clustering and botnet infrastructure.

### `Cowrie - Top Downloads.csv`
Captured download attempts via Cowrie (SSH honeypot). Shows which malware or payloads attackers tried to fetch after initial access.

### `Password Tagcloud.csv`
A tag cloud representation of attempted passwords against the SSH honeypot. Reveals brute-force trends and common credential reuse.

### `Suricata Alert Signature - Top 10.csv`
Top 10 triggered Suricata rules (signatures), indicating the most common types of attacks detected (e.g., exploit attempts, malware beacons).

### `Suricata CVE - Top 10.csv`
Most frequently observed CVEs based on Suricata rule matches. Highlights which known vulnerabilities are being targeted in the wild.

### `Suricata Source IP - Top 10.csv`
Top 10 attacker IP addresses triggering Suricata alerts. Can be used for blacklist generation or further threat enrichment.

### `Username Tagcloud.csv`
Visualization data of attempted usernames against Cowrie. Reveals common targets like `root`, `admin`, and default system users.

---

## 🖼️ Screenshots & Visualizations

### `ET MALWARE log results.png`
Snapshot of Suricata logs filtered by the "ET MALWARE" signature category. Highlights known malware communication or payload delivery patterns.

### `Elasticvue Health.png`
Screenshot from the Elasticvue interface showing Elasticsearch cluster health, document volume, and node status. Demonstrates observability and operational awareness.

### `Log analysis.png`
Dashboard or summary visualization of honeypot dataa. Useful for showcasing high-level trends in attacks, ports, and sources.

---

## 🧠 Usage

These files are referenced in the main project documentation and are intended to:

- Support resume project evidence for security analysis
- Back threat research findings with raw data
- Aid in visual storytelling of observed attacks
- Map real-world threats to the MITRE ATT&CK framework
