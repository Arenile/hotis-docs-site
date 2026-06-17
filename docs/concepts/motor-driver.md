---
tags:
  - L293
  - motor driver
  - H-bridge
  - direction
  - enable
  - Lab 3
---

# The Motor Driver

The L293 is the chip that actually drives the motor. This page explains what it does and why it exists.

---

## Why a separate driver chip?

The Raspberry Pi's GPIO pins output only a tiny amount of current — enough to light an LED, but nowhere near enough to spin a motor. A motor needs far more current than the Pi can safely deliver.

The L293 acts as an amplifier and switch. It takes a small control signal from the Pi and uses power from the external power supply to drive the motor. Your Pi controls *what* happens; the L293 provides the *power* to make it happen.

---

## How direction works

The L293 has two input pins for direction control: `L293_INPUT1` and `L293_INPUT2`. The direction the motor spins depends on which pin is `HIGH` and which is `LOW`:

| `INPUT1` | `INPUT2` | Result |
|---|---|---|
| `HIGH` | `LOW` | Motor spins one direction |
| `LOW` | `HIGH` | Motor spins the other direction |
| `HIGH` | `HIGH` | Motor brakes (both inputs same = no differential) |
| `LOW` | `LOW` | Motor brakes |

The two pins must always be set to **opposite** values to make the motor spin. Think of it like a seesaw — one side goes up while the other goes down.

!!! question "Try it"
    If the motor is spinning in the wrong direction, what is the smallest change you could make to the two `digitalWrite()` calls to reverse it?

---

## How speed works

The `L293_ENABLE` pin is connected to a PWM output on the Pi. Writing a value from 0 to `PWM_MAXVAL` (1024) to this pin controls how much power the L293 delivers to the motor:

- `0` → motor off
- `1024` → full speed
- values in between → proportional speed

See [What is PWM?](what-is-pwm.md) for how PWM works.

---

## Summary

| Pin | Controls | Function |
|---|---|---|
| `L293_ENABLE` | Speed | PWM value 0–1024 |
| `L293_INPUT1` | Direction | Must be opposite of INPUT2 |
| `L293_INPUT2` | Direction | Must be opposite of INPUT1 |

---

## See also

- [Pins & constants](../reference/pins-and-constants.md)
- [pinMode()](../reference/pinmode.md)
- [digitalWrite()](../reference/digitalwrite.md)
- [pwmWrite()](../reference/pwmwrite.md)
- [What is PWM?](what-is-pwm.md)
