---
tags:
  - hardware
  - Raspberry Pi
  - breadboard
  - MCP3008
  - L293
  - joystick
  - motor
  - fan
  - webcam
  - AI accelerator
  - HOTIS
---

# Your Toolkit

This page is a tour of the hardware you are working with — what each piece *is* and what it *does*. Wiring details live in the wiring diagram (see Labs 2–4).

**HOTIS** stands for *Hands-On Trainings In Semiconductors*, a University of Michigan program. That is where these labs come from.

---

## Raspberry Pi

The Raspberry Pi is a small, inexpensive computer — about the size of a credit card. It runs Linux, can run Python and C programs, and has a row of programmable pins along one edge called **GPIO** (General Purpose Input/Output) pins. Those pins are how it talks to the rest of the hardware on the breadboard.

---

## Breadboard

The breadboard is a plastic board with a grid of holes. Chips and wires plug directly into the holes. Think of it as an extension for a chip's pins — it holds wires in place so they don't fall off every time the board gets bumped. Internally, the holes in each short row are connected together, and the blue and red rails along the edges are connected end-to-end (ground and power, respectively).

!!! warning "Chip orientation matters"
    Both the MCP3008 and L293 chips have a small semi-circular divot on one end. That divot marks which way the chip is supposed to face. If you seat it backwards, things won't work — and may get damaged. Always check the orientation before pressing a chip in.

---

## MCP3008 — The ADC chip

The MCP3008 is an **Analog-to-Digital Converter** (ADC). The Raspberry Pi's GPIO pins can only read digital signals (0 or 1), but the joystick outputs a continuously varying voltage. The MCP3008 sits between the joystick and the Pi, measuring that voltage and converting it into a number your program can use. See [What is an ADC?](../concepts/what-is-an-adc.md) for a fuller explanation.

---

## L293 — The motor driver chip

The Raspberry Pi's GPIO pins can output only a tiny amount of current — nowhere near enough to spin a motor. The L293 is a **motor driver** that acts as an amplifier: it takes a small control signal from the Pi and uses the external power supply to drive the motor. It also lets you control which direction the motor spins. See [The motor driver](../concepts/motor-driver.md) for details.

---

## Joystick

The joystick module outputs two voltages — one for the X axis and one for the Y axis — that change as you push the stick around. Those voltages go through the MCP3008, which converts them into numbers from 0 to 1023 that your C program reads with `analogRead()`.

---

## DC Motor and fan blade

The DC motor is a small electric motor. In this lab, it has a **fan blade** attached to its shaft, so when the motor spins, the fan spins with it. In your code you will see it referred to as "the motor" — that matches what the code and the handout call it.

---

## Webcam

A standard USB webcam captures video frames. In Lab 4, those frames are fed into the AI pipeline.

---

## MemryX AI accelerator

The MemryX is a small chip that runs machine learning models much faster than a general CPU can. In Lab 4 it runs the MediaPipe hand-tracking model on every webcam frame. See [How the AI works](../concepts/how-the-ai-works.md) for the full pipeline.

---

## The wiring diagram

The wiring diagram is the single source of truth for how all of this connects together. You will use it in Labs 2, 3, and 4.

<div class="wiring-diagram">
![HOTIS Joystick and Fan Wiring Diagram](../assets/images/wiring-diagram-1.png)
</div>

[Download the full PDF](../assets/images/wiring-diagram.pdf){ .md-button }

## See also

- [Analog vs digital](../concepts/analog-vs-digital.md)
- [What is an ADC?](../concepts/what-is-an-adc.md)
- [The motor driver](../concepts/motor-driver.md)
- [Pins & constants](../reference/pins-and-constants.md)
