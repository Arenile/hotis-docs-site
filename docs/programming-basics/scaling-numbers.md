---
tags:
  - scaling
  - mapping
  - range
  - math
  - map
---

# Scaling Numbers

Sensors and actuators often speak different number ranges. A sensor might output values from 0 to 1023 while the thing you are driving only accepts 0 to 100. **Scaling** (also called *mapping*) is the math that converts a value from one range into the equivalent value in another range.

---

## The general formula

```
out = (value - inMin) * (outMax - outMin) / (inMax - inMin) + outMin
```

Where:

| Variable | Meaning |
|---|---|
| `value` | the input value you want to convert |
| `inMin`, `inMax` | the range the input comes from |
| `outMin`, `outMax` | the range you want the output in |
| `out` | the result |

---

## Worked example: temperature to percentage

Suppose a temperature sensor gives you values from −20 to 60 (degrees Celsius), and you want to display it as a 0–100% reading where −20 = 0% and 60 = 100%.

```c
int temp = 20;        // current reading from sensor
int inMin = -20;
int inMax = 60;
int outMin = 0;
int outMax = 100;

int percent = (temp - inMin) * (outMax - outMin) / (inMax - inMin) + outMin;
// percent == 50
```

Check: 20 is exactly halfway between −20 and 60, so 50% is correct.

---

## Integer division truncates

In C, dividing two integers drops the remainder:

```c
int result = 7 / 2;   // result is 3, not 3.5
```

If you need fractional results during the calculation, cast one operand to a float and convert back at the end, or multiply before dividing when possible:

```c
int result = (value - inMin) * (outMax - outMin) / (inMax - inMin) + outMin;
```

Multiplying before dividing keeps more precision in integer math.

---

!!! question "Try it"
    Think about this: if an input ranges from 0 to 1023 and the output ranges from 0 to 1024, what formula would convert an input of 512 to the correct output? Work it out by hand using the formula above before you write any code.

---

## See also

- [Variables & types](variables-and-types.md)
- [analogRead()](../reference/analogread.md)
- [pwmWrite()](../reference/pwmwrite.md)
- [Hand state (AI)](../reference/hand-state.md)
