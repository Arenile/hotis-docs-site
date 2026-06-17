---
tags:
  - errors
  - compiler
  - debugging
  - troubleshooting
---

# Reading Error Messages

Getting an error message is not a sign that something is catastrophically wrong. Every programmer reads error messages constantly — it is a normal part of writing code. The compiler is trying to help you.

---

## The format of a compiler error

When `make` fails, the compiler prints errors that look like this:

```
joystick.c:14:3: error: expected ';' before '}' token
```

Read it left to right:

| Part | Meaning |
|---|---|
| `joystick.c` | Which file the error is in |
| `14` | Which line number |
| `3` | Which column (character position) on that line |
| `error:` | This is a hard error — the program won't compile until it's fixed |
| `expected ';' before '}' token` | What the compiler expected to find |

Open the file in Geany, scroll to that line number, and look at what's there. The error is usually at or just before that spot.

---

## Common beginner errors

### Missing semicolon

C statements end with `;`. If you leave one out, the compiler gets confused about where the statement ends:

```
// Wrong — missing semicolon
int score = 10

// Right
int score = 10;
```

### Unmatched braces

Every `{` needs a matching `}`. If you open a block and forget to close it (or close it too early), the compiler reports an error somewhere after the mismatch — sometimes much later in the file.

### Typo in a name

C is case-sensitive. `analogread` and `analogRead` are different names. If you mistype a function name or variable name, the compiler says it is "undeclared."

---

## Reading a warning vs. an error

- **error** — the program will not compile until this is fixed.
- **warning** — the program compiles, but something looks suspicious. Warnings are often worth investigating.

When there are multiple errors, **fix the first one first**. One bug can cause a cascade of confusing messages after it.

---

!!! tip "You are not doing it wrong"
    Professional programmers deal with compiler errors every day. Reading the message carefully, finding the line, and figuring out what the compiler expected is a skill — and you are practicing it right now.

## See also

- [Building & running](build-and-run.md)
- [Troubleshooting](../troubleshooting.md)
