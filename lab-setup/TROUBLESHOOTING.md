Troubleshooting: Wazuh Dashboard Connection & Auth Failures
This document outlines the debugging process for a critical connectivity issue encountered during a Wazuh deployment in a Docker environment.

1. The Issue: "Application Not Found"
When accessing the Wazuh Dashboard via browser, the interface returned an "Application Not Found" error or failed to connect to the Wazuh Manager, despite all containers showing a status of Up.

2. Root Cause Analysis
The investigation revealed a synchronization failure between the Wazuh Dashboard, Wazuh Manager, and Wazuh Indexer.

Authentication Method: Modern Wazuh (v4.3+) uses RBAC (Role-Based Access Control) integrated with OpenSearch (Indexer).

Credential Mismatch: The default admin:admin credentials were deprecated. While a custom SecretPassword was identified in the opensearch_dashboards.yml configuration, the Wazuh Manager API was not updated to recognize this password, resulting in 401 Unauthorized errors.

3. Debugging Steps Taken
Step 1: Direct API Validation

To bypass the Dashboard UI and test the Manager directly, I executed a curl command from within the manager container:

Bash
docker exec -it wazuh-manager curl -u admin:SecretPassword -k -X GET "https://localhost:55000/manager/info?pretty=true"
Result: {"title": "Unauthorized", "detail": "No authorization token provided"}. This confirmed the issue was strictly related to API authentication, not network routing.

Step 2: Configuration Inspection

I performed a recursive search to locate where the deployment script stored sensitive strings:

Bash
grep -r "password" .
This revealed that while the Indexer was configured with a custom password, the Manager environment variables in the docker-compose.yml were missing or mismatched.

Step 3: Manual Auth Override Attempt

Attempted to force a password update using the Wazuh internal identity binary:

Bash
docker exec -it wazuh-manager /var/ossec/bin/wazuh-authd -P [PRIVATE_PASSWORD]
4. Key Lessons & Final Resolution
The "Frankenstein" nature of the docker-compose file (mixing different configuration sources) led to a broken chain of trust between services.

Final Fix Strategy:

Total Cleanup: Perform a docker-compose down -v to wipe corrupted volumes and old credential caches.

Official Baseline: Re-deploy using the official wazuh-docker repository.

Unified Identity: Utilize the generate-certs.yml tool to ensure all components share a consistent security manifest and a single source of truth for passwords (wazuh-passwords.txt).

Technical Stack Used
Orchestration: Docker / Docker-compose

Security: RBAC, OpenSearch Security Plugin

Diagnostics: Bash, cURL, Linux Filesystem Inspection (grep/find)
