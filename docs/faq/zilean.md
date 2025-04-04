---
title: Zilean FAQ
---

# Zilean FAQ

Below are some common questions and solutions related to Zilean when used with **DMB**.

---

## ❓ Frequently Asked Questions (FAQ)

### Why is Zilean spamming my logs!?!

This is normal for a first-time run of Zilean. 

Zilean parses all the DMM hash lists and saves them into the PostgreSQL database. 

Then, it will run a scheduled update to add/remove any new hash content. 

!!! note "Depending on the system, the first-time run can take hours to days."