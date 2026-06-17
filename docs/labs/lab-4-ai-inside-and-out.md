---
tags:
  - Lab 4
  - AI Inside and Out
  - AI
  - hand gesture
  - get_handstate
  - HandState
  - machine learning
  - motor
search:
  boost: 2
---

# Lab 4 · AI Inside & Out — Hand-Gesture Motor Control

So far your motor programs have been **hard-coded**: they always do the same thing no matter what is happening around them. This lab changes that. Instead of fixed instructions, the motor responds to your hand movements — detected by a camera and a machine learning model — without you changing a single line of code.

---

## Step 1 · Plug in the webcam

Connect the USB webcam to your Raspberry Pi before starting.

---

## Step 2 · Open the file

```
cd hotis-projects-starter
geany ai-motor.c
```

---

## Step 3 · Set up the motor pins

In the `setup()` function, you need the same three `pinMode()` calls you used in Lab 3. → [pinMode()](../reference/pinmode.md) · [Pins & constants](../reference/pins-and-constants.md)

---

## Step 4 · Understand the AI data

In `loop()` you will see a function call:

```c
get_handstate(fp, &lHand, &rHand);
```

This fills `lHand` and `rHand` with the latest data from the hand-tracking AI. Each `HandState` has four fields: `x`, `y`, `theta`, and `mag`.

→ See [Hand state (AI)](../reference/hand-state.md) for the full documentation on `get_handstate()` and how to access fields.

---

## Step 5 · Explore what the fields mean

Before you try to control the motor, run the program and watch what prints:

```
make ai-motor
./ai-motor
```

A webcam window will open. Hold up your left hand and move it around. Watch the terminal.

**Experiment:** The `printf` at the bottom of `loop()` prints one field — try swapping `theta` for `mag`, or `x`, or `y`. Recompile and run each time to see what changes.

### Your exploration table

Fill this in from your own observations (the table is in your paper handout too):

| Field | What it seems to measure | Range you observed |
|---|---|---|
| `lHand.theta` | | |
| `lHand.mag` | | |
| `lHand.x` | | |
| `lHand.y` | | |

!!! note "This table is yours to fill in"
    The answer is not written here — that is the point of this step. What you write in that table is your discovery from running the program and observing it.

---

## Step 6 · Control the motor with your hand

Now you know what the fields mean. Use that knowledge to write the `loop()` function so your hand controls the motor.

Some things to keep in mind:

**Speed scaling:** The motor accepts values from 0 to `PWM_MAXVAL` (1024). Hand angles (`theta`) are roughly in the range −180 to 180. Those ranges do not match directly — you will need to scale. → [Scaling numbers](../programming-basics/scaling-numbers.md) · [pwmWrite()](../reference/pwmwrite.md)

**Direction control:** The two direction pins must always be opposite (`HIGH`/`LOW`). You cannot set them proportionally — they are either one state or the other. You will need an `if/else` to decide which state based on some hand value. → [Making decisions (if/else)](../programming-basics/making-decisions.md) · [digitalWrite()](../reference/digitalwrite.md)

**You are the designer:** Which gesture controls speed? Which controls direction? The handout does not decide for you. Pick something that makes sense to you, try it, and adjust.

---

!!! question "What to try next"
    1. Can you control the motor *speed* with your hand? (Start here.)
    2. Once that works, can you control *both* speed and direction using different gestures?

---

## See also

- [Hand state (AI)](../reference/hand-state.md)
- [How the AI works](../concepts/how-the-ai-works.md)
- [Scaling numbers](../programming-basics/scaling-numbers.md)
- [Making decisions (if/else)](../programming-basics/making-decisions.md)
- [pwmWrite()](../reference/pwmwrite.md)
- [digitalWrite()](../reference/digitalwrite.md)
