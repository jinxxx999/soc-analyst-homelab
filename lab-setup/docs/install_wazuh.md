# Wazuh SIEM Lab Installation Guide

## Overview
This repository contains the deployment configuration for the Wazuh Manager, the central brain of the SOC laboratory. It orchestrates security monitoring, log analysis, and vulnerability detection across the infrastructure.

## Architecture
- **Wazuh Manager** (v4.14.1): Security management and log analysis
- **Wazuh Indexer** (v4.14.1): Data storage and search (OpenSearch-based)
- **Wazuh Dashboard** (v4.14.1): Web interface for visualization

## Prerequisites
- Docker & Docker Compose
- System Memory: 6GB+ RAM (total for the full stack)
- Ports 1514 (Agent logs), 1515 (Registration), 55000 (API)

---

## Installation Steps

###  Clone or create project structure
```bash
mkdir -p wazuh-lab/config
cd wazuh-lab
```

###  Create docker-compose.yml
[Content of your docker-compose.yml]

###  Create dashboard configuration
Create `config/opensearch_dashboards.yml`:
```yaml
server.host: "0.0.0.0"
server.port: 5601
opensearch.hosts: ["https://wazuh-indexer:9200"]
opensearch.ssl.verificationMode: none
opensearch.username: "admin"
opensearch.password: "SecretPassword"
opensearch.requestHeadersWhitelist: ["securitytenant","Authorization"]
opensearch_security.multitenancy.enabled: false
uiSettings.overrides.defaultRoute: /app/wazuh
```

###  Start services
```bash
docker-compose up -d
```

### Verify all containers are running
```bash
docker ps
```

### Access Dashboard
- URL: http://localhost:5601
- Username: `admin`
- Password: `SecretPassword`

## Troubleshooting

### Dashboard shows "not ready yet"
Wait 2-3 minutes for services to fully initialize.

### SSL certificate errors
Set `opensearch.ssl.verificationMode: none` in config file.

### Check logs
```bash
docker logs wazuh-dashboard
docker logs wazuh-manager
docker logs wazuh-indexer
```

## What I Learned
- Docker container orchestration
- SIEM architecture and components
- SSL/TLS configuration
- Troubleshooting containerized applications
- Volume management in Docker

## Next Steps
- [ ] Add Wazuh agents to monitor endpoints
- [ ] Configure custom detection rules
- [ ] Set up log forwarding from other systems
- [ ] Practice incident response scenarios
