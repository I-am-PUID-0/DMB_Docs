---
title: Zurg FAQ
---

# Zurg FAQ

Below are some common questions and solutions related to Zurg when used with DMB.

---

## ❓ Frequently Asked Questions (FAQ)

### ⚠️ `ERROR - rclone w/ RealDebrid subprocess: : IO error: File is temporarily unavailable: 423 Locked`
This error generally indicates that a **rate limit is being enforced by Real-Debrid**. It often occurs during media server scans that hit the API too frequently.

To mitigate this:
- If you're using **Plex**, this is commonly caused by automatic scans that trigger repeatedly.

### 🔧 Recommended Plex Library Settings
To reduce API hits and avoid triggering rate limits:

In each Plex Library, disable the following:

- `Video Preview Thumbnails`
- `Credits Detection`
- `Voice Detection`

Then go to **Settings > Library** and disable:

- `Scan my library automatically`
- `Run a partial scan when changes are detected`

See the [Plex FAQ](../faq/plex.md) for more Plex-specific recommendations and details.

---

## 📎 Related Pages
- [Zurg Configuration](../services/zurg.md)