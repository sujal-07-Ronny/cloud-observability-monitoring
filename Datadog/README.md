
# Datadog – AWS EC2 Monitoring

## Overview

This module covers setting up **Datadog** to monitor an AWS EC2 instance in real time. It includes agent-based infrastructure metric collection, a custom dashboard, a threshold-based metric monitor, and email alert notifications — implemented end-to-end on a live EC2 instance running in the **ap-south-1 (Mumbai)** region.

---

## Tools Used

- Datadog (Infrastructure Monitoring, Dashboards, Monitors)
- AWS EC2 (t2.small instance)
- Datadog Agent

---

## Project Components

### 1. EC2 Instance Setup
*(`Screenshots/ec2-instance.png`)*

Launched an AWS EC2 `t2.small` instance named **datadog-monitoring** in the Mumbai (`ap-south-1`) region and installed the Datadog Agent on it to begin streaming host-level telemetry to Datadog.

### 2. Infrastructure Dashboard
*(`Screenshots/Dashboard.png`)*

Built a custom dashboard ("Sujal's Dashboard") displaying live, real-time widgets for the monitored EC2 host:
- **EC2 CPU Usage (%)**
- **EC2 Memory Usage**
- **EC2 Disk Usage**
- **EC2 Network Traffic**

This gives a single-pane view of the instance's health over a rolling time window (e.g., past 1 hour).

### 3. Metric Monitor / Alert
*(`Screenshots/Alert-Graph.png`)*

Created a metric monitor named **"EC2 CPU High – Test Alert"** using the query:

```
avg(last_5m):avg:system.cpu.user{host:i-03d36c60beefc920b} > 1
```

The monitor evaluates the average CPU utilization over the last 5 minutes and transitions to an **Alert** state when usage crosses the 1% test threshold, demonstrating how threshold-based alerting is configured in Datadog.

### 4. Email Notification
*(`Screenshots/email-notification.png`)*

Configured the monitor to send notifications on trigger. When the alert fired, Datadog automatically sent an email — *"Triggered: EC2 CPU High - Test Alert"* — containing the affected host ID and alert message, confirming the full notification pipeline works end-to-end.

---

## Workflow

```
EC2 Instance Launched
        │
Datadog Agent Installed
        │
Metrics Sent to Datadog (CPU, Memory, Disk, Network)
        │
Custom Dashboard Built
        │
Metric Monitor Configured (Threshold-Based)
        │
Alert Triggered ──► Email Notification Sent
```

---

## Key Learnings

- Installing and configuring the Datadog Agent on an AWS EC2 instance
- Collecting and visualizing host-level infrastructure metrics
- Building custom, real-time monitoring dashboards
- Writing Datadog monitor queries and setting alert thresholds
- Configuring and validating email-based alert notifications
