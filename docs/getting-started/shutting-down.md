---
tags:
  - shutdown
  - power off
  - safety
---

# Shutting Down Safely

At the end of every session, shut down the Raspberry Pi properly before you unplug anything.

---

## The command

In the terminal, type:

```
shutdown now
```

The screen will go dark and the Pi will power off cleanly. Wait until the green activity LED on the board stops blinking before you unplug the power cable.

---

!!! warning "Never unplug the Pi while it is running"
    Yanking the power cable while the Pi is on can **corrupt the file system** — the same kind of damage that causes a "startup repair" screen on Windows, except the Pi does not have a repair tool. If that happens, the operating system may not boot and all your work could be lost.

    Always use `shutdown now` first.

---

## See also

- [Using the terminal](using-the-terminal.md)
