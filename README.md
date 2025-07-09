# cloud-security-postgres-lab
A PostgreSQL lab simulating real-time cloud security events and alert correlation using AWS EC2 event data.
# Cloud Security PostgreSQL Lab

This lab simulates a cloud security environment by modeling AWS EC2 events and security alerting using PostgreSQL. It's designed to demonstrate how a SOC Analyst or Cloud Security Engineer can correlate user activity, event severity, and alert resolution from log data.

---

## 🏗️ Project Structure

- **cloud_event_logs** – Stores raw cloud event details (e.g. EC2 stop/terminate).
- **users** – Maps user identities to their roles and teams.
- **alerts** – Tracks security alerts linked to specific events.

---

## 🧪 Key Use Cases

- Correlate EC2 actions to user roles and severity levels.
- Generate structured security alerts.
- Run JOIN queries to support SOC investigations.

---

## 📄 Files

| File | Description |
|------|-------------|
| `schema.sql` | Table creation for `cloud_event_logs`, `users`, and `alerts` |
| `seed_data.sql` | Insert statements for sample events and alerts |
| `queries.sql` | JOIN queries to retrieve meaningful threat insights |
| `screenshots/` | Visual documentation of terminal output |

---

## 📷 Example Output

```sql
SELECT
  c.event_id, c.event_time, c.action_taken, c.severity_level,
  u.full_name, u.team
FROM cloud_event_logs c
JOIN users u ON c.user_identity = u.user_identity;
