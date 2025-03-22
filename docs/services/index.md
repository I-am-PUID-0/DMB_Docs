---
title: Services Overview
---

# Services Overview

DMB is composed of multiple services that work together to provide a complete automated media management system. Each service can be configured, updated, and monitored independently, and serves a specific function within the DMB ecosystem.

Below is a summary of the available services:

---

## 📊 pgAdmin 4
A web-based UI for managing PostgreSQL databases. Automatically configured to connect to the PostgreSQL instance used by DMB.

- Default Port: `5050`
- Data Directory: `/pgadmin/data`
- Credentials: `setup_email` / `setup_password`

---

## 🗃️ PostgreSQL
The core database for DMB services, including Riven, Zilean, and pgAdmin.

- Default Port: `5432`
- User: `DMB`
- Preloaded Databases: `postgres`, `pgadmin`, `zilean`, `riven`

---

## ☁️ rclone
Used to mount remote cloud storage (such as Real-Debrid WebDAV) into the container.

- Works with `Zurg` for fetching content
- Mount Directory: `/data`
- Config Directory: `/config`

---

## 🧠 Riven Backend
Handles media tracking, search, download orchestration, and integration with Plex, Trakt, and Overseerr.

- Default Port: `8080`
- Config File: `/riven/backend/data/settings.json`
- Environment: `/riven/backend/src/.env`

---

## 🎨 Riven Frontend
Web interface for controlling and monitoring the Riven backend.

- Default Port: `3000`
- Version: configurable via release or branch
- Config Directory: `/riven/frontend`

---

## 🧠 Zilean
Caches metadata and hash lookups to reduce repeat requests for the same content. Written in .NET and Python.

- Default Port: `8182`
- Config File: `/zilean/app/data/settings.json`
- Environment variables are automatically injected for performance and compatibility.

---

## ⚡ Zurg
A content fetching engine that connects to debrid services (currently Real-Debrid only) and feeds downloads to Rclone.

- Default Port: `9090`
- Config Directory: `/zurg/RD`
- Config File: `/zurg/RD/config.yml`

---

## 📎 Next Steps
Click on any of the service names in the sidebar or below to explore how to configure and use them:

- [pgAdmin 4](pgadmin.md)
- [PostgreSQL](postgres.md)
- [rclone](rclone.md)
- [Riven Backend](riven-backend.md)
- [Riven Frontend](riven-frontend.md)
- [Zilean](zilean.md)
- [Zurg](zurg.md)
