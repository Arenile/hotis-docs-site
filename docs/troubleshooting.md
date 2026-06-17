---
tags:
  - troubleshooting
  - errors
  - debugging
  - help
---

# Troubleshooting

Common problems and what to check. Solutions here stay at the "what to look at" level — working through the problem yourself is part of the learning.

---

## The program won't compile

**What you see:** `make` fails and prints error messages.

**What to do:**

1. Read the *first* error message — later errors are often caused by the first one.
2. Find the file name and line number in the error message (e.g., `joystick.c:14:`).
3. Open that file in Geany and look at that line number.
4. Common culprits: missing `;` at the end of a statement, unmatched `{` or `}`, a misspelled function or variable name.

→ [Reading error messages](getting-started/reading-errors.md)

---

## "Permission denied" when running

**What you see:** `./motor: Permission denied` or similar.

**What to do:** Try prefixing the command with `sudo`:

```
sudo ./motor
```

Some programs that control GPIO pins require administrator permissions. Your handout will say which programs need `sudo` — follow it exactly.

---

## Motor doesn't spin

**What to check:**

1. **Power supply** — Is the battery connected to the power supply board? Is the power supply switch on?
2. **Wiring** — Do your wires match the wiring diagram exactly? Check the L293 chip's orientation (the divot).
3. **Pin modes** — Did you call `pinMode()` for all three motor pins in `setup()`? If a pin is not configured, `pwmWrite()` and `digitalWrite()` will have no effect.
4. **Direction pins** — Are `L293_INPUT1` and `L293_INPUT2` set to *opposite* values? If both are `HIGH` or both are `LOW`, the motor brakes instead of spinning. → [The motor driver](concepts/motor-driver.md)
5. **Enable pin** — Is `L293_ENABLE` set to a non-zero value with `pwmWrite()`? A value of `0` means no power to the motor.

---

## Joystick reads garbage or one axis is stuck

**What to check:**

1. **Wiring** — Recheck the MCP3008 wiring against the diagram. One crossed wire is enough to break a channel.
2. **Chip orientation** — Is the MCP3008's divot facing the correct direction?
3. **Wrong channel** — Are you reading the correct ADC channel for the axis? `X_INPUT` (100) is the X axis. If Y always reads 0 and you want Y, you need to find the Y channel from the wiring diagram and read that instead.

→ [analogRead()](reference/analogread.md)

---

## Camera window doesn't open (Lab 4)

**What to check:**

1. **Webcam plugged in?** — Make sure the USB camera is connected before you run `./ai-motor`.
2. **Give it a few seconds** — The model takes a moment to load. Wait 5–10 seconds after running before you decide something is wrong.
3. **Run as a regular user** — `ai-motor` should typically be run without `sudo` unless your handout says otherwise. Try both and see.

---

## `git reset --hard` didn't fix it

`git reset --hard` only restores tracked files to the last committed version. If you accidentally deleted a file rather than edited it, or if you are outside the `hotis-projects-starter` directory, it may not behave as expected.

Make sure you are in `hotis-projects-starter`:

```
cd hotis-projects-starter
git reset --hard
```

→ [Resetting your work](getting-started/resetting-your-work.md)

---

## Something else is wrong

Ask your instructor. Describe what you tried, what you expected to happen, and what actually happened. Describing a problem out loud often helps you notice the answer yourself.
