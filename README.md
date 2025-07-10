# ☁️ Cloud Security PostgreSQL Lab

This project simulates a real-world SOC Analyst workflow by correlating cloud security events from AWS EC2 with user data and generating actionable security alerts using PostgreSQL. The goal is to demonstrate cloud event visibility, log ingestion, and query-based investigation in a structured lab environment.

---

## 📚 Use Cases

✅ Correlate EC2 actions with user roles and severity levels  
✅ Detect termination or shutdown events from unknown sources  
✅ Simulate SOC workflows with JOIN queries and attribution  

---

## 🧱 Repository Contents

| File              | Description                                                  |
|-------------------|--------------------------------------------------------------|
| `schema.sql`      | SQL for creating `cloud_event_logs`, `users`, and `alerts` tables |
| `seed_data.sql`   | Insert statements for sample cloud events and alerts         |
| `queries.sql`     | JOIN queries to investigate cloud behavior and alert severity |
| `screenshots/`    | Visual walkthrough of key setup, data modeling, and output   |

---

## 🛠️ Technologies Used

- **AWS EC2** (Cloud events source)  
- **CloudWatch + EventBridge** (Log automation and rule generation)  
- **PostgreSQL (AWS RDS)** (Relational database for alert correlation)  
- **Ubuntu 24.04 VM (Jumpbox)** (Querying interface via psql)  
- **Terraform** (Infrastructure as Code for provisioning)

---

## 🧪 Sample Query Output

```sql
SELECT u.username, e.event_type, a.severity
FROM users u
JOIN cloud_event_logs e ON u.user_id = e.user_id
JOIN alerts a ON e.event_id = a.event_id
WHERE a.severity = 'High';

