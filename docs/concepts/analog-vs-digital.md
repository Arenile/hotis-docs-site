---
tags:
  - analog
  - digital
  - signal
  - joystick
  - LED
---

# Analog vs Digital

Almost every sensor and output device you will encounter falls into one of two categories: **analog** or **digital**. Understanding the difference helps you know what kind of function to use.

---

## Digital signals

A digital signal has only two possible states: **on** or **off** (often written as `1` or `0`, `HIGH` or `LOW`).

**Examples:**
- An LED: it is either lit up or not.
- A push button: it is either pressed or not.
- A motor direction pin: it is set to spin one way or the other.

You work with digital signals using `pinMode(pin, OUTPUT)` and `digitalWrite(pin, HIGH)` or `digitalWrite(pin, LOW)`.

---

## Analog signals

An analog signal is **continuous** — it can take any value across a smooth range, not just on or off.

**Examples:**
- A joystick: as you push it, the output voltage slides continuously from low to high.
- A microphone: the voltage follows the sound wave, changing smoothly thousands of times per second.
- A temperature sensor: outputs a voltage that rises and falls with temperature.

You cannot plug an analog signal directly into a digital GPIO pin because the pin can only understand on or off. That is why the labs use the MCP3008 chip — an Analog-to-Digital Converter. See [What is an ADC?](what-is-an-adc.md).

---

## Why this matters

When you look at a sensor or output in a circuit, ask yourself: does it have two states, or does it vary continuously?

- Two states → digital → `digitalWrite()`
- Continuously varying → analog → `analogRead()` (for input) or PWM (for output)

---

## See also

- [What is an ADC?](what-is-an-adc.md)
- [What is PWM?](what-is-pwm.md)
- [analogRead()](../reference/analogread.md)
- [digitalWrite()](../reference/digitalwrite.md)
