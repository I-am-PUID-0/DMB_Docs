---
title: Zurg FAQ
---

# Zurg FAQ

Below are some common questions and solutions related to Zurg when used with **DMB**.

---

## ❓ Frequently Asked Questions (FAQ)

### ⚠️ `ERROR - rclone w/ RealDebrid subprocess: : IO error: File is temporarily unavailable: 423 Locked`
This error generally indicates that a **rate limit is being enforced by Real-Debrid**. It often occurs during media server scans that hit the API too frequently.

To mitigate this:
- If you're using **Plex**, this is commonly caused by automatic scans that trigger repeatedly.

See the [Plex FAQ](../faq/plex.md/#️-recommended-library-settings) for more Plex-specific recommendations and details.

---

## 📎 Related Pages
- [Zurg Configuration](../services/zurg.md)