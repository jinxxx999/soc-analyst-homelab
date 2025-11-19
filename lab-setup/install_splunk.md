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
