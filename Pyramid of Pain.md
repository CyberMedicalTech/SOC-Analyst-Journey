# TryHackMe SOC 1: Pyramid of Pain

> Notes and reflections from the TryHackMe "Pyramid of Pain" room  
> Part of my cybersecurity learning path (SOC Analyst Track)

---

## 🧠 Overview

The **Pyramid of Pain**, developed by David Bianco, helps defenders understand which types of indicators cause the most "pain" to adversaries when detected or blocked.

---

## 🏗️ The Pyramid Levels

### 1. **Hash Values**
- **Description**: Unique digital fingerprints of malicious files (e.g., MD5, SHA1).
- **Example**: `d41d8cd98f00b204e9800998ecf8427e`
- **Detection Tools**:
  - VirusTotal
  - SIEM hash-based alerts
- **Pain Level**: 🔴 Very Low (easily changed by attacker)
- **My Notes**:
  - 
  - 

---

### 2. **IP Addresses**
- **Description**: Destination/source IPs used for command and control or attacks.
- **Example**: `192.168.1.100`
- **Detection Tools**:
  - Firewall logs
  - Threat intelligence feeds
- **Pain Level**: 🔴 Low
- **My Notes**:
  - 
  - 

---

### 3. **Domain Names**
- **Description**: Hostnames used by malware (e.g., C2 servers).
- **Example**: `badactor.com`
- **Detection Tools**:
  - DNS logging
  - Passive DNS databases
- **Pain Level**: 🟡 Moderate
- **My Notes**:
  - 
  - 

---

### 4. **Network/Host Artifacts**
- **Description**: Configuration files, registry keys, or log entries left behind by attackers.
- **Example**: `HKCU\Software\BadSoftware`
- **Detection Tools**:
  - Sysmon
  - EDR tools
- **Pain Level**: 🟡 Medium
- **My Notes**:
  - 
  - 

---

### 5. **Tools**
- **Description**: Software used by threat actors (e.g., Mimikatz, Cobalt Strike).
- **Example**: `mimikatz.exe`
- **Detection Tools**:
  - Behavior-based detection
  - File analysis
- **Pain Level**: 🟠 High
- **My Notes**:
  - 
  - 

---

### 6. **Tactics, Techniques, and Procedures (TTPs)**
- **Description**: The “how” of an attacker—their playbook or strategy.
- **Example**: Lateral movement via RDP + Pass-the-Hash (T1021.001 + T1550.002)
- **Detection Tools**:
  - MITRE ATT&CK mapping
  - Threat hunting playbooks
- **Pain Level**: 🔵 Very High (hardest for attacker to change)
- **My Notes**:
  - 
  - 

---

## 🔎 Summary

| Level | Indicator Type       | Pain to Attacker | Notes |
|-------|----------------------|------------------|-------|
| 1     | Hash Values          | 🔴 Very Low       |       |
| 2     | IP Addresses         | 🔴 Low            |       |
| 3     | Domain Names         | 🟡 Moderate       |       |
| 4     | Artifacts            | 🟡 Medium         |       |
| 5     | Tools                | 🟠 High           |       |
| 6     | TTPs                 | 🔵 Very High      |       |

---

## 💬 Personal Takeaways
- 
- 
- 

---

## 🔗 Resources
- [MITRE ATT&CK Framework](https://attack.mitre.org/)
- [David Bianco’s Pyramid of Pain Blog](https://detect-respond.blogspot.com/2013/03/the-pyramid-of-pain.html)
- [TryHackMe: Pyramid of Pain Room](https://tryhackme.com)

