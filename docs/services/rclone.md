# rclone

rclone is a command-line tool used in DMB to mount cloud storage—specifically Debrid services like Real-Debrid—into the container as a local file system. It works in tandem with Zurg and is configured automatically during container startup.

---

## ⚙️ Configuration Summary
Each `rclone` instance is defined under the `rclone.instances` section in `dmb_config.json`. Example:
```json
"rclone": {
  "instances": {
    "RealDebrid": {
      "enabled": true,
      "process_name": "rclone w/ RealDebrid",
      "suppress_logging": false,
      "log_level": "INFO",
      "key_type": "RealDebrid",
      "zurg_enabled": true,
      "mount_dir": "/data",
      "mount_name": "rclone_RD",
      "cache_dir": "/cache",
      "config_dir": "/config",
      "config_file": "/config/rclone.config",
      "zurg_config_file": "/zurg/RD/config.yml",
      "command": [],
      "api_key": ""
    }
  }
}
```

### 🔍 Configuration Key Descriptions
- **`enabled`**: Whether this rclone instance should be started.
- **`process_name`**: The label used in logs and process tracking.
- **`suppress_logging`**: If `true`, disables log output for this service.
- **`log_level`**: Logging verbosity level (e.g., `DEBUG`, `INFO`).
- **`key_type`**: The debrid service to use (`RealDebrid`, `AllDebrid`, etc.).
- **`zurg_enabled`**: Whether Zurg is linked to this rclone mount.
- **`mount_dir`**: The container path where the remote drive is to be mounted.
- **`mount_name`**: The rclone remote name.
- **`cache_dir`**: Directory used by rclone for VFS caching, when enabled.
- **`config_dir`**: Directory where the rclone config file is stored.
- **`config_file`**: Full path to the rclone configuration file.
- **`zurg_config_file`**: Full path to the Zurg config file for this instance.
- **`command`**: Custom CLI arguments to be appended to rclone at runtime.
- **`api_key`**: (Optional) Debrid API key, used if Zurg is not linked.

### 🔁 API Key Behavior
- If `zurg_enabled` & `zurg_config_file` are **set**: DMB will configure rclone to use **Zurg's WebDAV** endpoint. The API key should be defined in the **Zurg instance**, not the rclone one.
- If `zurg_enabled` & `zurg_config_file` are **unset or blank**: **(Future release)** DMB will configure rclone to **directly connect to the debrid service**, and the API key must be set in the rclone instance.

### ➕ Adding More Instances
Users can define additional rclone instances by duplicating the structure and ensuring:

- Each `instance name` is **unique**
- Each `process_name` is **unique**
- The `key_type` must match the type of Debrid service used (e.g., `RealDebrid`, `AllDebrid`, `TorBox`, `Premiumize`)

Example:
```json
"rclone": {
  "instances": {
    "RealDebrid": {
      "enabled": true,
      "process_name": "rclone w/ RealDebrid",
      "suppress_logging": false,
      "log_level": "INFO",
      "key_type": "RealDebrid",
      "zurg_enabled": true,
      "mount_dir": "/data",
      "mount_name": "rclone_RD",
      "cache_dir": "/cache",
      "config_dir": "/config",
      "config_file": "/config/rclone.config",
      "zurg_config_file": "/zurg/RD/config.yml",
      "command": [],
      "api_key": ""
    },    
    "AllDebrid": {
      "enabled": false,
      "process_name": "rclone w/ AllDebrid",
      "suppress_logging": false,
      "log_level": "INFO",
      "key_type": "AllDebrid",
      "zurg_enabled": false,
      "mount_dir": "/data",
      "mount_name": "rclone_AD",
      "cache_dir": "/cache",
      "config_dir": "/config",
      "config_file": "/config/rclone.config",
      "zurg_config_file": "",
      "command": [],
      "api_key": ""
    }
  }
}
```

---

## 🧠 Features Enabled by DMB

### 🔄 Auto-Generated `rclone.config`
DMB generates the required `rclone.config` file at runtime. This includes:
```ini
[rclone_RD]
type = webdav
url = http://localhost:9999/dav
vendor = other
pacer_min_sleep = 0
```
This eliminates the need for any manual setup.

### 🔒 Debrid API Integration
DMB supports multiple Debrid configurations **(Future release)** using a combination of `rclone` and `zurg` instances.

### 🧲 Works With Zurg
Zurg exposes a WebDAV server which rclone mounts using the configuration above.

### 🔧 rclone Flags via Environment Variables
All `--flag=value` options in rclone can be passed as environment variables. Format:
```bash
RCLONE_<OPTION_NAME_UPPERCASE>=<value>
```
Example:
```bash
RCLONE_VFS_CACHE_MODE=full
RCLONE_BUFFER_SIZE=64M
RCLONE_ATTR_TIMEOUT=30s
```
This enables advanced control without modifying CLI or config files.

For more info, see [rclone docs](https://rclone.org/docs/#environment-variables).

---

## 💻 Accessing rclone Inside the Container
To run rclone commands manually:
```bash
docker exec -it DMB /bin/bash
rclone listremotes
rclone mount rclone_RD: /mnt/test
```

---

## 🧠 Tips
- Mounts are bind-mounted into the container by default.
- If you mount `/data` to the host, you will see all Zurg-fetched content.
- Use the `ZURG_LOG_LEVEL` or `RCLONE_LOG_LEVEL` env vars to control verbosity.

---

## 📚 Resources
- [rclone Documentation](https://rclone.org/)
- [WebDAV Docs](https://rclone.org/webdav/)
- [rclone Environment Variables](https://rclone.org/docs/#environment-variables)
