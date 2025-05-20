## 📝Exercise 11: Difference Between NI and PRI and Modifying Process Priority Using `chrt`


### Video Explanation

For a visual explanation, watch this video:

▶️ [Watch on YouTube](https://youtu.be/N8KltYtGfXA)


### 🔹 a) What is the difference between NI and PRI in processes?

* **NI (Nice value):** A value ranging from `-20` to `+19`, used only for normal processes (with the `SCHED_OTHER` scheduling policy). A lower value means higher priority.

* **PRI (Priority):** The actual process priority used by the kernel for scheduling. For real-time processes, PRI is set separately from NI and ranges from `1` to `99`.

> In summary:
>
> * **NI** → Only used for normal processes.
> * **PRI** → Applies to all processes (both real-time and non-real-time). In real-time processes, it is independent of NI and user-configurable.

---

### 🔹 b) What is the formulaic relationship between NI and PRI?

For normal (non-real-time) processes:

```
PRI ≈ 20 + NI
```

For real-time processes:

```
PRI = real-time priority (1 to 99)
NI has no effect.
```

---

### 🔹 c) How to change a process's priority by modifying PRI (using `chrt`)

Steps performed:

1. Run the `xclock` program in the background:

   ```bash
   xclock &
   ```

2. Find the process PID (e.g., using `ps` or):

   ```bash
   ps -eo pid,ni,pri,comm | grep xclock
   ```

   Example output:

   ```
   12345   0  20 xclock
   ```

3. Check the current scheduling policy and PRI:

   ```bash
   chrt -p 12345
   ```

   Sample output:

   ```
   pid 12345's current scheduling policy: SCHED_OTHER
   pid 12345's current scheduling priority: 0
   ```

4. Change the policy to **SCHED\_RR** with priority 50:

   ```bash
   sudo chrt -r -p 50 12345
   ```

5. Re-check the new settings:

   ```bash
   chrt -p 12345
   ```

   Now it should show:

   ```
   pid 12345's current scheduling policy: SCHED_RR
   pid 12345's current scheduling priority: 50
   ```

6. View NI and PRI using `ps`:

   ```bash
   ps -eo pid,ni,pri,comm | grep xclock
   ```

   Example output:

   ```
   12345   -  90 xclock
   ```

   Note: For real-time processes, NI may appear as `-`, and PRI will be a number between 1 and 99.

---

### 🧠 Final Note:

* The `nice` command only affects NI (for normal `SCHED_OTHER` processes).
* The `chrt` command is the correct tool to set PRI for real-time processes.

