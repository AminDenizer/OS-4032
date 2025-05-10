

# Comparing systemd and SysVinit with Real Commands (No Code Required)

![GRUB Setup](https://github.com/AminDenizer/OS-4032/blob/practice5/initVSsystemd.gif)

This guide explains the differences between `systemd` and `SysVinit` using real-life terminal commands, without writing or creating any custom services.

---

## ✅ What You’ll Do

1. Check current init system
2. Compare startup service tools
3. Explore service management
4. Analyze logs
5. View boot performance (systemd only)

---

## 🔍 Step-by-Step Commands

### 1. Check which init system is running

```bash
ps -p 1 -o comm=
````

* If output is `systemd`, you are using systemd.
* If output is `init` or `sysv`, you are on SysVinit.

---

### 2. List services

#### systemd:

```bash
systemctl list-units --type=service
```

#### init:

```bash
ls /etc/init.d/
```

---

### 3. Start, Stop, Enable, Disable a Service

#### systemd:

```bash
sudo systemctl start ssh
sudo systemctl stop ssh
sudo systemctl enable ssh
sudo systemctl disable ssh
```

#### init:

```bash
sudo service ssh start
sudo service ssh stop
sudo update-rc.d ssh enable
sudo update-rc.d ssh disable
```

---

### 4. View Logs

#### systemd:

```bash
journalctl -u ssh
```

#### init:

```bash
cat /var/log/syslog | grep ssh
```

---

### 5. Analyze Boot Time (only in systemd)

```bash
systemd-analyze
systemd-analyze blame
```

---

## 📝 Summary of Differences

| Feature         | systemd                | SysVinit       |
| --------------- | ---------------------- | -------------- |
| Boot speed      | Faster                 | Slower         |
| Parallel boot   | Yes                    | No             |
| Logs            | `journalctl`           | Log files      |
| Service files   | `/etc/systemd/system/` | `/etc/init.d/` |
| Dependency mgmt | Automatic              | Manual         |

---

## 🎯 Recommended: Record Terminal While Running These Commands

You don’t need to create services or programs — just demonstrate:

* Checking active init system
* Starting/stopping services
* Viewing logs
* Comparing file structure and boot analysis
