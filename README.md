# Homelab Observer: Professional Monitoring & Observability Stack

## 👁️ Overview
Homelab Observer is a containerized monitoring solution optimized for ARM64 architectures. It implements a robust observability pipeline to track system health, resource utilization, and network performance across a distributed home lab environment.

This project follows the **Infrastructure as Code (IaC)** philosophy, ensuring that the entire monitoring environment is reproducible, secure, and decoupled from the host hardware.

##  Architectural Decisions
* **Data Persistence:** To ensure high availability and prevent SD card failure, all Prometheus TSDB data and Grafana databases are mapped to external high-speed storage (SSD).
* **Security First:** No sensitive information, IP addresses, or credentials are hardcoded. The stack uses environment variables and standardized ports.
* **Resource Management:** Prometheus retention is tuned to 15 days to optimize disk I/O and storage efficiency on edge devices.

## Tech Stack
* **Prometheus:** Time-series database for multi-node metrics collection.
* **Grafana:** Centralized visualization and analytics platform.
* **Node Exporter:** Hardware telemetry exporter for Linux kernels.
* **Docker Compose:** Orchestration layer for service lifecycle management.

##  Deployment

### 1. Prerequisites
* Docker and Docker Compose (v2.0+) installed.
* Linux-based host (Optimized for Ubuntu Server 24.04 LTS).
* Dedicated storage mount point for data persistence.

### 2. Configuration & Permissions
Before launching, ensure the directory ownership matches the internal container UIDs to prevent permission errors:

```bash
# Set ownership for Prometheus (UID 65534) and Grafana (UID 472)
sudo chown -R 65534:65534 ./prometheus/data
sudo chown -R 472:472 ./grafana/data
```

### 3. Launching the Stack
```bash
docker compose up -d
```

##  Access Points
Once deployed, the services are available at:
* **Grafana Dashboard:** `http://<HOST_IP>:3000`
* **Prometheus UI:** `http://<HOST_IP>:9090`
* **Metrics Stream:** `http://<HOST_IP>:9100/metrics`

*Note: Replace `<HOST_IP>` with your node's actual management IP.*

## 📅 Roadmap
- [x] Persistent storage implementation on external SSD.
- [x] ARM64 performance optimization.
- [ ] SNMP integration for Network Infrastructure monitoring.
- [ ] Centralized Log Management with Grafana Loki.
- [ ] Automated Alerting Pipeline (Discord/Webhook).

---