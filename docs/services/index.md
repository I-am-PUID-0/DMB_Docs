---
title: Services Overview
---

# Services Overview

DMB is composed of multiple services that work together to provide a complete automated media management system. Each service can be configured, updated, and monitored independently, and serves a specific function within the DMB ecosystem.

Below is a summary of the available services:

---

## 🧩 How the Services Work Together

DMB is built as a collection of microservices, each fulfilling a specific role in the pipeline:

1. **User Interaction**

       - 🖥️ **DMB Frontend** provides a graphical interface for managing all services.

2. **API & Coordination**

    - 🔌 **DMB API** acts as a centralized endpoint for frontend communication and coordinating actions between services.

3. **Metadata Management & Discovery**

    - 🧠 **Riven Backend** searches and indexes content, initiates downloads, and maintains integration with media platforms (Trakt, Overseerr, Plex).
    - 🎨 **Riven Frontend** interfaces directly with the backend to manage searches, downloads, and settings.

    !!! note "See the [Riven Wiki](https://rivenmedia.github.io/wiki/) for more details"

4. **Metadata Caching**

    - 🧠 **Zilean** caches metadata (e.g., hashes, filenames) and serves repeated requests to reduce lookup time for content Riven is indexing. In particular, [Debrid Media Manager](https://github.com/debridmediamanager/debrid-media-manager) (DMM) community hashes are leveraged to in an attempt to parse available content from Real-Debrid.

    !!! note "See the [Zilean Wiki](https://ipromknight.github.io/zilean/getting-started.html) for more details"

5. **Content Acquisition**

    - ⚡ **Zurg** interfaces with Real-Debrid to manage content on the debrid service; e.g., create download links for streaming, repair broken links, sort content into directories based on regex (movies, shows, etc), and other advance functions. Within DMB, it can run as multiple named instances (e.g., using two Real-Debrid accounts in parallel) and works alongside Riven or [Debrid Media Manager](https://github.com/debridmediamanager/debrid-media-manager) (DMM) to fetch and serve content on demand.

    !!! note "See the [Zurg Repo](https://github.com/debridmediamanager/zurg-testing) for more details"

6. **Cloud Storage Mounting**

    - ☁️ **rclone** mounts debrid storage (via WebDAV or similar) inside the container, making downloaded content available to other services. It is generally used with Zurg to mount the WebDAV content provided by Zurg.

7. **Persistent Storage and Management**

    - 🗃️ **PostgreSQL** provides the primary database layer for Zilean, Riven, and pgAdmin.
    - 📊 **pgAdmin 4** gives users a web-based interface for inspecting and managing PostgreSQL.

## 🧱 Core Service Summaries

### 📊 pgAdmin 4
A web-based UI for managing PostgreSQL databases. Automatically configured to connect to the PostgreSQL instance used by DMB.

- Default Port: `5050`
- Data Directory: `/pgadmin/data`
- Credentials: `setup_email` / `setup_password`

---

### 🗃️ PostgreSQL
The core database for DMB services, including Riven, Zilean, and pgAdmin.

- Default Port: `5432`
- User: `DMB`
- Preloaded Databases: `postgres`, `pgadmin`, `zilean`, `riven`

---

### ☁️ rclone
Used to mount remote cloud storage (such as Real-Debrid WebDAV) into the container.

- Works with `Zurg` for fetching content
- Mount Directory: `/data`
- Config Directory: `/config`

---

### 🧠 Riven Backend
Handles media tracking, search, download orchestration, and integration with Plex, Trakt, and Overseerr.

- Default Port: `8080`
- Config File: `/riven/backend/data/settings.json`
- Environment: `/riven/backend/src/.env`

---

### 🎨 Riven Frontend
Web interface for controlling and monitoring the Riven backend.

- Default Port: `3000`
- Version: configurable via release or branch
- Config Directory: `/riven/frontend`

---

### 🧠 Zilean
Caches metadata and hash lookups to reduce repeat requests for the same content. Written in .NET and Python.

- Default Port: `8182`
- Config File: `/zilean/app/data/settings.json`
- Environment variables are automatically injected for performance and compatibility.

---

### ⚡ Zurg
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
