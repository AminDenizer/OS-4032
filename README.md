# Exercise 6 – File and Directory Operations in Linux


For a visual explanation, watch this video:

▶️ [Watch on YouTube](https://youtu.be/RorapGUXbpU)

## Part A

### 1. Create Sample Files and Folders

We begin by creating several files and directories whose names start with `f` or `g`, and some of them end with a digit (0–9):

```bash
touch ffile1 ffile2 gfile3 gfile9 fdata7 gdata8
mkdir ffolder1 gfolder2 fdir3 gdir9
````

### 2. Find Files That Start with `f` or `g` and End with a Digit

To locate files in the current directory that:

* Start with `f` or `g`
* End with a digit (0–9)

Run:

```bash
find . -maxdepth 1 -type f -regex '\./[fg].*[0-9]$'
```

### 3. Delete the Matched Files

To remove all such matched files:

```bash
find . -maxdepth 1 -type f -regex '\./[fg].*[0-9]$' -exec rm {} \;
```

---

## Part B

### Copy `/etc/shadow` Contents into a New File

The `/etc/shadow` file contains hashed passwords and is protected. You must use `sudo` to read it.

To copy its contents into a new text file:

```bash
sudo cat /etc/shadow > shadow_backup.txt
```

⚠️ **Warning:** Accessing or modifying `/etc/shadow` can pose security risks. Only perform this step for educational or administrative purposes with proper authorization.

---

## Notes

* All commands are intended for use in a Unix-like terminal (e.g., Linux).
* Run these in a safe, test-friendly environment (like a VM or container) to avoid affecting critical system files.
