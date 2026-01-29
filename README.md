# Cloud Honeypot Lab: T-Pot on Microsoft Azure

![T-Pot Attack Map](images/tpot-attack-map-live-feed.png)

**Production-style cloud honeypot deployment** using **T-Pot CE on Microsoft Azure** to collect real-world attack telemetry, analyze adversary behavior, and demonstrate SOC and threat intelligence workflows.

This project reflects how blue teams safely deploy deception technology in cloud environments to observe attacker activity without exposing production systems.

> **Ethical & Legal Note**  
> This lab is configured for **passive monitoring only**.  
> No attacker interaction, no exploitation, and no outbound attack traffic.  
> All collected data is anonymized and retained for less than 30 days.

---

## 🎯 Project Objective

The objective of this lab was to deploy, secure, and operate a cloud-based honeypot to:

- Capture **real-world attack activity** (SSH brute force, web scanning, SMB probing)
- Observe attacker **Tactics, Techniques, and Procedures (TTPs)**
- Visualize attack telemetry using the **ELK stack** (Elasticsearch, Logstash, Kibana)
- Demonstrate **cloud security, detection, and threat intelligence skills** relevant to SOC and Blue Team roles

---

## Security & Compliance Controls

| Control Area | Implementation |
|-------------|----------------|
| **Network Hardening** | Only required honeypot service ports exposed — **never full port ranges** |
| **Authentication** | SSH key-based access with strong T-Pot web UI credentials |
| **Data Privacy** | Logs automatically expired after 30 days; IPs blurred in shared artifacts |
| **Legal Safety** | Honeypots restricted to inbound traffic only; no outbound connections |

![Azure NSG Rules](images/azure-nsg-rules.png)

---

## Observed Attack Activity (24-Hour Window)

During a controlled 24-hour collection period, the honeypot recorded continuous unsolicited attack traffic.

### High-Level Findings
- **Top Targeted Services**
  - SSH – 72%
  - HTTP – 18%
  - SMB – 6%

- **Common Attack Patterns**
  - SSH brute-force attempts
  - Automated web vulnerability scanning
  - SMB enumeration and probing

- **Payloads & Tooling Observed**
  - Mirai botnet variants
  - Log4j (Log4Shell) exploit scanners
  - WordPress brute-force scripts

- **Top Source Regions**
  - Egypt
  - Netherlands
  - United States
  - Bulgaria
  - Germany

![Attack Map – Top Countries](images/tpot-attack-map-top-countries.png)

---

## MITRE ATT&CK Mapping

Observed attacker behavior was mapped to **MITRE ATT&CK** techniques to provide SOC-relevant threat context.

| Technique ID | Technique Name | Evidence |
|-------------|----------------|---------|
| **T1110** | Brute Force | Repeated SSH authentication attempts |
| **T1046** | Network Service Discovery | Broad scanning of exposed services |
| **T1595** | Active Scanning | Automated reconnaissance activity |
| **T1190** | Exploit Public-Facing Application | Log4j and web exploit probes |
| **T1021.002** | SMB/Windows Admin Shares | SMB probing and enumeration |

This demonstrates how raw honeypot telemetry can be translated into **actionable threat intelligence**.

---

## Deployment Architecture

### Prerequisites
- Microsoft Azure account (Free Tier / $200 credit)
- SSH key pair (`ssh-keygen -t rsa -b 4096`)
- Basic Linux and Azure networking knowledge

### Azure VM Configuration
- **OS**: Ubuntu Server 22.04 LTS
- **VM Size**: D4s v3 (4 vCPU, 16 GB RAM)
- **Authentication**: SSH public key only
- **Cost Control**: Auto-shutdown enabled

### Network Security Configuration
Only the following inbound ports were opened to support T-Pot honeypots:
22 SSH
23 Telnet
80 HTTP
443 HTTPS
445 SMB
3389 RDP
5900 VNC
3306 MySQL
5432 PostgreSQL
6379 Redis


> Port exposure strictly follows official T-Pot requirements  
> Reference: https://github.com/telekom-security/tpotce#required-ports

---

## Analyst Takeaways

This project demonstrates hands-on capability in:

- **Cloud Security Engineering**
  - Secure Azure VM deployment
  - Network Security Group (NSG) hardening
- **Threat Intelligence Collection**
  - Safe observation of real attacker behavior
  - Identification of automated attack patterns
- **SOC-Relevant Analysis**
  - Mapping telemetry to MITRE ATT&CK
  - Understanding early-stage attacker reconnaissance
- **Operational Discipline**
  - Ethical boundaries
  - Data privacy controls
  - Cost and exposure management

---

## Future Enhancements

Planned improvements include:
- Forwarding honeypot logs into **Microsoft Sentinel** for SIEM correlation
- Automated ATT&CK technique tagging
- Long-term trend analysis across regions
- Alerting on high-risk exploit attempts

---

## Why This Matters to Employers

This lab shows the ability to:
- Deploy and secure **real cloud infrastructure**
- Collect and analyze **live threat data**
- Translate raw telemetry into **SOC-usable intelligence**
- Operate safely within **legal and ethical boundaries**

This mirrors how enterprise blue teams and managed SOCs use honeypots for early threat detection and intelligence gathering.

