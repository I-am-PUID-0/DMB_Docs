
# Riven Backend Configuration

The **Riven Backend** is the core component responsible for data handling, automation, API integrations, and scraping within the Riven ecosystem. Proper configuration ensures seamless integration with services like Overseerr, Plex, and Trakt.

## Configuration Settings in `dmb_config.json`

```json
"riven_backend": {
    "enabled": true,
    "process_name": "Riven Backend",
    "repo_owner": "rivenmedia",
    "repo_name": "riven",
    "release_version_enabled": false,
    "release_version": "v0.20.1",
    "branch_enabled": false,
    "branch": "release-please--branches--main",
    "suppress_logging": false,
    "log_level": "INFO",
    "host": "127.0.0.1",
    "port": 8080,
    "auto_update": false,
    "auto_update_interval": 24,
    "symlink_library_path": "/mnt",
    "clear_on_update": true,
    "exclude_dirs": [
        "/riven/backend/data"
    ],
    "env_copy": {
        "source": "/riven/backend/data/.env",
        "destination": "/riven/backend/src/.env"
    },
    "platforms": [
        "python"
    ],
    "command": [
        "/riven/backend/venv/bin/python",
        "src/main.py",
        "-p",
        "{port}"
    ],
    "config_dir": "/riven/backend",
    "config_file": "/riven/backend/data/settings.json",        
    "env": {},
    "wait_for_dir": "/data/rclone_RD/__all__"
},
```

### 🔍 Configuration Key Descriptions

- **`enabled`**: Whether to start the Riven Backend service.
- **`process_name`**: Used in logs and process tracking.
- **`host`**: IP address for the backend to listen on.
- **`port`**: Port exposed for the API.
- **`repo_owner`** / **`repo_name`**: GitHub repo to pull from.
- **`release_version_enabled`** / **`release_version`**: Use a tagged release if enabled.
- **`branch_enabled`** / **`branch`**: Use a specific branch if enabled.
- **`suppress_logging`**: If `true`, disables log output for this service.
- **`log_level`**: Logging verbosity level (e.g., `DEBUG`, `INFO`).
- **`host`**: IP address the backend should bind to.
- **`port`**: Port the backend API is served on.
- **`auto_update`**: Enables automatic self-updates.
- **`auto_update_interval`**: How often (in hours) to check for updates.
- **`symlink_library_path`**: Target path for media symlinks.
- **`clear_on_update`**: Clears build artifacts or cache during updates.
- **`exclude_dirs`**: Prevents specific directories from being affected by updates when using `clear_on_update`
- **`env_copy`**: Copies a `.env` file from one location to another. Such as the Riven .env discussed below
- **`platforms`**: Expected runtime environment (e.g., `python`).
- **`command`**: How the service is started.
- **`config_dir`** / **`config_file`**: Configuration directory and settings file.
- **`env`**: Dictionary of environment variables passed to the process.
- **`wait_for_dir`**: Delays startup until the specified directory exists.

---

## ⚙️ Branch / Version Targeting
You can control which version or branch of the backend is deployed by setting:

- `branch_enabled: true` and specifying a `branch`
- or `release_version_enabled: true` and specifying a `release_version`

---

## 🛠️ Setting Up Riven Backend

Riven Backend is the only service which will require additional setup before use.

Item 

---


## Riven's Environment Variables in the `.env.example`

The `.env.example` file includes:

- `RIVEN_FORCE_ENV`: Forces env vars to override `settings.json`.
- `SETTINGS_FILENAME`: Specifies the settings file name.
- `SKIP_TRAKT_CACHE`: Skips cached results.
- `HARD_RESET`: Drops and recreates all database tables.
- `REPAIR_SYMLINKS`: Fixes any broken symlinks.
- `API_KEY`: Custom static API key.
- `WORKERS`: Number of indexing workers.

Each Riven env can also be set within DMB, either through the **"env"** section of the "riven_backend" within the `dmb_config.json`, or buy utilizing methods defined in the [Configuration](../features/configuration.md) section of the docs.



[View full example on GitHub](https://github.com/rivenmedia/riven/blob/main/.env.example)

---

## Additional Resources

- [Riven Wiki](https://rivenmedia.github.io/wiki/)
- [Riven GitHub Repository](https://github.com/rivenmedia/riven)
