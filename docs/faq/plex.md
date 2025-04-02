---
title: Plex FAQ
---

# Plex FAQ

Below are commonly recommended settings and known issues when using **Plex** alongside **DMB** with services like Zurg and Rclone.

---
## ❓ Frequently Asked Questions (FAQ)

### ⚙️ Recommended Library Settings
To reduce the risk of excessive API calls to Real-Debrid (which can result in `423 Locked` errors or rate limits), the following Plex library settings should be disabled for each media library:

#### Library Settings (Per Library):
- **Video Preview Thumbnails**
- **Credits Detection**
- **Voice Detection**
- **Empty trash automatically after every scan** *(this can trigger deletions unnecessarily when using symlinked content)*

#### Global Settings (Settings > Library):
- **Scan my library automatically**
- **Run a partial scan when changes are detected**

These settings reduce the number of filesystem scans Plex performs, which can otherwise generate a high number of requests to mounted Real-Debrid content.

---

## 📎 Related Pages
- [Zurg FAQ](../faq/zurg.md)
- [Rclone Configuration](../services/rclone.md)
- [Riven Symlink Strategy](../services/riven-backend.md#symlink-directory)

