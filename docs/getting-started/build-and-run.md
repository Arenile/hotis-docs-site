---
tags:
  - make
  - compile
  - run
  - sudo
  - build
---

# Building & Running

Before your C program can run, it must be **compiled** — translated from the code you wrote into instructions the CPU can execute directly. This page explains how to do that.

---

## What "compiling" means

When you write C code, you are writing instructions for humans to read. The CPU does not understand C. A program called the **compiler** reads your `.c` file and translates it into a binary file — a sequence of machine instructions that the CPU executes directly.

If there are any mistakes in your code (typos, missing semicolons, etc.), the compiler stops and tells you what went wrong. See [Reading error messages](reading-errors.md) for help interpreting those messages.

---

## Building with `make`

The project uses a **Makefile** — a recipe file that knows how to compile each program. You do not need to write the compile command yourself; just tell `make` which target you want:

```
make joystick
```

```
make motor
```

```
make ai-motor
```

When it succeeds you will see output ending in something like:

```
gcc -o joystick joystick.c core.c -lwiringPi -lm
```

No red errors = success. The compiled binary appears in the same folder.

---

## Running the program

After a successful build, run the binary with `./`:

```
./joystick
```

The `./` tells the terminal "run this file from the current directory." Without it, the terminal looks for the program in system-wide locations and won't find yours.

### Running with an argument

Some programs take a value when you run them, like the Lab 1 counting programs:

```
./HOTIS-count-till-cpp.out 500
```

The number after the program name is called a **command-line argument**. The program uses it as input.

### `sudo` — running with administrator permissions

Some programs need administrator (root) access to use the GPIO pins:

```
sudo ./motor
```

`sudo` stands for "superuser do." Your handout will tell you when `sudo` is needed — follow the exact run command printed there.

---

!!! warning "Always follow the handout's run command"
    Some programs in these labs need `sudo` and some don't. The safest rule: use the exact command your handout tells you to use for each program.

## See also

- [Reading error messages](reading-errors.md)
- [Resetting your work](resetting-your-work.md)
