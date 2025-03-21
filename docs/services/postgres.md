---
title: PostgreSQL
---

# PostgreSQL

PostgreSQL is the core database system used by DMB to store metadata and internal configuration for services like Riven, Zilean, and pgAdmin. It is pre-installed and automatically initialized during container startup.

---

## 🚪 Access & Credentials
- Default Port: `5432`
- Default User: `DMB`
- Default Password: `postgres`
- Default Databases:
  - `postgres`
  - `pgadmin`
  - `zilean`
  - `riven`

> 🔐 Override any of the above using `POSTGRES_USER`, `POSTGRES_PASSWORD`, or `POSTGRES_DB` environment variables.

---

## 📁 Data & Config Paths
| Purpose              | Path                      |
|----------------------|---------------------------|
| Data Directory       | `/postgres_data`          |
| Config File          | `/postgres_data/postgresql.conf` |
| Runtime Directory    | `/run/postgresql`         |

---

## 🧠 Useful Commands

### 📦 Run SQL Command Directly (one-liner)
```bash
docker exec -it DMB psql -U DMB -d riven -c 'SELECT COUNT(*) FROM media;'
```

### 🧭 Enter the Container & PostgreSQL Shell
```bash
docker exec -it DMB /bin/bash
psql -U DMB -d riven
```

### 🗑️ Drop the Riven Database
> ⚠️ This will permanently delete the Riven database. Be sure you’ve backed up anything important.

From the host (one-liner):
```bash
docker exec -it DMB psql -U DMB -c 'DROP DATABASE riven;'
```

From inside the container:
```bash
docker exec -it DMB /bin/bash
psql -U DMB
DROP DATABASE riven;
```

---

## ⚙️ Configurable Settings in `dmb_config.json`
```json
"postgres": {
  "enabled": false,
  "process_name": "PostgreSQL",
  "suppress_logging": false,
  "log_level": "INFO",
  "user": "DMB",
  "password": "postgres",
  "host": "127.0.0.1",
  "port": 5432,
  "shared_buffers": "128MB",
  "max_connections": 100,
  "databases": [
    { "name": "postgres", "enabled": true },
    { "name": "pgadmin", "enabled": true },
    { "name": "zilean", "enabled": true },
    { "name": "riven", "enabled": true }
  ],
  "config_dir": "/postgres_data",
  "config_file": "/postgres_data/postgresql.conf",
  "initdb_args": "--data-checksums",
  "user": "DMB",
  "password": "postgres",
  "shared_buffers": "128MB",
  "max_connections": 100,
  "run_directory": "/run/postgresql",
  "command": "postgres -D {postgres_config_dir} -c config_file={postgres_config_file}",
  "env": {}  
}
```

### 🔍 Configuration Key Descriptions
- **`enabled`**: Whether to start the PostgreSQL service.
- **`process_name`**: The label used in logs and process tracking.
- **`suppress_logging`**: If `true`, disables log output for this service.
- **`log_level`**: Logging verbosity level (e.g., `DEBUG`, `INFO`).
- **user/password** – Default database credentials.
- **shared_buffers** – Amount of memory allocated to PostgreSQL.
- **max_connections** – Maximum simultaneous database connections.
- **databases** – List of databases to initialize, with each entry containing:
    - **name** – Name of the database.
    - **enabled** – Whether this database should be created.
- **config_dir** – Directory where PostgreSQL configuration files are stored.
- **config_file** – Path to the primary PostgreSQL configuration file.
- **initdb_args** – Additional arguments passed to initdb during database initialization.
- **run_directory** – Directory where PostgreSQL runtime files (like sockets) are stored.
- **command** – The command used to start PostgreSQL.
- **env** – Dictionary of environment variables passed to the process.


---

## 🧠 Tips
- Always restart the container after modifying config files in `/postgres_data`.
- Ensure you mount `/postgres_data` if you want persistent databases.
- [pgAdmin](../services/pgadmin.md) is the easiest way to visually explore and manage PostgreSQL.

---

## 📚 More Info
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
