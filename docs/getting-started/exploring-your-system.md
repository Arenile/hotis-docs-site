---
tags:
  - lscpu
  - meminfo
  - df
  - system info
  - Lab 1
---

# Exploring Your System

These commands let you inspect the hardware and storage on your Raspberry Pi. You use them in Lab 1.

---

## `lscpu` — CPU information

```
lscpu
```

Prints details about the processor: its architecture, how many cores it has, clock speed, and more. Look for lines like `Architecture`, `CPU(s)`, and `CPU max MHz`.

On a Raspberry Pi 5 you will see an ARM architecture and four cores — a different design than the Intel/AMD chips in most laptops.

---

## `cat /proc/meminfo` — memory information

```
cat /proc/meminfo
```

`cat` prints the contents of a file. `/proc/meminfo` is a special file the Linux kernel keeps up-to-date with current memory statistics. Look for `MemTotal` (total installed RAM) and `MemAvailable` (how much is free right now).

Memory is measured in kilobytes (kB) in this output. Divide by 1024 to get megabytes, divide again by 1024 to get gigabytes.

---

## `df -h` — storage (disk) information

```
df -h
```

`df` stands for "disk free." The `-h` flag means "human readable" — it shows sizes in KB, MB, or GB instead of raw block counts. Look at the row for `/` (the root of the file system) to see how much storage the Pi has and how much is used.

---

!!! note "Why does this matter?"
    Lab 1 asks you to compare a Python program and a C++ program that do the same job. Before you look at code, it helps to know what kind of machine you are working with. The same program behaves differently on different hardware.

## See also

- [Using the terminal](using-the-terminal.md)
- [Compiled vs interpreted](../concepts/compiled-vs-interpreted.md)
- [Lab 1 · Count Your Instructions](../labs/lab-1-count-your-instructions.md)
