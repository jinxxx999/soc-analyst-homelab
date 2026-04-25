# 🛡️ SOC Analyst Home Lab: Detection & Analysis
## Overview
This project demonstrates a fully functional Security Operations Center (SOC) environment built within a virtualized infrastructure. The goal was to simulate real-world cyber attacks and practice monitoring, detecting, and analyzing security events using industry-standard tools.

## 🏗️ Architecture & Tools
SIEM/Log Management: Splunk / Elastic Stack (ELK)

Endpoint Detection & Response (EDR): Wazuh

Virtualization: Docker / VMware / VirtualBox

Traffic Analysis: Wireshark

OS: Ubuntu (Server), Kali Linux (Attacker), Windows (Victim)

## 🛠️ Lab Setup
The environment was deployed using Docker Compose for rapid scaling and management.

Endpoint Monitoring: Configured Wazuh agents on Windows/Linux endpoints to collect syslogs and monitor file integrity.

Centralized Logging: Integrated Wazuh with Splunk/Elastic for advanced data visualization and long-term retention.

Network Security: Setup pfSense/Snort (если использовала) to capture and inspect network traffic.

📂 Detailed setup instructions can be found in the lab-setup/ directory.

## 🎯 Security Scenarios & Investigations
In this lab, I conducted several attack simulations to test detection capabilities:

1. Brute Force Attack Detection

Attack: Performed an SSH brute force using Hydra from a Kali Linux machine.

Detection: Wazuh triggered a Level 10 alert for "Multiple failed SSH logins."

Analysis: Investigated the logs in Splunk to identify the source IP and the targeted user account.

Outcome: Created a custom rule to block the attacker's IP after 5 failed attempts.

2. Malware Analysis (Example)

Investigation: Analyzed a suspicious .ppt file (Oski Stealer) to identify C2 communication and persistence mechanisms.

Tools Used: VirusTotal, Any.run, Wireshark.

## 📈 Key Achievements
Successfully integrated multiple security tools into a unified monitoring dashboard.

Improved incident response time by creating custom alerting rules.

Gained hands-on experience with log parsing and query languages (SPL/KQL).
