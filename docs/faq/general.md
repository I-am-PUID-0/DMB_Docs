---
title: General FAQ
---

# General FAQ

Below are some common questions and solutions related to **DMB** that apply across multiple services or the platform as a whole.

---

## ❓ Frequently Asked Questions (FAQ)

### 💾 Will DMB use a lot of storage space?

That depends on how you configure it. Most services (like Zurg and Rclone) operate by streaming content from the debrid service, so **very little is permanently stored** on your local system — unless you're using `rclone` with VFS caching enabled.

If you're using VFS cache (recommended for Plex), ensure that the cache size is managed appropriately. See the [rclone configuration](../services/rclone.md) for more.

---

### 🧱 Do I need to install every service?

No — DMB is modular. You can enable or disable services in `dmb_config.json` under each service section. Some services (like `riven_backend` or `zurg`) provide core functionality, but others (like `pgadmin`) are optional tools to help you manage your setup.

---

### 🌍 Can I run DMB offline?

Most DMB services interact with external APIs (e.g., Real-Debrid, Plex, Trakt, TMDB, etc.), so **internet access is required** for normal operation. However, local database tools (e.g., pgAdmin) and UIs may still function offline for inspection.

---

### 🔄 What happens when I update DMB?

DMB includes **auto-update** functionality for most services. Depending on your configuration (`auto_update` and `auto_update_interval`), the system will check for new versions of services like Zurg, Riven, Zilean, etc.

You can configure update frequency and behavior in each service’s section of `dmb_config.json`.

---

### 🔒 Is DMB secure?

DMB is intended to run on your **local or private server**. Most services are, by default, bound to `127.0.0.1` and not exposed publicly unless explicitly configured by exposing ports in the Docker compose or changing the bound address.

Most of the web-based UIs and APIs lack any form of authentication. 

If you're exposing services externally (e.g., via Traefik or NGINX), consider using authentication layers like OAuth2, HTTPS, and firewalls.

---

### 🛠️ Can I use my own custom version of a service?

Yes — you can point most services to a custom branch or fork by editing the `repo_owner`, `repo_name`, `branch`, or `release_version` in its config section in `dmb_config.json`. This is especially useful if you are testing development builds or your own patches.

---

### 📦 Can I back up my DMB setup?

Absolutely. The most important files to back up are:

- `dmb_config.json`
- Any data directories (e.g., `/riven/backend/data`, `/zilean/app/data`, `/pgadmin/data`, `postgres_data`)

Regularly backing these up allows you to quickly restore your environment.

---

### 📈 Can I monitor the system?

Yes — the DMB Frontend shows real-time logs, service status, and allows interactive config management. You can also access logs from the filesystem or via the DMB API (see [API docs](../api/index.md)).

---

## 📎 Related Pages

- [Configuration Guide](../features/configuration.md)
- [Service Overview](../services/index.md)
- [DMB Frontend](../services/dmb-frontend.md)
- [Deployment](../deployment/index.md)

