---
title: Configuration
---

# Configuration

## 📑 Overview
DMB relies on a **centralized configuration file**, `dmb_config.json`, to control its services, logging, API settings, and more. This file allows you to customize the behavior of DMB without modifying the source code.

DMB also supports **environment variables, .env files, and Docker secrets**. If the same setting is defined in multiple places, the **precedence is as follows:**

1. **Environment Variables** (highest priority)
2. **.env File**
3. **Docker Secrets**
4. **`dmb_config.json`** (lowest priority)

## 🛠️ Configuration File Structure
Below is the **general structure** of `dmb_config.json`:

```json
{
    "puid": 1000,
    "pgid": 1000,
    "tz": "",
    "dmb": { ... },
    "postgres": { ... },
    "pgadmin": { ... },
    "rclone": { ... },
    "riven_backend": { ... },
    "riven_frontend": { ... },
    "zilean": { ... },
    "zurg": { ... }
}
```

Each section configures a specific service. Below is a detailed breakdown of the most important sections:

!!! caution "Be Careful When Modifying `dmb_config.json`"
    While DMB is highly configurable via `dmb_config.json`,  
    some changes can cause failures during startup.  
    As such, it is **not recommended** to make modifications unless you fully understand their impact.


---

## 🔧 General Settings

### **User & Timezone**
```json
"puid": 1000,
"pgid": 1000,
"tz": ""
```

- **puid** / **pgid** – Define the user and group IDs for container execution.
- **tz** – Set the timezone (e.g., `America/New_York`).

---

## 📜 Logging Settings
Located in `dmb`:
```json
"log_level": "INFO",
"log_name": "DMB",
"log_dir": "/log",
"log_count": 2,
"log_size": "10M",
"color_log": true
```

- **log_level** – Set the logging verbosity (`DEBUG`, `INFO`, `WARNING`, `ERROR`).
- **log_dir** – Directory where logs are stored.
- **log_count** – Number of rotated logs to retain.
- **log_size** – Maximum log file size before rotation.
- **color_log** – Enables colored log output.

---

## 📡 API Service Configuration
Located in `dmb.api_service`:
```json
"enabled": true,
"process_name": "DMB API",
"log_level": "INFO",
"host": "127.0.0.1",
"port": 8000
```

- **enabled** – Whether the API service should run.
- **host** / **port** – Define where the API service runs.
- **log_level** – Logging verbosity for the API.

---

## 🌍 Frontend Configuration
Located in `dmb.frontend`:
```json
"enabled": true,
"process_name": "DMB Frontend",
"repo_owner": "nicocapalbo",
"repo_name": "dmbdb",
"port": 3005,
"auto_update": false,
"clear_on_update": true
```

- **repo_owner/repo_name** – Defines where the frontend is pulled from.
- **port** – The port where the frontend runs.
- **auto_update** – Enables automatic updates.
- **clear_on_update** – Clears existing files before updating.

---

## 🗄️ Database: PostgreSQL
Located in `postgres`:
```json
"enabled": true,
"host": "127.0.0.1",
"port": 5432,
"user": "DMB",
"password": "postgres",
"shared_buffers": "128MB",
"max_connections": 100
```

- **user/password** – Default database credentials.
- **shared_buffers** – Amount of memory allocated to PostgreSQL.
- **max_connections** – Maximum simultaneous database connections.

---

## ⚙️ Zilean Configuration
Located in `zilean`:
```json
"enabled": true,
"process_name": "Zilean",
"port": 8182,
"auto_update": false,
"config_dir": "/zilean",
"env": {
    "DOTNET_RUNNING_IN_CONTAINER": "true",
    "DOTNET_gcServer": "1",
    "DOTNET_GCDynamicAdaptationMode": "1",
    "DOTNET_SYSTEM_GLOBALIZATION_INVARIANT": "false",
    "PYTHONUNBUFFERED": "1",
    "ASPNETCORE_URLS": "http://+:{port}",
    "PYTHONPATH": "/zilean/venv/lib/python3.11/site-packages",
    "PATH": "/zilean/venv/bin:${PATH}",
    "ZILEAN_PYTHON_PYLIB": "/usr/local/lib/libpython3.11.so.1.0",
    "Zilean__Database__ConnectionString": "Host={postgres_host};Port={postgres_port};Database=zilean;Username={postgres_user};Password={postgres_password};Timeout=300;CommandTimeout=3600;"
}
```

- **port** – API port for Zilean.
- **env** – Defines environment variables used by Zilean.

---

## 📌 Next Steps
1. Review and modify `dmb_config.json` as needed.
2. For a deep dive into individual services, see the [Services](../services/index.md) section.
