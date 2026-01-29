# Threat Detection & Log Analysis with Splunk

Real-world threat detection using Splunk SIEM and various custom Log Datasets.

---

## 🎯 Project Overview

This project demonstrates:
- **Threat detection** using Splunk SPL queries
- **Incident analysis** with real attack data 
- **MITRE ATT&CK mapping** for threat classification

**Dataset Used:** custom and public security log datasets relevant to each detection scenario

**Technologies:** Splunk Enterprise, SPL (Search Processing Language), Windows Event Logs, Sysmon

---
# **NOTE :** This repository will be continuously updated as new attack scenarios are added.
---

## 📁 Detection Scenarios

### 1. [SSH Brute Force Attack](./01_ssh_bruteforce.md)  
Detection of repeated failed SSH login attempts indicating credential brute-force activity.  
- **Log Source:** [SSH authentication logs](https://drive.google.com/drive/folders/1BL-kVlc3yCRcAH8NnDmAyRm_3j_2mNLM?usp=sharing)
- **MITRE ATT&CK:** T1110.001 (Brute Force: Password Guessing)

### 2. Under Progress...

---

## 🔧 Key Skills Demonstrated

- **SPL Query Development** - stats, timechart, transaction, rex, eval commands
- **Log Analysis** - Windows Event Logs and Sysmon correlation
- **Threat Detection** - Pattern recognition and anomaly detection
- **Incident Investigation** - Timeline reconstruction and IOC identification
- **Technical Documentation** - Clear explanations with visual evidence

---

## Final Structure [Threat Detection & Log Analysis with Splunk]

```
Threat-Detection-Log-Analysis-Splunk/
│
├── README.md
│  
├── 01_ssh_bruteforce.md
│  
├── Detection_Images/
│   └── ssh_bruteforce/
│       
└── What_I_Learned.md

```

## 📬 Contact

**LinkedIn:** [linkedin.com/in/ashish6t7](https://www.linkedin.com/in/ashish6t7)  
**Email:** ashishkumar173362@gmail.com

**Related Project:** [Enterprise SOC Lab](https://github.com/ashish6t7/Enterprise-SOC-Lab) - Lab infrastructure and SIEM deployment

---

## Author

- Ashish Kumar **( CompTIA Security+ Certified )** - Aspiring SOC Analyst  

---

## Disclaimer

All datasets are used strictly for educational purposes.  
No real systems were harmed.
