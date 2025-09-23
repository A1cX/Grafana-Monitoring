
# Grafana-Monitoring

This repository provides a basic system monitoring setup for macOS using **Node Exporter**, **Prometheus**, and **Grafana**.  
The setup enables the collection, storage, and visualization of system metrics including CPU, memory, disk, and network usage.

---
## System Architecture
The monitoring setup follows a three-tier architecture:

1. **Node Exporter**: Collects metrics from the host system and exposes them on port `9100`.  
2. **Prometheus**: Scrapes the metrics from Node Exporter at regular intervals and stores them.  
3. **Grafana**: Connects to Prometheus to display metrics using dashboards.

---

## Repository Contents

- `node_exporter_dashboard.json` – Preconfigured Grafana dashboard for Node Exporter metrics.  
- `prometheus.yml` – Prometheus configuration file specifying the scrape targets and intervals.

---

## Setup Instructions

### 1. Install Dependencies

I installed Prometheus and Grafana via Homebrew:

```bash
brew install prometheus grafana
This ensures the required software components are available on the system.

---

2. Downloaded and Run Node Exporter

Downloaded the appropriate Node Exporter version for the system architecture (Apple Silicon arm64) from the Node Exporter releases

Extract and run Node Exporter:
tar -xzf node_exporter-1.9.1.darwin-amd64.tar.gz
cd node_exporter-1.9.1.darwin-amd64
./node_exporter

Verified that Node Exporter is running:
curl http://localhost:9100/metrics | head -n 10

3. Configured and Started Prometheus

Added the provided prometheus.yml to the project directory and started Prometheus:
prometheus --config.file=prometheus.yml
Access Prometheus via: http://localhost:9090

Prometheus scrapes metrics from Node Exporter according to the configuration.
4. Start Grafana
brew services start grafana
Access Grafana via: http://localhost:3000

Default credentials: admin/admin

5. Imported the Dashboard

Navigated to Dashboards → Import in Grafana.

Uploaded node_exporter_dashboard.json.

Set the Data Source to the Prometheus instance.

Applied changes to visualize system metrics.

Note: the dashboard initially showed no data, even after restart to allow Prometheus to scrape metrics.
Manually correcetd the .json file to match the configuration of my Dashboard and linked them, restarted Prometehus and it worked.

6. Verification

Node Exporter metrics endpoint: http://localhost:9100/metrics

Prometheus scrape targets: http://localhost:9090/targets

Grafana dashboard displays metrics from Prometheus after data is collected.

7. Version Control

To track the project with Git i used:

git init
git add .
git commit -m "Initial Grafana monitoring setup"
git remote add origin https://github.com/YourUsername/Grafana-Monitoring.git
git branch -M main
git push -u origin main

Notes

Ensured the Node Exporter version matches the macOS architecture.

Dashboards included variables (job, node, instance) that needed manual correction/selection for metrics display.

Prometheus must successfully scrape Node Exporter in order for Grafana to display data and manaual checks and restart was needed.

This personal setup provides a functional monitoring stack that allows visualization of system metrics in a Grafana dashboard on macOS.
More metrics to be added soon, probably also visualisation.

