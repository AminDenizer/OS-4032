Here's the `README.md` file based on the steps you've provided:

---

# USB Runlevel Handler Setup

This guide outlines the steps to create a script that changes system runlevels when a USB device is inserted or removed. The system will switch to runlevel 3 (multi-user) when a USB is inserted and to runlevel 5 (graphical) when the USB is removed.

## Prerequisites

- A Linux system with `systemd` and `udev` support.
- Root privileges (`sudo` access).

## Steps

### 1. Check USB Information

Use the following command to check the USB information:

```bash
sudo dmesg | grep -i usb
```

This will display all USB-related events and help you find the serial number of the connected USB device.

### 2. Find the Serial Number

Search for the serial number of the USB device:

```bash
my serial for USB is A0525H14YD37000872
```

You need this serial number to identify the specific USB device in the udev rule.

### 3. Create the USB Handler Script

Create a script file to handle the runlevel changes based on USB events.

```bash
sudo nano /usr/local/bin/usb-runlevel-handler.sh
```

Add the following content:

```bash
#!/bin/bash

# Check if the USB is added or removed
if [ "$1" == "add" ]; then
    # When the USB is inserted, switch to runlevel 3 (multi-user)
    systemctl isolate multi-user.target
fi
```

Make the script executable:

```bash
sudo chmod +x /usr/local/bin/usb-runlevel-handler.sh
```

### 4. Create udev Rule

Create a udev rule to trigger the script when the USB device is added or removed:

```bash
sudo nano /etc/udev/rules.d/99-usb-runlevel.rules
```

Add the following content:

```bash
ACTION=="add|remove", SUBSYSTEM=="usb", ATTRS{serial}=="A0525H14YD37000872", RUN+="/usr/local/bin/usb-runlevel-handler.sh %E{ACTION}"
```

Make sure to replace the serial number `A0525H14YD37000872` with the serial number of your USB device.

### 5. Reload udev Rules

Reload the udev rules to apply the changes:

```bash
sudo udevadm control --reload-rules
```

---

This setup will now automatically switch the system between runlevels 3 and 5 based on the USB device events.
