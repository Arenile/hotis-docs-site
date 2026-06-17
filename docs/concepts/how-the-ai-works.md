---
tags:
  - AI
  - machine learning
  - MediaPipe
  - MemryX
  - hand tracking
  - webcam
  - Lab 4
---

# How the AI Works

Lab 4 is called "AI Inside and Out." This page explains what the AI is actually doing — the pipeline from camera to your C program.

---

## The pipeline

```
Webcam
  ↓  (video frames)
MediaPipe hand-tracking model
  ↓  runs on the MemryX AI accelerator
  ↓  (hand landmarks — coordinates of joints)
get_handstate()
  ↓  (HandState struct — x, y, theta, mag)
Your C program
  ↓
Motor commands
```

Here is each stage in detail.

---

## 1. The webcam captures frames

A standard USB webcam records video. Video is just a rapid sequence of still images called **frames** — typically 30 or more per second. Each frame is an array of pixel color values.

---

## 2. MediaPipe detects your hand

**MediaPipe** is a library developed by Google for real-time video analysis. One of its pre-trained models, the hand tracker, looks at each video frame and identifies the positions of 21 **landmarks** — key points like fingertips, knuckles, and the base of the palm.

Detecting these landmarks is a machine learning task. The model was trained on a huge dataset of labeled hand images. After training, it learned to recognize the pattern of a hand in a new image it has never seen before — even if the lighting, angle, or skin tone are different. This is what "machine learning" means: the model learned a skill from data, not from being programmed with explicit rules.

---

## 3. The MemryX accelerator speeds it up

Running a machine learning model is computationally expensive — it involves millions of arithmetic operations per frame. The **MemryX** is a specialized chip designed to perform exactly these operations very efficiently, much faster than a general-purpose CPU could.

Without the MemryX, running MediaPipe hand-tracking on every video frame would be too slow to be useful in real time.

---

## 4. `get_handstate()` delivers the data

The provided code in `core.c` manages the camera, runs the MediaPipe model via the MemryX, and streams the hand position data into your program. You access that data through `get_handstate()`, which fills in a `HandState` struct with four values for each hand: `x`, `y`, `theta`, and `mag`.

Your job in Lab 4 is to decide what those values mean (by experimenting) and then use them to control the motor.

---

## Hard-coded vs AI-driven

Your Lab 3 motor program always does the same thing every time it runs. The code determines the behavior completely. This is called **hard-coded** behavior.

In Lab 4, the *environment* — specifically, the position of your hand in front of the camera — changes the motor's behavior without changing the code. The AI reads the environment and feeds data into your program, which makes decisions based on that data. The same code, running on a different day with different hand movements, produces different results.

That is the core idea behind AI-driven systems: instead of programming every behavior explicitly, you let the system respond to what it observes.

---

## See also

- [Hand state (AI)](../reference/hand-state.md)
- [Lab 4 · AI Inside & Out](../labs/lab-4-ai-inside-and-out.md)
- [Your toolkit](../getting-started/orientation.md)
