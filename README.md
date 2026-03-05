# 🕵️ Vidar Stealer Campaign Investigation (March 2026)

This project documents the technical investigation and behavioral analysis of a large-scale **Vidar Stealer** campaign identified in March 2026. The analysis focuses on the infrastructure, data exfiltration methods, and automated polymorphism techniques used by the threat actors.

---

## 📊 Campaign Summary
Analysis of the `Malware_Pro_DB.db` dataset reveals a highly organized operation:

* **Total Samples Detected:** 689 unique records.
* **Infrastructure Scope:** 53 Command & Control (C2) servers.
* **Variant Distribution:** Each C2 server manages exactly **13 malware variants**, indicating an automated polymorphic builder used to evade signature-based detection.
* **Activity Peak:** The campaign showed a significant surge in activity during early March 2026.

---

## 🔑 Indicators of Compromise (IoCs)

### 1. SHA256 Hashes (Representative Samples)
The following hashes have been confirmed as malicious through deep behavioral analysis:
* `69c7b3654300bd7f94ba603da9be8f743442dc2e07504685a07f79f1cc318b4c`
* `5923bca62a5df9e12255a6726bccbed3fbb84ba59385cc21d07cac986b2bdcb4`
* `ed7c98b2ea017fb82e7e93806d3a348002e78eb2cd1902c84c3bf664ec1dac38`

### 🌐 C2 Infrastructure
Key Command & Control nodes identified during the investigation:
* `bot.cricket-physio.com`
* `151.247.193.50:443`
* `46.226.162.174:80`
* `ths.jhotpot.com.bd`

---

## 🛠️ Detailed Behavioral Analysis
Analysis from the sandbox environment highlights Vidar’s specific intrusion tactics:

### 📂 Data Targets (Exfiltration)
The malware specifically targets browser-stored credentials and session cookies:
* **Cookie Theft:** Accessing `C:\Users\<USER>\AppData\Local\Microsoft\Windows\INetCookies`.
* **Database Access:** Reading from `C:\Users\<USER>\AppData\Local\Microsoft\Windows\INetCookies\ESE\`.

### 💻 Execution & Stealth
The malware leverages legitimate system processes to mask its malicious activities:
* **Masquerading:** Executing under the guise of `C:\Windows\system32\svchost.exe`.
* **Profile Harvesting:** Utilizing Chrome with the `--profile-directory="Default"` parameter to extract user-specific profile data.

### 🔑 System Tampering (Registry)
Vidar modifies or creates registry keys within the `Software\Microsoft` path to ensure persistence or disable security configurations.

---

## 📜 Methodology & Tools
This investigation was conducted using Python-based scripts on Google Colab, interfacing with the VirusTotal API and processing raw SQLite forensic data. Source code for these tools can be found in the `/scripts` directory.

---
*Disclaimer: This report was generated for cyber threat intelligence and educational purposes.*
