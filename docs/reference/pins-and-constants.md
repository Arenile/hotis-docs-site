---
tags:
  - pins
  - constants
  - define
  - L293
  - PWM
  - joystick
---

# Pins & Constants

This page lists every `#define` constant used in the motor lab files and what it means. These are defined for you at the top of each `.c` file — you do not need to write them yourself.

---

## Motor pin constants

| Constant | Value | What it controls |
|---|---|---|
| `L293_ENABLE` | 26 | Motor **speed** — this is the PWM pin connected to the L293 enable input |
| `L293_INPUT1` | 21 | Motor **direction** pin A |
| `L293_INPUT2` | 22 | Motor **direction** pin B |
| `PWM_MAXVAL` | 1024 | Maximum PWM value — represents 100% motor speed |

### How the motor pins work together

`L293_ENABLE` controls how fast the motor spins (via PWM). `L293_INPUT1` and `L293_INPUT2` together control the direction. The two direction pins must always be set to **opposite** values — one `HIGH` and one `LOW`. See [The motor driver](../concepts/motor-driver.md) for details.

---

## Joystick constant

| Constant | Value | What it means |
|---|---|---|
| `X_INPUT` | 100 | The ADC channel for the joystick X axis (pinBase 100 via the MCP3008) |

---

## Logic level constants

These are defined by wiringPi and available in all the lab files:

| Constant | Value | Meaning |
|---|---|---|
| `HIGH` | 1 | Digital on (approximately 3.3 V on a GPIO pin) |
| `LOW` | 0 | Digital off (0 V) |

---

## Pin mode constants

| Constant | Meaning |
|---|---|
| `OUTPUT` | Pin is used for digital output (on/off) |
| `PWM_OUTPUT` | Pin is used for PWM output (variable power) |

---

## See also

- [pinMode()](pinmode.md)
- [digitalWrite()](digitalwrite.md)
- [pwmWrite()](pwmwrite.md)
- [analogRead()](analogread.md)
- [The motor driver](../concepts/motor-driver.md)
- [What is PWM?](../concepts/what-is-pwm.md)
