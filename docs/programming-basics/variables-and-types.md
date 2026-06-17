---
tags:
  - variables
  - types
  - int
  - unsigned
  - declare
---

# Variables & Types

A **variable** is a named storage location. You give it a name, store a value in it, and use the name to get the value back later.

---

## Declaring a variable

In C, you must declare a variable before you use it. A declaration tells the compiler the variable's **name** and **type**:

```c
int score;
```

This reserves space for one integer called `score`. It does not have a value yet.

### Declaring and assigning in one step

```c
int score = 0;
```

Now `score` starts with the value `0`.

---

## Common types in these labs

### `int` — integer

A whole number, positive or negative:

```c
int temperature = -5;
int level = 42;
```

### `unsigned` — non-negative integer

An integer that can only be zero or positive. Useful when you know a value (like a sensor reading) will never be negative:

```c
unsigned reading = 512;
```

---

## Updating a variable

You can assign a new value to a variable any time after it is declared:

```c
int score = 0;
score = 10;       // score is now 10
score = score + 5; // score is now 15
```

The right-hand side is evaluated first, then the result is stored in the variable on the left.

---

## Example: a simple counter

```c
int count = 0;

// ... later, inside loop() ...
count = count + 1;
printf("Count so far: %d\n", count);
```

This keeps a running count of how many times `loop()` has run. It has nothing to do with joysticks or motors — it's just a counter — but the same pattern applies anywhere you need to remember a value between iterations.

---

## See also

- [Printing with printf](printing-with-printf.md)
- [How a C program works](how-a-c-program-works.md)
- [analogRead()](../reference/analogread.md)
