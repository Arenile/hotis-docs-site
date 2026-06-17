---
tags:
  - delay
  - reference
  - pause
  - timing
---

# `delay()`

Pauses the program for a specified number of milliseconds.

---

## Signature

```c
void delay(unsigned int ms);
```

### Parameters

| Parameter | Type | Description |
|---|---|---|
| `ms` | `unsigned int` | Duration to pause, in milliseconds |

### Return value

None (`void`).

---

## Milliseconds

One second = 1000 milliseconds. Common values:

| Call | Pause duration |
|---|---|
| `delay(100)` | 0.1 seconds |
| `delay(500)` | 0.5 seconds (half a second) |
| `delay(1000)` | 1 second |
| `delay(5000)` | 5 seconds |

---

## Example

Blinking a light: on for one second, off for one second:

```c
void loop(void) {
    digitalWrite(18, HIGH);
    delay(1000);
    digitalWrite(18, LOW);
    delay(1000);
}
```

---

## See also

- [digitalWrite()](digitalwrite.md)
- [pwmWrite()](pwmwrite.md)
