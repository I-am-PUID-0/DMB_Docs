---
title: Usage
---

# Usage

## 🚀 Running DMB
Once installed and configured, DMB automatically starts the services defined in `dmb_config.json`. Each service can also be managed independently using the DMB API or by directly modifying the configuration.
!!! important "Important: Configure API Key Before Startup"
    DMB is preset to start all services on the first startup.  
    As such, please ensure `ZURG_INSTANCES_REALDEBRID_API_KEY` is configured with your RealDebrid API Key in the compose **before starting the container**.


### 🔄 Automatic Service Start
All services with `"enabled": true` in the config will be started on container launch. These typically include:
- DMB API
- DMB Frontend
- PostgreSQL
- pgAdmin 4
- rclone
- Riven Backend & Frontend
- Zilean
- Zurg

If a service fails to start, check its log file in the `/log` directory (or wherever `log_dir` is set).

---

## 🧪 Interacting with Services

### ✅ Healthcheck
A full list of currently running services is available at:
```
GET http://<host>:8000/healthcheck/running_processes.json
```
This is useful for checking container health in orchestrators like Docker Compose.

### 📊 Logs API (Added in v6.3.0)
You can retrieve logs for each service using:
```
GET /logs/{service_name}
```
Optional query parameters:
- `level` – Filter by log level (e.g., `INFO`, `ERROR`)
- `lines` – Limit the number of lines returned
- `search` – Search for a string in the logs

Example:
```
GET /logs/riven_backend?level=ERROR&lines=100
```

---

## 🔃 Managing Updates

### 🛠️ Manual Updates
Each service can be updated by modifying the configuration file or using the DMB API. Updates include:
- Branch switching
- Version pinning
- Auto-update toggling

### ⚙️ Auto-Update
Some services support automatic updates. Enable by setting:
```json
"auto_update": true,
"auto_update_interval": 24
```
- `auto_update_interval` is measured in hours.

Services supporting auto-updates:
- DMB Frontend
- Riven Backend
- Riven Frontend
- Zilean
- Zurg

---

## ⚡ Shutdown Handling
DMB handles graceful shutdown of all services. This includes:
- Stopping running processes
- Unmounting rclone mounts
- Syncing configuration states

To allow time for clean shutdowns, use:
```yaml
docker-compose:
  stop_grace_period: 60s
```

---

## 📌 Tips
- Always monitor `/log/*.log` files for troubleshooting.
- Ensure PostgreSQL is running before launching services that depend on it.
- If using Real-Debrid, ensure `api_key` is provided in rclone and Zurg instances.
- Logs can be colored if `color_log` is enabled in the config.

---

## 📎 Related Docs
- [Configuration](configuration.md)
- [Services Overview](../services/index.md)
- [API Endpoints](../api/endpoints.md)
