# Splunk Installation Guide (Home Lab)

## Overview
Standalone Splunk Enterprise deployment for log aggregation and security analysis comparison.
## Components
Splunk Enterprise (Latest): All-in-one indexer, search head, and forwarder management (Free 60-day license)
## Prerequisites
Docker & Docker Compose installed

4GB+ RAM (Splunk is memory-hungry)

Ports: 8000 (Web UI), 8089 (Management), 9997 (Indexing)

---

## Installation Steps
### Project Directory

``` Bash 
mkdir -p splunk-lab
cd splunk-lab
```
### Deployment Command

Run the container with accepted license and admin password:

```Bash
docker-compose up -d splunk
```
### Verify Container Status

```Bash
docker ps | grep splunk
```
### Access Web Interface

URL: http://localhost:8000

Username: admin

Password: [YourSecretPassword]
## Troubleshooting
High CPU/RAM usage

Splunk can be slow on startup. Give it 3-5 minutes to initialize the web interface.

Data not appearing

Ensure the HEC (HTTP Event Collector) or Receiver (Port 9997) is manually enabled in the Settings > Data Inputs menu.

## What I Learned
Splunk licensing and basic setup

Difference between Splunk and OpenSearch-based Indexers

Managing heavy containers in Docker

## Next Steps
[ ] Install Splunk Universal Forwarder on a test machine

[ ] Create a basic dashboard for failed login attempts

[ ] Integrate Wazuh alerts via API/Syslog
