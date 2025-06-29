# TryHackMe SOC 1: Pyramid of Pain

> Notes and reflections from the TryHackMe "Pyramid of Pain" room  
> Part of my cybersecurity learning path (SOC Analyst Track)

---

## 🧠 Overview

The **Pyramid of Pain**, developed by David Bianco, helps defenders understand which types of indicators cause the most "pain" to adversaries when detected or blocked.

---

## 🏗️ The Pyramid Levels

### **Hash Values**
- **Description**: Unique digital fingerprints of malicious files (e.g., MD5, SHA1).
- **Example**: `d41d8cd98f00b204e9800998ecf8427e`
- **Detection Tools**:
  - VirusTotal
  - SIEM hash-based alerts
- **Pain Level**: 🔴 Very Low (easily changed by attacker)
- **My Notes**:
  - Base of pyramid. Easiest level tp verify if a hash is malicious. Easy for attacker to change the hash value of malware.
  - MD5 is not considered cryptographically secure. SHA-1 was banned for use with digital signatures in 2013.
  - SHA-256 most widly used. reRurns a hash value of 256-bits as a 64 digit hexadecimal number.
  - A hash is not considered to be cryptographically secure if two files have the same hash value or digest.

---

### **IP Addresses**
- **Description**: Destination/source IPs used for command and control or attacks.
- **Example**: `192.168.1.100`
- **Detection Tools**:
  - Firewall logs
  - Threat intelligence feeds
- **Pain Level**: 🔴 Low
- **My Notes**:
  - Identify associated IP addresses and domain names of malware. Network activity can query HTTP requests, connections and domain names.
  - From a defensive perspective, identifying the IP addresses used by an attacker can be useful. A common strategy is to block or deny incoming traffic from those IPs at the perimeter or external firewall. However, this approach has limitations, as skilled attackers can easily bypass it by switching to a new public IP address.

  -### 🌀 Fast Flux
Fast Flux is a DNS evasion technique used by attackers to hide malicious infrastructure like phishing sites or command-and-control (C2) servers. It involves rapidly rotating IP addresses associated with a single domain, often using compromised machines as proxies. This makes takedown efforts and detection much harder.


---

### 🌐 Domain Names

Domain names map IP addresses to human-readable text. While easier to rotate than IP addresses, they’re still more painful for attackers to manage since registering and configuring domains takes time and often involves cost.

Many DNS providers make it easy for attackers to automate domain changes using APIs, weakening this layer of defense. Still, defenders can detect malicious domains using proxy or web server logs.

---

#### 🧨 Punycode Attacks

Attackers can disguise malicious domains using **Punycode**, which encodes non-ASCII characters to appear legitimate. These visually deceptive domains trick users into visiting harmful sites.

Modern browsers like Chrome and Safari can detect Punycode, but vigilance is still required.

---

#### 🔗 URL Shorteners Used by Attackers

Common shortener services used to hide malicious domains:
- `bit.ly`
- `goo.gl`
- `ow.ly`
- `s.id`
- `smarturl.it`
- `tinyurl.com`
- `x.co`

**Tip**: Add a `+` to the end of shortened URLs (e.g., `bit.ly/example+`) to preview the destination before visiting.

---

#### 🧪 Sandboxing with Any.run

**Any.run** helps analyze malware behavior, showing:
- **HTTP Requests**: Resources fetched from malicious servers (e.g., droppers, callbacks).
- **Connections**: Host-to-host communications (e.g., FTP, C2 traffic).
- **DNS Requests**: Domain lookups by the malware (used to detect sandbox evasion or connectivity).

⚠️ *Always be cautious when viewing URLs or IPs from malware samples—do not visit them directly.*

---

### 🖥️ Host Artifacts

Host artifacts are clues left behind on a compromised system, such as:
- Suspicious process execution (e.g., `winword.exe` spawning `powershell.exe`)
- Malicious registry keys or services
- Dropped or modified files
- Indicators of Compromise (IOCs) unique to the threat

These artifacts require attackers to significantly alter their methods or tooling if detected—making this level of detection much more **frustrating and time-consuming** for them.

