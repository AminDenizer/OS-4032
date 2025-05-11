## 📘 Difference Between `available` and `free` Memory in Linux

### 🧠 Basic Concepts

When you check memory usage in Linux using `free`, `top`, or `htop`, you’ll often see two key memory indicators:

* **Free Memory**:

  * Memory that is completely unused.
  * Not being used by any program or system cache.
  * This number may be low even when your system is performing well.

* **Available Memory**:

  * Memory that is readily available for new applications.
  * Includes `free` memory **plus** memory currently used by buffers, cache, or temporary allocations that the system can reclaim.
  * A more accurate reflection of usable memory for new tasks.

🔍 **Key Point:** `available` memory is a better indicator of actual usable RAM than `free`.

---

### 🧪 Practical Test: Comparing During Application Execution

#### 1. Check memory before running any apps:

```bash
free -h
```

Sample output:

```
              total        used        free      shared  buff/cache   available
Mem:           7.7G        1.2G        3.0G        200M        3.5G        6.0G
```

#### 2. Run a resource-heavy program (e.g., OBS or screen recorder):

```bash
obs
```

or

```bash
simplescreenrecorder
```

#### 3. Check memory again:

```bash
free -h
```

Sample output:

```
              total        used        free      shared  buff/cache   available
Mem:           7.7G        2.5G        1.0G        300M        4.2G        5.0G
```

📊 As you can see:

* `free` memory decreased (more RAM is being used),
* But `available` is still high, meaning the system can still allocate memory if needed.

---

## Video Explanation

For a visual explanation, watch this video:

▶️ [Watch on YouTube](https://youtu.be/NIUUwrCrKE8)


### ✅ Conclusion

* Don’t rely on `free` memory alone — it can be misleading.
* `available` memory gives you a better understanding of how much memory your system can still use.
* Linux aggressively uses RAM for performance (e.g., caching), but will free it when necessary.
