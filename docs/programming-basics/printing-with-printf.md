---
tags:
  - printf
  - print
  - format
  - %d
  - output
---

# Printing with `printf`

`printf` (short for "print formatted") prints text to the terminal. It is the main way your program communicates what is happening.

---

## Basic usage

```c
printf("Hello!\n");
```

This prints `Hello!` followed by a new line. The `\n` is the **newline character** — it moves the cursor to the next line, just like pressing Enter. Without it, the next output would appear right after `Hello!` on the same line.

---

## Format specifiers

`printf` can insert values into the output using **format specifiers** — placeholders starting with `%`.

### `%d` — print an integer

```c
int laps = 7;
printf("Laps completed: %d\n", laps);
```

Output:
```
Laps completed: 7
```

The `%d` is replaced by the value of `laps` when the line runs.

### `%4d` — print an integer, at least 4 digits wide

```c
int laps = 7;
printf("Laps: %4d\n", laps);
```

Output:
```
Laps:    7
```

The `4` is the minimum field width. If the number is shorter than 4 digits, spaces are added on the left to pad it out. This keeps columns aligned when the value is changing:

```
Laps:    7
Laps:   18
Laps:  304
```

Without `%4d`, the line width would jump around and be harder to read.

---

## Multiple values in one line

You can have more than one `%d` in a format string. Add the corresponding variables after the format string, separated by commas, in the same order:

```c
int x = 3;
int y = 9;
printf("Position: x=%d, y=%d\n", x, y);
```

Output:
```
Position: x=3, y=9
```

---

## See also

- [Variables & types](variables-and-types.md)
- [How a C program works](how-a-c-program-works.md)
