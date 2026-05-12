# Troubleshooting Guide: Wazuh Connection & Auth Failures

This document details the debugging process for critical connectivity and synchronization issues encountered during the SOC Home Lab deployment.

## 1. The "Application Not Found" & Connectivity Issue
**Issue:** The Wazuh Dashboard returned "Application Not Found" or connection timeouts, even though Docker containers were reported as `Up`.

**Root Cause:** Synchronization failure between the Dashboard, Manager and Indexer caused by mismatched API credentials and resource constraints.

**Diagnostic Steps:**
* **Direct API Validation:** I bypassed the UI to test the Manager API directly from within the container:
  ```bash
  docker exec -it wazuh-manager curl -u admin:YourPassword -k -X GET "https://localhost:55000/manager/info?pretty=true"

* **Log Inspection:** Identified 401 Unauthorized errors, confirming the issue was authentication-based, not network-based.

* **Credential Discovery:** Used `grep -r "password" .`to locate mismatched strings across the configuration files.
  
## 2. Authentication & Password Mismatches
**Issue:** Standard credentials (`admin:admin`) failed, and custom passwords defined in configuration files were not being accepted.

**Resolution:**

* **Security Admin Script**: Manually forced the Indexer to apply security configurations to the cluster:
```bash
bash /usr/share/wazuh-indexer/plugins/opensearch-security/tools/securityadmin.sh -cd /usr/share/wazuh-indexer/plugins/opensearch-security/securityconfig/ -icl -nhnv -cacert /usr/share/wazuh-indexer/config/certs/root-ca.pem -cert /usr/share/wazuh-indexer/config/certs/admin.pem -key /usr/share/wazuh-indexer/config/certs/admin-key.pem -h localhost
```
* **Unified Identity:** Implemented a single source of truth for passwords to ensure all components share a consistent security manifest.


## 3. Resource & Environment Fixes
**Issue:** Containers crashing or hanging during the initialization sequence.

**Resolution:**
* **Memory Limits:** Increased Docker RAM allocation to **6GB** to support the resource-heavy Indexer and Dashboard stack.
* **Kernel Parameters:** Adjusted the host machine's memory map limits to prevent Elasticsearch crashes:
  ```bash
  sysctl -w vm.max_map_count=262144
  ```
* **Total Cleanup:** When configuration "Frankensteining" occurred, I used `docker-compose down -v` to wipe corrupted volumes and ensure a clean state for re-deployment.
  
### Lessons Learned
**Trust but Verify:** Always test backend APIs via `curl` before troubleshooting the frontend UI.

**Infrastructure as Code:** Maintaining a clean `docker-compose.yml` and unified `.env` variables is more efficient than fixing a running stack.

**Documentation is Key:** Keeping track of manual overrides (like securityadmin.sh) is essential for long-term lab stability.

### Technical Stack Used
**Orchestration:** Docker / Docker-compose

**Security:** RBAC, OpenSearch Security Plugin

**Diagnostics:** Bash, cURL, Linux Filesystem Inspection (grep/find)
