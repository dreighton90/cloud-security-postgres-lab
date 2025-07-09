# cloud-security-postgres-lab

A hands-on PostgreSQL lab simulating real-time cloud event monitoring and alert correlation using AWS EC2 logs. Built to demonstrate how a SOC Analyst or Cloud Security Engineer can use log data to track user behavior, detect critical events, and run investigations using SQL.

---

## 🧱 Project Overview

This lab models a simplified cloud security environment with three core PostgreSQL tables:

- `cloud_event_logs` – Raw cloud event data (e.g., EC2 stop/terminate)
- `users` – Maps user identities to teams and roles
- `alerts` – Tracks high-severity or unauthorized activity for investigation

---

## 🎯 Use Cases

- Correlate EC2 actions with user roles and severity levels  
- Detect termination or shutdown events from unknown sources  
- Simulate SOC workflows with JOIN queries and attribution  

---

## 🗂️ Repository Contents

| File | Description |
|------|-------------|
| `schema.sql` | SQL for creating all three tables |
| `seed_data.sql` | Sample insert statements for cloud events, users, and alerts |
| `queries.sql` | JOIN queries used to investigate behavior and correlate alerts |
| `screenshots/` | Visual walkthrough of key steps and outputs |

---

## 🖥️ Technologies Used

- AWS EC2 + CloudWatch + EventBridge
- PostgreSQL (RDS)
- Ubuntu 24.04 (jumpbox VM)
- Terraform (for infrastructure provisioning)

---

## 📸 Project Walkthrough (Selected Screenshots)

> See the `screenshots/` folder for a chronological walkthrough of the full lab setup, from provisioning to final query validation.

Example query output (alert correlation):

```sql
SELECT a.alert_id, a.severity, u.username, c.event_type, c.timestamp
FROM alerts a
JOIN cloud_event_logs c ON a.event_id = c.event_id
JOIN users u ON c.user_id = u.user_id
WHERE a.severity = 'high';
