# SOC Analyst Home Lab: Detection & Monitoring

## 📌 Project Overview
This repository contains a professional-grade Security Operations Center (SOC) home lab environment. The project focuses on deploying a centralized security monitoring system (EDR/SIEM) to detect threats, monitor system integrity, and analyze security events in real-time.

## 🏗️ Tech Stack
* **SIEM/EDR:** Wazuh Stack (Indexer, Manager, Dashboard)
* **Deployment:** Docker / Docker-compose (Single-node setup)
* **Hosts Monitored:** macOS (Native Agent), Docker Host (Linux)
* **Key Skills:** Log analysis, Configuration management, Troubleshooting, SIEM Engineering

## 🛠️ Implementation Details
The lab is built on a **Wazuh single-node deployment** within a Docker environment. This setup allows for rapid testing of detection rules and centralized log management.

* **Endpoint Monitoring:** Deployed Wazuh agents to collect security telemetry and monitor File Integrity (FIM).
* **Configuration Management:** Customized `ossec.conf` to handle macOS-specific agent requirements.
* **Automation:** Utilized Docker for consistent environment state and easy scaling.

## 📂 Project Structure
* `wazuh-docker/`: Contains all Docker-compose files and configurations.
* `lab-setup/`: Technical documentation of the deployment process.
* `docs/`: Detailed guides and research notes.
* `troubleshooting.md`: **(Crucial)** Documentation of bugs found during setup and their solutions.

## 🎯 Current Status: Detection Scenarios
*Developing custom rules for:*
1.  **Unauthorized Access:** Detecting failed login attempts and privilege escalation.
2.  **FIM (File Integrity Monitoring):** Monitoring sensitive system directories for unauthorized changes.
*(Detailed walkthroughs coming soon)*

---
*Note: This lab is an ongoing project focused on defensive security and SIEM engineering.*
