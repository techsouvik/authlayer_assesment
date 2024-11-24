# Self-Hosted Grafana Monitoring Stack

This repository contains the setup and configuration for deploying a self-hosted monitoring stack using **Grafana**, **Loki**, and **Promtail**. The stack provides log collection, visualization, service status monitoring, and email alerting for application health.

---

## Features
1. **Log Aggregation**: Collect logs using **Promtail** and store them in **Loki**.
2. **Dashboard Visualization**: Visualize logs and system health status using **Grafana**.
3. **Service Monitoring**: Status dashboard with live updates (Green = Up, Red = Down).
4. **Alerting**: Email notifications for service downtime using **Grafana AlertManager**.

---

## Prerequisites
- **Docker** and **Docker Compose** installed on the host machine.
- Open ports: `4000-11000`.
- Access to a Gmail account for sending email alerts via SMTP.

---

## Folder Structure
```plaintext
.
├── docker-compose.yml       # Defines services for Grafana, Loki, and Promtail
├── config/
│   ├── grafana/             # Grafana configuration files
│   ├── loki/                # Loki configuration files
│   └── promtail/            # Promtail configuration files
├── logs/                    # Sample logs for ingestion
├── env.example              # Example environment variables (SMTP settings, etc.)
└── README.md                # Documentation (this file)
```

## Setup Instructions

- Clone the Repository

```env
git clone <repository-url>
cd <repository-name>
```

- Persistent Data Storage

```env
mkdir {grafana,loki,promtail}
```

- Start the Monitoring Stack

```env
docker-compose up -d
```

## Note 

- The Vonage-status-panel has to installed manually,
    - Run the command inside the docker container of grafana
    ```env
        grafana-cli install plugins vonage-status-panel
    ```


## Tasks Completed

- Ingest Logs and Visualize
    - Logs from the logs/ directory are ingested into Loki and displayed in Grafana.
    
- Status Dashboard
    - A status dashboard displays the live status of services:
        - Green: Logs received in the last minute.
        - Red: No logs received in the last minute.

- Email Alerts
    - Alerts are triggered via Grafana AlertManager if any service is marked as "down".