---
tags:
  - pwmWrite
  - reference
  - PWM
  - motor speed
---

# `pwmWrite()`

Sets a PWM output pin to a value between 0 and 1024, controlling how much power is delivered. Use this with pins configured as `PWM_OUTPUT` with `pinMode()`.

---

## Signature

```c
void pwmWrite(int pin, int value);
```

### Parameters

| Parameter | Type | Description |
|---|---|---|
| `pin` | `int` | The PWM-capable pin number |
| `value` | `int` | Duty cycle, from `0` (off) to `1024` (full power) |

### Return value

None (`void`).

---

## Value range

| Value | Meaning |
|---|---|
| `0` | Off — no power delivered |
| `512` | Half power (50% duty cycle) |
| `1024` | Full power (100% duty cycle) |

Any integer between 0 and 1024 is valid.

---

## Example

Fading a light through three brightness levels:

```c
void loop(void) {
    pwmWrite(12, 256);    // 25% — dim
    delay(1000);
    pwmWrite(12, 512);    // 50% — medium
    delay(1000);
    pwmWrite(12, 1024);   // 100% — full brightness
    delay(1000);
}
```

---

!!! note "Why 1024 and not 100?"
    1024 is 2¹⁰ — a round number in binary. PWM hardware counts in powers of two, so the maximum is one step beyond 1023 (10-bit maximum). See [What is PWM?](../concepts/what-is-pwm.md) for the full explanation.

## See also

- [pinMode()](pinmode.md)
- [Pins & constants](pins-and-constants.md)
- [What is PWM?](../concepts/what-is-pwm.md)
- [Scaling numbers](../programming-basics/scaling-numbers.md)
