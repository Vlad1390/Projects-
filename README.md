# Investigating with ELK

## Overview
This project demonstrates how to use the ELK (Elasticsearch, Logstash, and Kibana) stack for cybersecurity investigations. The goal is to collect, analyze, and visualize security-related logs to identify potential threats.

## Prerequisites
- Docker and Docker Compose (recommended for quick setup)
- ELK Stack (Elasticsearch, Logstash, Kibana)
- Sample log data (Sysmon, Windows Event Logs, or any security-related logs)

## Setup Instructions

### 1. Clone the Repository
```bash
git clone https://github.com/your-username/Investigating-with-ELK.git
cd Investigating-with-ELK
```

### 2. Start ELK Stack Using Docker
```bash
docker-compose up -d
```

### 3. Verify Services
- **Elasticsearch**: http://localhost:9200
- **Kibana**: http://localhost:5601

### 4. Import Logs
Use Logstash to ingest log data:
```bash
docker exec -it logstash bin/logstash -f /etc/logstash/conf.d/logstash.conf
```

## Investigation Scenarios
1. **Suspicious Login Attempts** – Analyze authentication logs for brute-force attacks.
2. **Malware Execution** – Monitor Sysmon logs for suspicious process creation.
3. **Data Exfiltration** – Detect unusual outbound traffic patterns.

## Visualization
- **Dashboards in Kibana**: Create visualizations to identify trends and anomalies.
- **SIEM Integration**: Use Elastic Security features for threat detection.

### Example Kibana Dashboard
![Kibana Dashboard](images/kibana-dashboard.png)

## Contributing
Feel free to submit issues or pull requests to improve this project.
