---
tags:
  - Lab 1
  - Count Your Instructions
  - terminal
  - lscpu
  - objdump
  - perf
  - machine instructions
  - Python
  - C++
search:
  boost: 2
---

# Lab 1 · Count Your Instructions — Exploring Your Machine

This lab is different from the others: there is no breadboard and no motor. Today you explore what the computer is actually doing when it runs code. You will use the terminal to inspect your Raspberry Pi's hardware, look inside a compiled program, and count how many machine instructions two different programs execute to do the same job.

!!! note "Where are the lab files?"
    The `HOTIS-count-till-py.py`, `HOTIS-count-till-cpp.cc`, and compiled files are pre-installed on your Pi image. Ask your instructor if you are not sure which directory to find them in.

---

## Step 1 · Access the Terminal

Look for the grey icon with a white `>_` in the top-left corner of the desktop and click it.

→ See [Using the terminal](../getting-started/using-the-terminal.md) if you need help opening or navigating it.

---

## Step 2 · Check your CPU

```
lscpu
```

This shows details about the processor in your Pi. What architecture is it? How many cores does it have?

→ See [Exploring your system](../getting-started/exploring-your-system.md) for what these fields mean.

---

## Step 3 · Check Memory

```
cat /proc/meminfo
```

Look for `MemTotal`. How much RAM does this machine have?

---

## Step 4 · Check Storage

```
df -h
```

Find the row for `/`. How much total storage does the Pi have, and how much is used?

---

## Step 5 · Show All Files

```
ls -al
```

This lists every file and folder in your current directory. You will use this constantly throughout all the labs.

---

## Step 6 · Navigate the File System

Practice moving around:

```
cd <a directory name>
```

Move into a folder you saw in `ls -al`. To come back:

```
cd ..
```

`..` always means "up one level." → See [Using the terminal](../getting-started/using-the-terminal.md) for more detail.

---

## Step 7 · Look at the Programs

Navigate to the directory where the Lab 1 files live (ask your instructor if needed), then open the source files:

```
geany HOTIS-count-till-py.py
geany HOTIS-count-till-cpp.cc
```

Both programs count up to a number you give them. One is Python; one is C++. Read them side by side. How similar are they? How different?

Now look inside the compiled C++ file:

```
objdump -d HOTIS-count-till-cpp.o
```

This **disassembles** the compiled object file — it shows you the raw machine instructions the compiler produced. This is what the CPU actually runs. → See [Compiled vs interpreted](../concepts/compiled-vs-interpreted.md) to understand what you are looking at.

---

## Step 8 · Run the Programs

```
python HOTIS-count-till-py.py <a number of your choice>
./HOTIS-count-till-cpp.out <a number of your choice>
```

Replace `<a number of your choice>` with an actual integer, like `500` or `1000`.

!!! question "Try it — make a prediction"
    Before running Step 9, write down your guess: how many machine instructions do you think each program executes to count to that number? More for Python or more for C++? By how much?

---

## Step 9 · Count the Machine Instructions

```
perf stat -e instructions:u python HOTIS-count-till-py.py <your number>
perf stat -e instructions:u ./HOTIS-count-till-cpp.out <your number>
```

`perf stat -e instructions:u` counts the actual number of user-space machine instructions that ran while executing the command.

- Who guessed closest?
- Are you surprised by how different (or similar) the two counts are?
- What does this tell you about the difference between a compiled language and an interpreted one?

→ See [Compiled vs interpreted](../concepts/compiled-vs-interpreted.md) for the explanation.

---

## Step 10 · Shut Down

At the end of your session, shut down safely:

```
shutdown now
```

!!! warning "Never unplug the Pi while it's running"
    See [Shutting down safely](../getting-started/shutting-down.md) for why this matters.
