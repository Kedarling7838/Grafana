# AWS EC2 Monitoring with Prometheus and Grafana

## Project Overview

This project demonstrates how to monitor an AWS EC2 Ubuntu instance using Prometheus and Grafana. Prometheus collects system metrics, while Grafana visualizes those metrics through interactive dashboards. The Stress tool is used to generate CPU load for testing and monitoring purposes.

## Architecture

```text
+-------------------------+
|      AWS EC2 (Ubuntu)   |
|                         |
|   Stress Tool           |
|         |               |
|         v               |
|   Prometheus            |
| (Metrics Collection)    |
+-----------+-------------+
            |
            | Query Metrics
            v
+-------------------------+
|        Grafana          |
| Dashboards & Charts     |
+-----------+-------------+
            |
            v
         End User
```

## Technologies Used

* AWS EC2
* Ubuntu Linux
* Prometheus
* Grafana
* Stress Tool
* Linux Systemd Services

## Prerequisites

* AWS Account
* EC2 Ubuntu Instance
* Security Group allowing:

  * Port 22 (SSH)
  * Port 3000 (Grafana)
  * Port 9090 (Prometheus)

## Installation Steps

### Update Packages

```bash
sudo apt update
```

### Install Prometheus

```bash
sudo apt-get install prometheus
sudo systemctl enable prometheus
sudo systemctl start prometheus
```

### Verify Prometheus

```bash
sudo systemctl status prometheus
```

Access:

```text
http://52.90.238.227:9090
```

### Install Grafana

```bash
sudo apt install grafana -y
sudo systemctl enable grafana-server
sudo systemctl start grafana-server
```

### Verify Grafana

```bash
sudo systemctl status grafana-server
```

Access:

```text
(http://52.90.238.227:3000)
```

Default Login:

Username: admin

Password: admin

## Configure Prometheus Data Source

1. Login to Grafana.
2. Navigate to Connections → Data Sources.
3. Select Prometheus.
4. URL:

```text
(http://52.90.238.227:3000)
```

5. Click Save & Test.

## Generate CPU Load

Install Stress:

```bash
sudo apt install -y stress
```

Run Stress Test:

```bash
stress --cpu $(nproc) --timeout 60s
```

## Prometheus Query

Use the following query to monitor CPU utilization:

```promql
100 - (avg by (instance) (irate(node_cpu_seconds_total{mode="idle", instance="localhost:9100"}[10m])) * 100)
```

## Results

* Real-time CPU monitoring
* Interactive Grafana dashboards
* System performance visualization
* Stress testing validation

## Screenshots

Add screenshots of:

1. EC2 Instance
2. Prometheus Dashboard
3. Grafana Dashboard
4. CPU Load Monitoring
5. Stress Test Execution

## Future Enhancements

* Memory Monitoring
* Disk Monitoring
* Alert Configuration
* Email Notifications
* Multi-Server Monitoring

## Author

Kedarling Ashok Kanade

MCA Student

GM University, Davangere
