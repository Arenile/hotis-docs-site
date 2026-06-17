---
tags:
  - digitalWrite
  - reference
  - HIGH
  - LOW
  - digital output
---

# `digitalWrite()`

Sets a GPIO pin to either `HIGH` (on) or `LOW` (off). Use this with pins that have been configured as `OUTPUT` with `pinMode()`.

---

## Signature

```c
void digitalWrite(int pin, int value);
```

### Parameters

| Parameter | Type | Description |
|---|---|---|
| `pin` | `int` | The pin number to write to |
| `value` | `int` | `HIGH` (1) or `LOW` (0) |

### Return value

None (`void`).

---

## Example

Toggling an LED on pin 18 on and off with a one-second pause between:

```c
void loop(void) {
    digitalWrite(18, HIGH);   // LED on
    delay(1000);              // wait 1 second
    digitalWrite(LOW, 18);    // LED off  ← spot the bug?
    delay(1000);
}
```

!!! warning "Argument order matters"
    The pin number is always the **first** argument, the value is the **second**. Swapping them (`digitalWrite(LOW, 18)`) compiles without error but does the wrong thing — it tries to write to pin 0 and writes 18 as the value (which is treated as HIGH).

---

## See also

- [pinMode()](pinmode.md)
- [Pins & constants](pins-and-constants.md)
- [delay()](delay.md)
- [The motor driver](../concepts/motor-driver.md)
