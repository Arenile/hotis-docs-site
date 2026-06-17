---
tags:
  - geany
  - editor
  - edit code
---

# Opening & Editing Code

The labs use **Geany**, a simple text editor that understands code. You open it from the terminal.

---

## Opening a file

```
geany joystick.c
```

This opens the file `joystick.c` in Geany. The file must exist in your current directory — navigate there first with `cd` if needed (see [Using the terminal](using-the-terminal.md)).

You can open any `.c` file the same way:

```
geany motor.c
geany ai-motor.c
```

---

## Saving

**Ctrl + S** saves the file. The title bar shows an asterisk (`*`) next to the filename when there are unsaved changes. Make sure to save before you go back to the terminal.

---

## Closing

Close the Geany window normally when you are done. You can also have Geany open while you use the terminal — they are separate windows and do not interfere with each other.

---

!!! tip "Syntax highlighting"
    Geany colors different parts of the code — keywords, strings, numbers, and comments appear in different colors. This makes it much easier to spot typos like a missing `"` or a misspelled keyword.

## See also

- [Building & running](build-and-run.md)
- [Reading error messages](reading-errors.md)
