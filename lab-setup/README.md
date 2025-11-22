# SOC Analyst Home Lab

## Overview
This project is a personal **SOC Analyst home lab** designed to simulate real-world security operations.  
It demonstrates hands-on skills in **SIEM deployment, attack simulation, log analysis, and incident reporting**, making it ideal for a resume or portfolio.

---

## Tech Stack
- **SIEM Tools:** Splunk, Wazuh, Elastic Stack  
- **Attack Tools / Techniques:** Hydra, Nmap, SQL Injection, Brute-force, BadUSB simulation  
- **Scripting & Analysis:** Python, Bash  
- **Environment:** Local lab using virtual machines or Docker

---

## Lab Setup
1. **Install and configure SIEM tools**  
   - [Splunk setup instructions](lab-setup/install_splunk.md)  
   - [Wazuh setup instructions](lab-setup/install_wazuh.md)  
   - [Elastic Stack setup instructions](lab-setup/install_elastic.md)

2. **Verify connectivity and log ingestion**  
   Ensure logs from simulated attacks are being received by each SIEM tool.

---

## Attack Simulations
The following attack simulations were performed:

| Attack Type       | Tool/Script              | Notes |
|------------------|-------------------------|-------|
| Brute Force       | `attacks/brute_force.py` | Successful login attempts logged |
| Hydra Password Attack | Hydra                 | Example SSH brute-force |
| SQL Injection     | `attacks/sql_injection_test.md` | Detected in Wazuh/Elastic logs |
| Network Scanning  | Nmap                    | Logs captured in Splunk |
| BadUSB Simulation | Manual/Script           | Simulated in isolated VM |

---

## Detection Rules & Dashboards
- **Splunk:** Custom alerts and dashboards in `dashboards/splunk_dashboard.json`  
- **Wazuh:** Rule configurations in `detections/wazuh_rules.md`  
- **Elastic Stack:** Queries and visualizations for attack detection  

Screenshots or exported dashboards can be found in the `dashboards/screenshots/` folder.

---

## Logs & Analysis
Sample logs collected during attacks are stored in `logs/sample_logs.log`.  
Analysis includes identifying suspicious activity, correlating events, and generating alerts.

---

## Final Report
A comprehensive report of the lab, including methodology, attack results, and detection findings, is available in `reports/SOC_lab_report.md`.

---

## How to Use
1. Clone the repo:  
   ```bash
   git clone https://github.com/your-username/soc-analyst-homelab.git
   cd soc-analyst-homelab
