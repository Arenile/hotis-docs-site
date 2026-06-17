---
tags:
  - ADC
  - analog to digital
  - MCP3008
  - 10-bit
  - joystick
---

# What is an ADC?

An **ADC** (Analog-to-Digital Converter) translates a continuously-varying analog voltage into a discrete number a computer can work with.

---

## The problem

Microcontrollers and computers are digital — they work with 1s and 0s. A joystick, however, outputs a voltage that slides continuously between its minimum and maximum as you push the stick. A digital GPIO pin can only tell you whether that voltage is above or below a threshold (on or off) — it cannot tell you *how far* you have pushed the joystick.

---

## How an ADC solves it

An ADC samples the voltage many times per second and converts each sample into a number. The precision of that number depends on how many bits the ADC uses.

### 10-bit resolution

The MCP3008 used in these labs is a **10-bit** ADC. That means it divides the full voltage range into 2¹⁰ = 1024 equal steps, numbered 0 through 1023:

- `0` → minimum voltage (joystick all the way to one end)
- `1023` → maximum voltage (joystick all the way to the other end)
- `511` → roughly the middle (joystick centered)

More bits means finer resolution. A 12-bit ADC would give you 4096 steps; an 8-bit gives only 256.

---

## The MCP3008 in your circuit

The MCP3008 sits on the breadboard between the joystick and the Raspberry Pi. It reads the analog voltage from the joystick and sends a digital number to the Pi over a communication protocol called SPI. The `mcp3004Setup()` call in your `setup()` function configures this connection and assigns a pin number to each channel so you can call `analogRead()` on it.

---

## See also

- [analogRead()](../reference/analogread.md)
- [Analog vs digital](analog-vs-digital.md)
- [Your toolkit](../getting-started/orientation.md)
