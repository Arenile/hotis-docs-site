---
tags:
  - hand state
  - AI
  - get_handstate
  - HandState
  - Lab 4
  - machine learning
---

# Hand State (AI)

This page documents the AI interface — how your C program receives information about what your hands are doing.

---

## The `HandState` struct

A **struct** is a way to group related variables together under one name. The `HandState` struct holds four pieces of information about a hand:

```c
struct HandState {
    int x;      // a position
    int y;      // a position
    int theta;  // an angle
    int mag;    // a magnitude
};
```

- `x` and `y` describe position in **Cartesian** coordinates — the familiar (horizontal, vertical) grid.
- `theta` and `mag` describe a direction and size in **polar** coordinates — an angle and a distance from the origin. These are just two different mathematical ways to describe the same kind of information.

!!! note "Discover the mapping yourself"
    Lab 4 asks you to run the program and experiment — move your hand in different ways and observe what `theta`, `mag`, `x`, and `y` print. That exploration *is* the lab exercise. This page intentionally does not say which field maps to which hand motion. Fill in the table in your handout from your own observations.

---

## `get_handstate()`

```c
void get_handstate(FILE *fp, struct HandState *lHand, struct HandState *rHand);
```

### Parameters

| Parameter | Type | Description |
|---|---|---|
| `fp` | `FILE *` | The file pointer to the AI data stream — already set up for you, just pass it in |
| `lHand` | `struct HandState *` | Pointer to a `HandState` variable for the **left** hand |
| `rHand` | `struct HandState *` | Pointer to a `HandState` variable for the **right** hand |

### Usage

Declare two `HandState` variables, then call `get_handstate()` to fill them with the latest data:

```c
struct HandState lHand, rHand;
get_handstate(fp, &lHand, &rHand);
```

The `&` before a variable name means "the address of this variable" — it lets `get_handstate` write into your variables directly.

### Accessing fields

After the call, access individual fields with a dot:

```c
lHand.theta    // the theta value for the left hand
lHand.mag      // the magnitude value for the left hand
rHand.x        // the x value for the right hand
rHand.y        // the y value for the right hand
```

---

## Scaling for motor control

The motor speed ranges from 0 to `PWM_MAXVAL` (1024). Hand angles (`theta`) are roughly in the range −180 to 180 degrees. Those ranges do not match, so you will need to scale — see [Scaling numbers](../programming-basics/scaling-numbers.md).

---

## See also

- [Scaling numbers](../programming-basics/scaling-numbers.md)
- [Making decisions (if/else)](../programming-basics/making-decisions.md)
- [How the AI works](../concepts/how-the-ai-works.md)
- [Lab 4 · AI Inside & Out](../labs/lab-4-ai-inside-and-out.md)
