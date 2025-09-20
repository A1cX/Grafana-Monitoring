# Grafana-Monitoring

This repository contains a basic Grafana and Prometheus monitoring setup for personal use.

## Files

- `node_exporter_dashboard.json` – Exported Grafana dashboard for Node Exporter metrics.
- `prometheus.yml` – Prometheus configuration file for local scraping.

## Setup Instructions

1. **Install Prometheus** and Grafana on your machine.
2. **Move the files** into a project folder, e.g., `Grafana-Monitoring`.
3. **Start Prometheus**:
   ```bash
   prometheus --config.file=prometheus.yml

