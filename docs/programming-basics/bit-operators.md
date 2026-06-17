---
tags:
  - bit operators
  - binary
  - shift
  - bitwise
  - bonus
---

# Bit Operators

???+ note "Advanced — bonus activity"
    This page is only needed for the [LED Speedometer bonus activity](../labs/bonus-led-speedometer.md). If you are working through Labs 1–4, you can skip it for now.

---

## Binary and bits

Every number stored in a computer is represented in **binary** — a sequence of 1s and 0s. Each digit is called a **bit**.

For example, the decimal number 13 in binary is `1101`:

| Bit position | 3 | 2 | 1 | 0 |
|---|---|---|---|---|
| Value | 1 | 1 | 0 | 1 |
| Place value (2ⁿ) | 8 | 4 | 2 | 1 |

`8 + 4 + 0 + 1 = 13`. Each position is worth a power of 2.

---

## Bit operators

### Left shift `<<`

```c
int x = 1 << 3;   // x == 8
```

`<<` shifts the bits of the left operand to the left by the number of positions given on the right. Shifting left by N is the same as multiplying by 2ⁿ.

`1` in binary is `0001`. Shift it left 3 → `1000` = 8.

### Right shift `>>`

```c
int x = 16 >> 2;  // x == 4
```

Shifts bits to the right. Shifting right by N is the same as dividing by 2ⁿ (integer division).

### Bitwise AND `&`

```c
int x = 13 & 4;   // x == 4
```

Compares each bit position. The result bit is 1 only if **both** input bits are 1.

```
  1101   (13)
& 0100   (4)
------
  0100   (4)
```

This is useful for reading a specific bit: `(value & (1 << n))` is non-zero if bit N is set, zero if it is not.

### Bitwise OR `|`

```c
int x = 9 | 4;    // x == 13
```

The result bit is 1 if **either** input bit is 1.

```
  1001   (9)
| 0100   (4)
------
  1101   (13)
```

---

## Reading bit N of a number

To check whether bit N of a value is 1:

```c
if (value & (1 << n)) {
    // bit n is set
}
```

This is the pattern used in the binary LED speedometer approach — each LED corresponds to one bit of the speed value.

---

!!! question "Try it"
    Pick a number between 0 and 31. Write it out in binary (5 bits). Which bits are set? Verify using the `&` and `<<` operators in your program by printing the result.

## See also

- [Variables & types](variables-and-types.md)
- [Bonus · LED Speedometer](../labs/bonus-led-speedometer.md)
