
# Changing the Parent of a Process in Linux (Ubuntu)

This guide explains how to change the parent process (PPID) of a running process on Ubuntu. This is typically done for better process management or for learning how `init`/`systemd` handles orphaned processes.


## Video Explanation

For a visual explanation, watch this video:

▶️ [Watch on YouTube](https://youtu.be/GaZXmERweqE)


## Step 1: Create a Child Process

Start a simple process in the background, such as `sleep`:

```bash
sleep 3600 &
````

## Step 2: View the Process Info with PID and PPID

To check the PID and PPID of the process:

```bash
ps -eo pid,ppid,cmd | grep sleep
```

Or in a more structured format:

```bash
ps -fj -p $(pgrep sleep)
```

Example output:

```
UID        PID  PPID  C STIME TTY          TIME CMD
user     12345 67890  0 14:30 pts/0    00:00:00 sleep 3600
```

## Step 3: Detach the Process from Its Current Parent

### Method A: Using `disown`

```bash
disown %1  # Assumes the sleep command is the first background job
```

### Method B: Using `nohup`

```bash
nohup sleep 3600 &
```

> Both methods ensure that the process continues running even after the terminal is closed.

## Step 4: Change Parent to `init` (PID=1)

Once the process is detached, it will automatically be adopted by `init` or `systemd` (PID=1).

To confirm:

```bash
ps -o pid,ppid,cmd -p $(pgrep sleep)
```

## Step 5 (Optional): Reassign to a Custom Parent Process with `reptyr`

### 1. Install `reptyr`:

```bash
sudo apt install reptyr
```

### 2. Allow `ptrace` Access:

```bash
echo 0 | sudo tee /proc/sys/kernel/yama/ptrace_scope
```

> To make this change permanent, edit `/etc/sysctl.d/10-ptrace.conf` or a similar config file.

### 3. Get the PID of a New Terminal:

In the new terminal:

```bash
echo $$
```

### 4. Attach the `sleep` Process to the New Terminal:

```bash
reptyr PID_SLEEP
```

## Step 6: Final Verification

To verify the updated PPID:

```bash
ps -eo pid,ppid,cmd | grep sleep
```

* If you used `disown` or `nohup`, the PPID should be `1`.
* If you used `reptyr`, the PPID should match the new terminal's PID.

---

## Resources

* man pages: `ps`, `disown`, `nohup`, `reptyr`
* [reptyr GitHub](https://github.com/nelhage/reptyr)
