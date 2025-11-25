# Wazuh SIEM Lab Installation Guide

## Overview
Docker-based Wazuh SIEM environment for threat detection and security monitoring practice.

## Components
- **Wazuh Manager** (v4.14.1): Security management and log analysis
- **Wazuh Indexer** (v4.14.1): Data storage and search (OpenSearch-based)
- **Wazuh Dashboard** (v4.14.1): Web interface for visualization

## Prerequisites
- Docker installed
- Docker Compose installed
- 4GB+ RAM available
- Ports 1514, 1515, 5601, 9200, 55000 available

## Installation Steps

### 1. Clone or create project structure
```bash
mkdir -p wazuh-lab/config
cd wazuh-lab
```

### 2. Create docker-compose.yml
[Content of your docker-compose.yml]

### 3. Create dashboard configuration
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

### 4. Start services
```bash
docker-compose up -d
```

### 5. Verify all containers are running
```bash
docker ps
```

### 6. Access Dashboard
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
