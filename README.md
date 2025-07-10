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
```

---

## 🖼️ Project Walkthrough 

> These screenshots provide a step-by-step visual of the project process.

![cloud-logs-and-user-table](screenshots/cloud-logs-and-user-table.png)  
📌 Preview of `cloud_event_logs` and `users` tables used for alert correlation.

![data-inserts](screenshots/data-inserts.png)  
📌 Sample `INSERT` statements for seeding test events and users.

![full-event-query-output](screenshots/full-event-query-output.png)  
📌 Combined event query showing user, action, and alert severity.

![high-severity-termination](screenshots/high-severity-termination.png)  
📌 Example of a high-severity EC2 termination alert.

![joined-data-view](screenshots/joined-data-view.png)  
📌 JOIN of all three tables with correlated cloud event and user data.

![red-team-user](screenshots/red-team-user.png)  
📌 User attributes for a Red Team engineer responsible for the event.

![initial-ec2-instance-view](screenshots/initial-ec2-instance-view.png)  
📌 AWS EC2 instance deployed for PostgreSQL monitoring.

![security-group-review](screenshots/security-group-review.png)  
📌 Review of security group settings for network access.

![rds-instance-details](screenshots/rds-instance-details.png)  
📌 PostgreSQL RDS instance configuration details.

![postgres-endpoint-connect](screenshots/postgres-endpoint-connect.png)  
📌 Endpoint string used to connect via psql.

![successful-psql-connection](screenshots/successful-psql-connection.png)  
📌 Terminal confirmation of successful PostgreSQL login.

![created-custom-tables](screenshots/created-custom-tables.png)  
📌 Confirmed creation of custom `cloud_event_logs`, `users`, and `alerts` tables.

![cloudwatch-event-policy](screenshots/cloudwatch-event-policy.png)  
📌 Policy used to enable CloudWatch event delivery.

![cloudwatch-trigger-test](screenshots/cloudwatch-trigger-test.png)  
📌 Manual test trigger for CloudWatch rule validation.

![cloudwatch-logs-creation](screenshots/cloudwatch-logs-creation.png)  
📌 Log group creation to store EC2 event activity.

![eventbridge-rule-preview](screenshots/eventbridge-rule-preview.png)  
📌 AWS EventBridge rule setup preview.

![ec2-shutdown-log](screenshots/ec2-shutdown-log.png)  
📌 Example log for EC2 shutdown detection.

![high-severity-alert-generated](screenshots/high-severity-alert-generated.png)  
📌 Alert generated and stored in `alerts` table.

![jumpbox-psql-query-output](screenshots/jumpbox-psql-query-output.png)  
📌 Terminal output from Ubuntu 24.04 Jumpbox querying PostgreSQL.

![second-event-log](screenshots/second-event-log.png)  
📌 Additional log showing second EC2 termination event.

![terraform-rds-provision-success](screenshots/terraform-rds-provision-success.png)  
📌 Terraform deployment output confirming successful RDS provisioning.

![terraform-output-values](screenshots/terraform-output-values.png)  
📌 Terraform output values used for connection string and monitoring setup.

![additional-user-insert](screenshots/additional-user-insert.png)  
📌 Inserted new user into `users` table for correlation testing.

![cloudwatch-dashboard-view](screenshots/cloudwatch-dashboard-view.png)  
📌 CloudWatch dashboard monitoring EC2 state transitions.

![system-query-with-user-attribution](screenshots/system-query-with-user-attribution.png)  
📌 Query results showing user attribution for a system-level event.

![final-query-validation](screenshots/final-query-validation.png)  
📌 Final JOIN validation confirming alert, event, and user linkage.
