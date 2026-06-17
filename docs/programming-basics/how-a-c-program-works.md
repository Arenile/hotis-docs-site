---
tags:
  - C
  - include
  - define
  - setup
  - loop
  - structure
---

# How a C Program Works

This page explains the skeleton of every `.c` file you work with in these labs.

---

## `#include` — importing tools

At the top of most `.c` files you will see lines like:

```c
#include <stdio.h>
#include <wiringPi.h>
```

`#include` tells the compiler to pull in a **header file** — a list of function definitions from a library. Think of it like looking up a word in a dictionary before you use it: the compiler needs to know what `printf` or `analogRead` means before it can compile your code.

- `<stdio.h>` provides `printf` and other input/output functions.
- `<wiringPi.h>` provides `pinMode`, `digitalWrite`, `analogRead`, and the other GPIO functions.

---

## `#define` — naming constants

```c
#define PI 3.14159
#define MAX_SPEED 100
```

`#define` creates a named constant. Before compilation, the compiler replaces every use of `PI` in the code with `3.14159`. This is exactly like a find-and-replace — it is not a variable and it does not occupy memory at runtime.

Using named constants instead of bare numbers makes code easier to read and easier to change. If you decide `MAX_SPEED` should be 200 instead of 100, you change one line instead of hunting through every place you wrote `100`.

---

## `setup()` and `loop()`

The motor lab files are structured around two functions:

```c
void setup(void) {
    // runs once, right at the start
}

void loop(void) {
    // runs over and over, forever
}
```

- **`setup()`** is called once when the program starts. Use it to configure pins and initialize anything that only needs to happen once.
- **`loop()`** is called repeatedly in an endless loop. Every sensor read, motor command, and print statement you want to happen continuously goes here.

### Where is `main()`?

In a standard C program, execution starts in `main()`. In these labs, `main()` is already written for you inside `core.c`. It calls `setup()` once and then calls `loop()` in an infinite loop. You do not need to write or edit `core.c`.

---

## See also

- [Variables & types](variables-and-types.md)
- [Pins & constants](../reference/pins-and-constants.md)
- [Building & running](../getting-started/build-and-run.md)