Examples:
- Word launching unexpected scripts or child processes
- System events logged after opening a malicious file
- New or modified files written to disk by the malware

🟡 **Pain Level**: Medium – Forces attacker to retool and reinvest time/resources.

### 🌐 Network Artifacts

Network artifacts fall in the 🟡 **yellow zone** of the Pyramid of Pain. Detecting these forces attackers to modify their C2 traffic, user-agent strings, or URI patterns—slowing them down and giving defenders time to respond.

Common examples include:
- **Unusual User-Agent strings** in HTTP headers
- **Suspicious URI patterns** used in POST requests
- **C2 (Command & Control) domains or IPs**

These indicators can be found in:
- **PCAP files** (e.g., using Wireshark or TShark)
- **IDS logs** from systems like Snort or Suricata

---
### 🛠️ Tools

The high-pain zone for attackers. Detecting and blocking **tools**—like malware builders, backdoors, payload generators, and password crackers—means the adversary must rebuild, repurchase, or relearn their tradecraft. This often leads to frustration, delays, or outright abandonment of the attack.

🧨 Common tool-based artifacts:
- Custom `.exe` or `.dll` files (e.g., `Stealer.exe`)
- Maldoc generators for phishing
- C2 backdoors and droppers

🛡️ Detection Techniques:
- **Antivirus and endpoint detection**
- **YARA rules** (pattern-based malware detection)
- **Fuzzy hashing** (e.g., using `SSDeep`) to identify similar malicious files
- **Community feeds** and rule sets:
  - [MalwareBazaar](https://bazaar.abuse.ch/)
  - [Malshare](https://malshare.com/)
  - [SOC Prime Threat Detection Marketplace](https://tdm.socprime.com/)

Example SSDeep usage (via VirusTotal or local comparison) helps detect polymorphic variants of known tools.

🔵 **Pain Level**: High – Forces attackers to retool, rebuild, or give up.

---
### 🧠 Tactics, Techniques & Procedures (TTPs)

The **apex** of the Pyramid of Pain—**TTPs**, or the strategic behaviors attackers use across an intrusion.

TTPs reflect the **“how”** of an attack, including:
- Phishing campaigns
- Lateral movement (e.g., Pass-the-Hash)
- Persistence methods
- Data exfiltration tactics

This level maps to the entire **MITRE ATT&CK Framework**, giving defenders a structured way to identify and disrupt adversary behavior.

If you're able to detect TTPs early—like catching a Pass-the-Hash attack using Windows Event Logs—you can isolate affected hosts, prevent further access, and **shut down the attack mid-chain**.

🚨 Forcing an attacker to change their TTPs is incredibly costly. At this point, they must:
- Research and learn new methods
- Rebuild or reconfigure tools
- Or give up and move on to another target

🔵 **Pain Level**: Very High – Most effective form of defense; disrupts the entire strategy.


---

## 🔎 Summary

| Level | Indicator Type       | Pain to Attacker |
|-------|----------------------|------------------|
| 1     | Hash Values          | 🔴 Very Low       |     
| 2     | IP Addresses         | 🔴 Low            |       
| 3     | Domain Names         | 🟡 Moderate       |       
| 4     | Artifacts            | 🟡 Medium         |       
| 5     | Tools                | 🟠 High           |       
| 6     | TTPs                 | 🔵 Very High      |

---

## 💬 Personal Takeaways
- ### 🧾 Personal Takeaway

Learning about the Pyramid of Pain really opened my eyes to the layers of cyber threat detection. I used to think blocking IPs and hashes was enough, but now I understand that the real damage to attackers happens when you detect their tools and behaviors (TTPs). It’s not just about reacting—it's about making the attacker’s job harder at every level. This framework is helping me think more like a defender, not just a responder.

---

## 🔗 Resources
- [MITRE ATT&CK Framework](https://attack.mitre.org/)
- [David Bianco’s Pyramid of Pain Blog](https://detect-respond.blogspot.com/2013/03/the-pyramid-of-pain.html)
- [TryHackMe: Pyramid of Pain Room](https://tryhackme.com)

