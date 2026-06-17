---
tags:
  - if
  - else
  - decisions
  - conditions
  - comparison
---

# Making Decisions (if / else)

Your program does not always have to do the same thing every time. An `if` statement lets you run a block of code only when a condition is true.

---

## `if`

```c
if (condition) {
    // code that runs when condition is true
}
```

The condition is an expression that evaluates to true or false. If it is true, the code inside the `{ }` runs. If it is false, that block is skipped entirely.

### Example

```c
int score = 85;

if (score >= 90) {
    printf("Grade: A\n");
}
```

Because `85 >= 90` is false, nothing is printed.

---

## `else`

`else` provides a block that runs when the `if` condition is false:

```c
int score = 85;

if (score >= 90) {
    printf("Grade: A\n");
}
else {
    printf("Grade: below A\n");
}
```

Exactly one of the two blocks will run, never both.

---

## `else if` — more than two cases

Chain multiple conditions with `else if`:

```c
int score = 85;

if (score >= 90) {
    printf("Grade: A\n");
}
else if (score >= 80) {
    printf("Grade: B\n");
}
else if (score >= 70) {
    printf("Grade: C\n");
}
else {
    printf("Grade: below C\n");
}
```

The conditions are checked top to bottom. The first one that is true runs its block, and the rest are skipped. With `score = 85`, the second condition (`>= 80`) matches and `Grade: B` is printed.

---

## Comparison operators

| Operator | Meaning |
|---|---|
| `==` | equal to |
| `!=` | not equal to |
| `<` | less than |
| `>` | greater than |
| `<=` | less than or equal to |
| `>=` | greater than or equal to |

!!! warning "= vs =="
    A single `=` **assigns** a value. A double `==` **compares** two values. Writing `if (x = 5)` instead of `if (x == 5)` is a classic C mistake — it assigns 5 to x instead of comparing.

---

## See also

- [Variables & types](variables-and-types.md)
- [Scaling numbers](scaling-numbers.md)
- [digitalWrite()](../reference/digitalwrite.md)
