# Cloud Honeypot Lab: T-Pot on Microsoft Azure

![T-Pot Attack Map](images/tpot-attack-map-live-feed.png)

A secure, ethical deployment of [T-Pot](https://github.com/telekom-security/tpotce) — an all-in-one multi-honeypot platform — on **Microsoft Azure** for threat intelligence and attacker behavior analysis.

> **Ethical Note**: This lab is configured for **passive monitoring only**. No interaction with attackers. All data is anonymized and retained <30 days per privacy best practices.

---

## 🎯 Project Goal

Deploy a production-grade honeypot in the cloud to:
- Capture real-world attack patterns (SSH brute-force, SMB exploits, web scanners, etc.)
- Analyze attacker TTPs (Tactics, Techniques, Procedures)
- Visualize threats using ELK stack (Elasticsearch, Logstash, Kibana)
- Demonstrate cloud security + threat detection skills for SOC/Threat Intel roles

---

## 🛡️ Security & Compliance

| Practice | Implementation |
|--------|----------------|
| **Network Hardening** | Only essential honeypot ports open (22, 23, 80, 443, 445, 3389, etc.) — **never 0–65535** |
| **Authentication** | Strong SSH key + complex T-Pot web UI password |
| **Data Privacy** | Raw logs auto-deleted after 30 days; IPs blurred in public artifacts |
| **Legal Safety** | No outbound connections from honeypots; no personal data collected |

![Azure NSG Rules](images/azure-nsg-rules.png)

---

## 🧪 Key Findings (24-Hour Run)

- **Top Attacked Services**: SSH (72%), HTTP (18%), SMB (6%)
- **Most Common Payloads**: Mirai botnet, Log4j scanners, WordPress brute-force
- **Geographic Hotspots**: Egypt, The Netherland, United States, Bulgaria, Germany
- **Notable CVEs Observed**: CVE-2021-44228 (Log4Shell), CVE-2017-0144 (EternalBlue)

![Attack Map Top Countries](images/tpot-attack-map-top-countries.png)

---

## 🚀 Deployment Steps (Safe & Reproducible)

### Prerequisites
- Azure account ($200 free credit)
- SSH key pair (`ssh-keygen -t rsa -b 4096`)
- Basic Linux/Azure knowledge

### 1. Create Azure VM
- **Image**: Ubuntu Server 22.04 LTS
- **Size**: D4s v3 (4 vCPU, 16 GB RAM)
- **Auth**: SSH public key
- **Auto-shutdown**: Enabled (cost control)

### 2. Configure Network Security
Open **only these inbound ports**: 22 (SSH), 23 (Telnet), 80 (HTTP), 443 (HTTPS),
445 (SMB), 3389 (RDP), 5900 (VNC),
3306 (MySQL), 5432 (PostgreSQL), 6379 (Redis)

> Full port list: [T-Pot Official Ports](https://github.com/telekom-security/tpotce/tree/master?tab=readme-ov-file#required-ports)
