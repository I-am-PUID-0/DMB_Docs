---
title: pgAdmin 4
---

# pgAdmin 4

pgAdmin 4 is a web-based administration tool for managing PostgreSQL databases. DMB includes pgAdmin pre-installed and configured to work out of the box, allowing you to inspect, query, and back up your databases directly from a browser.

---

## ⚙️ Configuration Settings in `dmb_config.json`
```json
"pgadmin": {
    "enabled": true,
    "process_name": "pgAdmin4",
    "config_dir": "/pgadmin/data",
    "config_file": "/pgadmin/data/config_local.py",
    "log_file": "/pgadmin/data/pgadmin4.log",
    "port": 5050,
    "default_server": "0.0.0.0",
    "setup_email": "DMB@DMB.DMB",
    "setup_password": "postgres",
    "command": []
},
```    

### 🔍 Configuration Key Descriptions
- **`enabled`**: Whether to start the pgAdmin service.
- **`process_name`**: The label used in logs and process tracking.
- **`config_dir`** – Directory where pgAdmin configuration files are stored.
- **`config_file`** – Path to the primary pgAdmin configuration file.
- **`port`**: Port exposed for the pgAdmin.
- **`default_server`**: IP address pgAdmin should bind to. 

    !!! note "`0.0.0.0` allows access to pgAdmin from all addresses"

- **`setup_email`**: The email address to be used with pgAdmin.
- **`setup_password`**: The password to be used with pgAdmin. 
- **`command`** – The command used to start pgAdmin.

## 🚪 Accessing pgAdmin
- Navigate to: `http://<host>:<port>` 
    - default port `5055`
- Login using the credentials set via environment variables:
  - `PGADMIN_SETUP_EMAIL` 
    - default: `DMB@DMB.DMB`
  - `PGADMIN_SETUP_PASSWORD` 
    - default: `postgres`

!!! tip "The email is used as the username. It does not need to be a real email address."

![Login Screen](../assets/images/pgadmin/pgadmin-login.png)

---

## 🔐 Server Configuration
- pgAdmin is preconfigured with a server connection named **DMB**.
- On first login, you must enter the password for the PostgreSQL server connection.
  - Default password: `postgres`
  - Or, use the value of `POSTGRES_PASSWORD` if set in your environment.

![Server View](../assets/images/pgadmin/pgadmin-server-view.png)

---

## ⚙️ Extensions
The following PostgreSQL extensions are included in the DMB image:

### 📈 `system_stats`
Provides system performance statistics inside PostgreSQL.
- Find it in the pgAdmin dashboard under the connected database (e.g., `pgadmin` or `riven`).

![System Stats](../assets/images/pgadmin/pgadmin-system-stats.png)

### 📅 `pgAgent`
A job scheduler for PostgreSQL. Useful for:
- Scheduling backups
- Routine maintenance

![pgAgent Jobs](../assets/images/pgadmin/pgadmin-pgagent-jobs.png)

---

## 💾 Example: Scheduled Backups with pgAgent

1. Navigate to `pgAgent Jobs` under your connected DMB server.
2. Right-click → `Create → pgAgent Job`

    ![Create Job](../assets/images/pgadmin/pgadmin-create-job.png)

3. Enter the job name and any comments you like:

    ![Add Job](../assets/images/pgadmin/pgadmin-add-job.png)

4. In the **Steps** tab, click the `+` button to **Add row** to the steps:

    ![Add Step](../assets/images/pgadmin/pgadmin-add-step.png)

5. Click the `pencil` icon to edit the new row and configure the step:

    ![Edit Step](../assets/images/pgadmin/pgadmin-edit-step.png)

6. Enter a step name and select `Kind` = `Batch`:

    ![Step Details](../assets/images/pgadmin/pgadmin-step-details.png)

7. Add backup commands to the **Code** tab:

    !!! note "The following code is an example of a backup command. You may need to modify it to suit your needs."

    ```sql
    pg_dump --username=DMB --dbname=riven --clean --file=/pgadmin/data/riven_backup-`date +%Y-%m-%d-%H-%M-%S`.sql
    pg_dump --username=DMB --dbname=zilean --clean --file=/pgadmin/data/zilean_backup-`date +%Y-%m-%d-%H-%M-%S`.sql
    ```

    ![Step Code](../assets/images/pgadmin/pgadmin-backup-step-code.png)

8. Click on the **Schedules** tab to set the schedule for the backup.

9. As before with the **Steps**, add a row to add a new schedule, and edit the row to configure the schedule.

10. Enter the schedule name, select the **Enabled?** toggle, and set the Start and End dates for the schedule.

    ![Add Schedule](../assets/images/pgadmin/pgadmin-schedule-add.png)

11. On the **Repeat** tab, set the repeat frequency (e.g., daily at 12:00 AM):

    ![Repeat Tab](../assets/images/pgadmin/pgadmin-schedule-repeat.png)

12. Click **Save** to save the scheduled backup job.

!!! tip "Backups are stored in `/pgadmin/data`."

---

## 📚 More Info
- [pgAdmin Docs](https://www.pgadmin.org/docs/pgadmin4/latest/index.html)
- [pgAgent Job Scheduler](https://www.pgadmin.org/docs/pgadmin4/development/pgagent_jobs.html)

---

## 🧠 Summary
| Setting                | Value                |
|------------------------|----------------------|
| UI Address             | `http://<host>:5050` |
| Default Email/Username| `DMB@DMB.DMB`         |
| Default Password       | `postgres`           |
| Data Directory         | `/pgadmin/data`      |
| Config File            | `/pgadmin/data/config_local.py` |
