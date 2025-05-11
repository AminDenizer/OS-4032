## Exercise 9 – Managing Background Processes with `nohup`

### Goal:

Create a background process that persists after shell logout, view its output, and adjust its execution priority.

---

### A. Create a Background Process That Survives Shell Logout

#### Method 1: Test with `sleep`

```bash
nohup sleep 1000 &
```

* This process sleeps for 1000 seconds.
* `nohup` ensures the process won't be terminated if the shell is closed.
* `&` sends the process to the background.

To check its status:

```bash
jobs
```

Or after reopening the terminal:

```bash
ps aux | grep sleep
```

#### Method 2: Infinite loop printing "hello" every second

```bash
nohup bash -c 'while true; do echo "hello"; sleep 1; done' &
```

---

### B. View the Contents of `nohup.out`

By default, the output of `nohup` is redirected to a file named `nohup.out`.

To view its contents:

```bash
cat nohup.out
```

To monitor it live:

```bash
tail -f nohup.out
```

---

### C. Adjust the Process Priority (Using `nice` / `renice`)

#### 1. Find the Process ID (PID):

```bash
ps aux | grep bash
```

Or more precisely:

```bash
ps -ef | grep '[h]ello'
```

Assume the PID is `12345`.

#### 2. Change the Priority:

* To **lower** the priority (higher nice value → lower priority):

```bash
renice +10 -p 12345
```

* To **increase** the priority (lower nice value → higher priority; requires root):

```bash
sudo renice -5 -p 12345
```

---

### Stopping the Process

To stop a running process:

```bash
kill 12345
```

If it doesn't respond:

```bash
kill -9 12345
```

---

### Additional Tip: View Parent Process

To see the parent-child relationship:

```bash
ps -o pid,ppid,cmd -p 12345
```

Or use `pstree` (if installed):

```bash
pstree -p | grep bash
```

---

## Video Explanation

For a visual explanation, watch this video:

▶️ [Watch on YouTube](https://youtu.be/48lQZe_LWCo)


**End of Exercise**

These steps help you understand how to manage background processes that persist beyond shell sessions, monitor their output, and adjust their CPU scheduling priority.

