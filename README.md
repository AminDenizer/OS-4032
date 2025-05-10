# 🛠️ telinit

**telinit** is a lightweight utility to **switch between Linux runlevels** and **log the transitions** for documentation and auditing purposes.

---

## ✅ What It Does

* Changes the system runlevel using `telinit`
* Logs each change with timestamp
* Shows current and previous runlevels using the `runlevel` command

---

## 🔧 Usage

### Check current runlevel:

```bash
runlevel
```

### Switch to a different runlevel (e.g. runlevel 3):

```bash
sudo telinit 3
```

> You can also use `sudo teinit 3` if telinit wraps the `telinit` command and logs the action.

---

## 📁 Log File

Every time you switch runlevels with `telinit`, the change is logged here:

```
/var/log/telinit.log
```

Example log entry:

```
[2025-05-10 14:23:01] Switched from 5 to 3
```

---

## 🎥 Video Guide

Watch the video tutorial here:
👉 ▶️ [Watch on YouTube](https://youtu.be/Hz6QDE2qIBY)

---

## 🧠 Notes

* Requires root privileges for switching runlevels.
* On systems using `systemd`, you may use `systemctl isolate` instead of `telinit`.
* Classic runlevels:

  | Runlevel | Description               |
  | -------- | ------------------------- |
  | 0        | Halt / Shutdown           |
  | 1        | Single-user (rescue mode) |
  | 3        | Multi-user (no GUI)       |
  | 5        | Multi-user with GUI       |
  | 6        | Reboot                    |

---
