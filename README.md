## 📘 Exploring `kill` Signals in Linux with `xclock` Testing

---

### ✅ Overview of System Signals in Linux

Linux uses signals as a mechanism for inter-process communication or for kernel-to-process interaction. Here’s a complete list of the 64 standard signals, each with a short explanation:

| No.   | Signal Name | Description                                                             |
| ----- | ----------- | ----------------------------------------------------------------------- |
| 1     | SIGHUP      | Hangup detected on controlling terminal or death of controlling process |
| 2     | SIGINT      | Interrupt from keyboard (like Ctrl+C)                                   |
| 3     | SIGQUIT     | Quit from keyboard, produces core dump                                  |
| 4     | SIGILL      | Illegal instruction                                                     |
| 5     | SIGTRAP     | Trace/breakpoint trap (debugging)                                       |
| 6     | SIGABRT     | Abort signal from process                                               |
| 7     | SIGBUS      | Bus error (bad memory access)                                           |
| 8     | SIGFPE      | Floating-point exception (e.g. divide by zero)                          |
| 9     | SIGKILL     | Kill signal — cannot be caught or ignored                               |
| 10    | SIGUSR1     | User-defined signal 1                                                   |
| 11    | SIGSEGV     | Invalid memory reference (Segfault)                                     |
| 12    | SIGUSR2     | User-defined signal 2                                                   |
| 13    | SIGPIPE     | Broken pipe — write to pipe with no reader                              |
| 14    | SIGALRM     | Timer signal from `alarm()`                                             |
| 15    | SIGTERM     | Termination signal                                                      |
| 16    | SIGSTKFLT   | Stack fault (obsolete)                                                  |
| 17    | SIGCHLD     | Child stopped or terminated                                             |
| 18    | SIGCONT     | Continue a stopped process                                              |
| 19    | SIGSTOP     | Stop process (cannot be caught or ignored)                              |
| 20    | SIGTSTP     | Stop typed at terminal (Ctrl+Z)                                         |
| 21    | SIGTTIN     | Background read attempted from tty                                      |
| 22    | SIGTTOU     | Background write attempted to tty                                       |
| 23    | SIGURG      | Urgent condition on socket                                              |
| 24    | SIGXCPU     | CPU time limit exceeded                                                 |
| 25    | SIGXFSZ     | File size limit exceeded                                                |
| 26    | SIGVTALRM   | Virtual alarm clock                                                     |
| 27    | SIGPROF     | Profiling timer expired                                                 |
| 28    | SIGWINCH    | Window size change                                                      |
| 29    | SIGIO       | I/O now possible                                                        |
| 30    | SIGPWR      | Power failure                                                           |
| 31    | SIGSYS      | Bad system call                                                         |
| 32–64 | SIGRTMIN+   | Real-time signals used by applications                                  |

---

### 🧪 Testing 10 Important Signals on `xclock`

To observe the behavior of various signals, the `xclock` GUI app was used. The following table documents the result of sending 10 signals:

| No. | Signal  | Code | Command Used     | Observed Effect                        |
| --- | ------- | ---- | ---------------- | -------------------------------------- |
| 1   | SIGSTOP | 19   | `kill -19 <PID>` | `xclock` froze (stopped execution)     |
| 2   | SIGCONT | 18   | `kill -18 <PID>` | `xclock` resumed                       |
| 3   | SIGTERM | 15   | `kill -15 <PID>` | Closed gracefully                      |
| 4   | SIGINT  | 2    | `kill -2 <PID>`  | Closed, similar to graceful exit       |
| 5   | SIGTSTP | 20   | `kill -20 <PID>` | No effect (in GUI apps, often ignored) |
| 6   | SIGKILL | 9    | `kill -9 <PID>`  | Killed instantly                       |
| 7   | SIGHUP  | 1    | `kill -1 <PID>`  | Closed (simulates terminal hang-up)    |
| 8   | SIGUSR1 | 10   | `kill -10 <PID>` | No visible effect                      |
| 9   | SIGUSR2 | 12   | `kill -12 <PID>` | No visible effect                      |
| 10  | SIGALRM | 14   | `kill -14 <PID>` | No visible effect                      |

---

### 🧭 Step-by-Step Instructions for Running the Experiment

1. **Start the `xclock` app**:

   ```bash
   xclock &
   ```

2. **Get the process ID (PID)**:

   ```bash
   pidof xclock
   ```

3. **Send signal to the process**:

   ```bash
   kill -<signal_number> <PID>
   # or
   kill -SIGNAME <PID>
   ```

   **Example**:

   ```bash
   kill -SIGTERM 1234
   ```

---


## Video Explanation

For a visual explanation, watch this video:

▶️ [Watch on YouTube](https://youtu.be/yXnZsuMsInw)




### 📌 Notes

* `SIGKILL` and `SIGSTOP` cannot be caught, blocked, or ignored.
* Signals like `SIGUSR1`, `SIGUSR2`, and `SIGALRM` are application-defined — visible behavior only occurs if the app handles them.
* Always verify the target PID before sending signals to avoid terminating critical processes.

---
