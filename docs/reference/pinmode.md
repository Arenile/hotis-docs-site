---
tags:
  - pinMode
  - reference
  - OUTPUT
  - PWM_OUTPUT
  - setup
---

# `pinMode()`

Sets a GPIO pin's mode — whether the program will use it for digital output or PWM output. Call this in `setup()`, once per pin, before using the pin.

---

## Signature

```c
void pinMode(int pin, int mode);
```

### Parameters

| Parameter | Type | Description |
|---|---|---|
| `pin` | `int` | The pin number (use a named constant from [Pins & constants](pins-and-constants.md)) |
| `mode` | `int` | One of `OUTPUT` or `PWM_OUTPUT` |

### Return value

None (`void`).

---

## Modes

| Mode | Use when… |
|---|---|
| `OUTPUT` | You will write `HIGH` or `LOW` to the pin with `digitalWrite()` |
| `PWM_OUTPUT` | You will write a value from 0 to 1024 with `pwmWrite()` |

---

## Example

Setting up two LEDs — one for on/off, one for variable brightness:

```c
void setup(void) {
    pinMode(18, OUTPUT);      // LED on pin 18: digital on/off
    pinMode(12, PWM_OUTPUT);  // LED on pin 12: variable brightness via PWM
}
```

Note: these pin numbers are arbitrary examples for illustration. The pins you use in the labs are defined as named constants in your `.c` file — always use those names, not bare numbers.

---

## See also

- [Pins & constants](pins-and-constants.md)
- [digitalWrite()](digitalwrite.md)
- [pwmWrite()](pwmwrite.md)
- [How a C program works](../programming-basics/how-a-c-program-works.md)
