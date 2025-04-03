---
title: Deployment
---

# 🚀 Deployment Overview

DMB can be deployed across a variety of platforms and environments. Whether you're using **Docker**, **Portainer**, **Unraid**, **WSL2**, or another method, this section will guide you through the available options to get DMB up and running.

All deployment methods provide access to the same integrated services and configurations, with slight differences in how the container is started and managed.

---

## 📦 Available Deployment Guides

### 🐳 Docker Compose
Quickest way to get started using Docker CLI and `docker-compose.yml`.
- [Deploy with Docker](docker.md)

### 📚 Portainer
Deploy using the Portainer web interface.
- [Deploy with Portainer](portainer.md)

### 🧯 Unraid
Deploy using the Unraid Community Applications plugin and container template.
- [Deploy with Unraid](unraid.md)

### 💻 WSL2 (Windows Subsystem for Linux)
Deploy DMB in a WSL2 environment on Windows 11.
- [Deploy with WSL](wsl.md)

---

## 🔐 Additional Notes

- All methods rely on a valid and accessible `dmb_config.json` file for configuring services.
- It is strongly recommended to bind-mount a local `config` directory to persist user data.

Example:
```yaml
dmb:
  image: iampuid0/dmb:latest
  volumes:
    - ./config:/config
```

For more about configuring services, see the [Configuration](../features/configuration.md) page.

---

## 📎 Related Pages
- [Service Overview](../services/index.md)
- [Features](../features/index.md)
