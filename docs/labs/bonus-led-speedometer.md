---
tags:
  - bonus
  - LED Speedometer
  - LED
  - GPIO
  - binary
  - bit operators
  - digitalWrite
search:
  boost: 2
---

# Bonus · LED Motor Speedometer

Right now your joystick-controlled motor program prints the current speed to the terminal. This bonus project replaces that number with a visual speedometer built from LEDs.

The project is open-ended — there are two approaches, and you pick the one that appeals to you.

---

## Approach A — Threshold speedometer (easier, less precise)

Divide the maximum motor speed into 20% chunks. Use 5 LEDs. Light up one more LED for each 20% threshold you cross:

- 0–20%: 0 LEDs lit
- 20–40%: 1 LED lit
- 40–60%: 2 LEDs lit
- 60–80%: 3 LEDs lit
- 80–100%: 4 LEDs lit
- 100%: 5 LEDs lit

This is straightforward with `if/else if` logic. → [Making decisions (if/else)](../programming-basics/making-decisions.md)

---

## Approach B — Binary counter (harder, very precise)

Use N LEDs to display the motor speed as a binary number. Each LED represents one bit: lit = 1, off = 0. With 9 LEDs you can represent values from 0 to 511 exactly; with 10 LEDs, 0 to 1023.

This approach uses **bit shift operators** to read each bit of the speed value and translate it to an LED state. → [Bit operators](../programming-basics/bit-operators.md)

---

## What you need

- LEDs (ask your instructor how many, based on your chosen approach)
- Extra wires to connect each LED to a GPIO pin on the Pi

---

## Setting up the LEDs

### On the breadboard

Insert each LED so that:
- The **shorter leg** (cathode) goes into the blue ground rail
- The **longer leg** (anode) goes into a numbered row

You may need to bend the legs slightly to fit.

### Connecting to the Raspberry Pi

Run a wire from the numbered row (where the long leg is) to a GPIO pin on the Pi. **Any GPIO pin works** — look up "Raspberry Pi 5 pinout diagram" to find them. Write down which pin number you use for each LED, because you will need those numbers in your code.

---

## Driving an LED in code

There are two steps for each LED:

**In `setup()`:** Set the pin mode to `OUTPUT`.

**In `loop()`:** Write `HIGH` to turn the LED on, `LOW` to turn it off.

→ [pinMode()](../reference/pinmode.md) · [digitalWrite()](../reference/digitalwrite.md)

!!! question "Try it"
    Start by getting a single LED working: set its pin mode in `setup()`, then write `HIGH` to turn it on. Once that works, add a second LED, then the rest.

---

## For Approach B: bit operators

If you chose the binary counter approach, you will need to read individual bits of the speed value. The pattern is:

- Bit N of a value is set if `(value & (1 << N))` is non-zero.

Look into how that works before you start coding. → [Bit operators](../programming-basics/bit-operators.md)

---

## See also

- [digitalWrite()](../reference/digitalwrite.md)
- [pinMode()](../reference/pinmode.md)
- [Making decisions (if/else)](../programming-basics/making-decisions.md)
- [Bit operators](../programming-basics/bit-operators.md)
- [Scaling numbers](../programming-basics/scaling-numbers.md)
