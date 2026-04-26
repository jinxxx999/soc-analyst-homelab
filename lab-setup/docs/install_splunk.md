 HEAD
# Splunk Installation Guide (Home Lab)

## Overview
This guide explains how to install Splunk Enterprise on a local machine or virtual machine for the SOC Analyst Home Lab.

---

## 1. Download Splunk Enterprise
Go to the Splunk website and download the free trial:

- Splunk Enterprise (Free 60-day license)
- Linux, macOS, or Windows version depending on your OS

Link: https://www.splunk.com/en_us/download/splunk-enterprise.html

---

## 2. Install Splunk (Linux Example)

### Update system
```bash
sudo apt update && sudo apt upgrade -y

## Splunk Installation and Setup (macOS)

1. **Download Splunk**  
   - Go to https://www.splunk.com/en_us/download/splunk-enterprise.html  
   - Choose macOS `.dmg` version

2. **Install Splunk**  
   - Open the `.dmg` file and drag Splunk to `/Applications`  
   - Open Terminal and run:
     ```bash
     cd /Applications/Splunk/bin
     ./splunk start --accept-license
     ```
   - Create admin username and password

3. **Add Data Input**  
   - Go to Splunk Web: http://localhost:8000 → Login  
   - Settings → Add Data → Monitor → Files & Directories  
   - Source: `/var/log/system.log`  
   - Sourcetype: `mac_system_log`  
   - Host: `MacBook-Air-Yelizaveta.local`  
   - Index: `main`  
   - Submit → Splunk now indexes your macOS system logs

4. **Verify Logs**  
   - Search:
     ```spl
     index=main sourcetype="mac_system_log" | head 20
     ```
   - Logs should appear, confirming Splunk is running successfully
 a4c614a6aa2b72f3a8cf7b65293bea62a5f66a60
