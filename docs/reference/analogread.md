---
tags:
  - analogRead
  - reference
  - joystick
  - ADC
  - MCP3008
---

# `analogRead()`

Reads the current value from an analog input channel and returns it as an integer from 0 to 1023.

---

## Signature

```c
int analogRead(int pin);
```

### Parameters

| Parameter | Type | Description |
|---|---|---|
| `pin` | `int` | The ADC channel to read from (e.g., `X_INPUT` for the joystick X axis) |

### Return value

An `int` between `0` and `1023`, representing the measured voltage as a 10-bit value.

- `0` corresponds to 0 V (minimum voltage).
- `1023` corresponds to the reference voltage (maximum voltage).

---

## How it works

The Raspberry Pi's GPIO pins cannot directly read analog voltages. An external chip called the MCP3008 (an **Analog-to-Digital Converter**, or ADC) reads the voltage and converts it to a digital number. The `mcp3004Setup()` call in `setup()` configures the MCP3008 and maps its channels to pin numbers starting at a base address. You do not need to call `mcp3004Setup()` yourself — it is already in the provided setup code.

After setup, you call `analogRead()` with the channel's pin number (e.g., `X_INPUT`, which equals 100) to get the current reading.

---

## Example

Reading a light sensor on ADC channel 101 and printing the value:

```c
unsigned lightLevel = analogRead(101);
printf("Light level: %4d\n", lightLevel);
```

Note: channel 101 is just an illustration. In the labs, use the named constants defined in your `.c` file — do not use bare numbers.

---

## See also

- [Pins & constants](pins-and-constants.md)
- [What is an ADC?](../concepts/what-is-an-adc.md)
- [Analog vs digital](../concepts/analog-vs-digital.md)
- [Scaling numbers](../programming-basics/scaling-numbers.md)
