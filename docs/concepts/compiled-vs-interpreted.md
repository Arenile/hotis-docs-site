---
tags:
  - compiled
  - interpreted
  - machine instructions
  - Python
  - C++
  - objdump
  - perf
  - Lab 1
---

# Compiled vs Interpreted

Lab 1 asks you to measure and compare how many machine instructions two programs use to do the same job — one written in Python, one in C++. This page explains the concepts behind that experiment.

---

## What is a machine instruction?

Your CPU — the main chip that runs everything — operates on tiny, fundamental operations called **machine instructions**: add two numbers, move data from one place to another, compare two values, jump to a different place in the program. Each instruction is one step the processor actually executes.

A machine instruction is not a line of Python or C — it is much more primitive. A single line of a high-level language might translate into dozens or hundreds of machine instructions.

---

## Compiled languages (C, C++)

When you write a C++ program and run `make`, a program called the **compiler** reads every line of your source code and translates the whole thing into a binary file of machine instructions — all at once, before the program runs.

When you later run the program, the CPU executes those pre-translated instructions directly. There is no intermediary; the CPU is running exactly what the compiler produced.

`objdump -d` lets you peek inside a compiled file and see those machine instructions in a human-readable form called **assembly language**:

```
objdump -d HOTIS-count-till-cpp.o
```

Each line of assembly you see corresponds to one (or a few) machine instructions the CPU will execute.

---

## Interpreted languages (Python)

Python works differently. When you run a Python program, a separate program called the **interpreter** reads your source code one line at a time, figures out what it means, and translates it into machine instructions on the fly — while the program is running.

This translation overhead happens every single time the program runs. The interpreter itself is a compiled program, so running even a simple Python script involves executing the interpreter's machine instructions in addition to what your script needs.

---

## Why the counts differ so much

Because Python re-translates your code every time it runs, and because the interpreter itself is doing a lot of work behind the scenes, a Python program typically executes many more machine instructions than the equivalent C++ program.

The `perf stat -e instructions:u` command counts exactly how many user-space machine instructions were executed:

```
perf stat -e instructions:u ./HOTIS-count-till-cpp.out 500
perf stat -e instructions:u python HOTIS-count-till-py.py 500
```

How different do you think the counts will be? Make a prediction before you run it — that is the Lab 1 game.

---

## Why this matters for later labs

The motor labs are written in C (a compiled language). One reason: C code runs efficiently with few instructions and fast response times. When you need a motor to respond quickly to a sensor, you do not want an interpreter getting in the way.

---

## See also

- [Exploring your system](../getting-started/exploring-your-system.md)
- [Building & running](../getting-started/build-and-run.md)
- [Lab 1 · Count Your Instructions](../labs/lab-1-count-your-instructions.md)
