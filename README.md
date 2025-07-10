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

## 📸 Project Walkthrough

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
📌 Reviewing EC2 security group configurations.

![rds-instance-details](screenshots/rds-instance-details.png)  
📌 Amazon RDS PostgreSQL instance details.

![postgres-endpoint-connect](screenshots/postgres-endpoint-connect.png)  
📌 Copying RDS endpoint to connect via psql CLI.

![successful-psql-connection](screenshots/successful-psql-connection.png)  
📌 Successful PostgreSQL login from jumpbox terminal.

![created-custom-tables](screenshots/created-custom-tables.png)  
📌 Tables `users`, `alerts`, and `cloud_event_logs` successfully created.

![cloudwatch-event-policy](screenshots/cloudwatch-event-policy.png)  
📌 IAM policy to allow logging EC2 events to CloudWatch.

![cloudwatch-trigger-test](screenshots/cloudwatch-trigger-test.png)  
📌 Triggering an EC2 shutdown to test logging pipeline.

![cloudwatch-logs-creation](screenshots/cloudwatch-logs-creation.png)  
📌 New CloudWatch log group confirming event capture.

![eventbridge-rule-preview](screenshots/eventbridge-rule-preview.png)  
📌 AWS EventBridge rule set up to forward EC2 stop/terminate events.

![ec2-shutdown-log](screenshots/ec2-shutdown-log.png)  
📌 Log event of EC2 shutdown action written to CloudWatch.

![high-severity-alert-generated](screenshots/high-severity-alert-generated.png)  
📌 PostgreSQL alert raised due to severity + user role mapping.

![jumpbox-psql-query-output](screenshots/jumpbox-psql-query-output.png)  
📌 Query executed from hardened Linux jumpbox to validate logs.

![second-event-log](screenshots/second-event-log.png)  
📌 Inserted second test event to validate alert logic.

![terraform-rds-provision-success](screenshots/terraform-rds-provision-success.png)  
📌 Terraform successfully deployed PostgreSQL RDS instance.

![terraform-output-values](screenshots/terraform-output-values.png)  
📌 Output from `terraform apply` showing connection info and resources.

![additional-user-insert](screenshots/additional-user-insert.png)  
📌 Adding a second Red Team user to test attribution mapping.

![cloudwatch-dashboard-view](screenshots/cloudwatch-dashboard-view.png)  
📌 Confirming EC2 events visually through CloudWatch dashboards.

![system-query-with-user-attribution](screenshots/system-query-with-user-attribution.png)  
📌 Final JOIN query showing linked user identity, action, and alert.

![final-query-validation](screenshots/final-query-validation.png)  
📌 Query output confirms all relationships and alert triggers function correctly.

