---
tags:
  - PWM
  - pulse width modulation
  - motor speed
  - duty cycle
---

# What is PWM?

**PWM** stands for Pulse-Width Modulation. It is a technique for delivering a controlled amount of power through a pin that can only be fully on or fully off.

---

## The problem it solves

A GPIO output pin is digital — it can only be `HIGH` or `LOW`. But you often want something in between. A motor at half speed, a light at half brightness. How do you get a partial value from a pin that can only be fully on or fully off?

---

## The solution: switch very fast

PWM works by switching the pin on and off extremely rapidly — hundreds or thousands of times per second. The key is the **duty cycle**: the percentage of each cycle the pin spends in the `HIGH` state.

```
100% duty cycle:   |‾‾‾‾‾‾‾‾‾‾|  (always on — full power)
 50% duty cycle:   |‾‾‾‾‾|_____| (on half, off half — half power)
 25% duty cycle:   |‾‾|________| (on quarter, off three-quarters)
  0% duty cycle:   |___________| (always off — no power)
```

Because the switching happens faster than the motor or LED can respond, the device "sees" an average power level — as if the pin were outputting a steady voltage somewhere between 0 and full.

---

## PWM values in wiringPi

`pwmWrite()` accepts a value from 0 to 1024:

| Value | Duty cycle | Delivered power |
|---|---|---|
| 0 | 0% | None |
| 256 | ~25% | Quarter power |
| 512 | ~50% | Half power |
| 1024 | 100% | Full power |

The value 1024 is 2¹⁰ — a round number in binary, since the PWM hardware counts in powers of two.

---

## See also

- [pwmWrite()](../reference/pwmwrite.md)
- [Analog vs digital](analog-vs-digital.md)
- [The motor driver](motor-driver.md)
- [Pins & constants](../reference/pins-and-constants.md)
