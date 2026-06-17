---
tags:
  - educators
  - teachers
  - standards
  - alignment
---

# For Educators

This page is teacher-facing. Students do not need to read it — it is kept out of the main lab flow intentionally.

---

## Lab sequence

The recommended sequence is:

1. **Lab 1 · Count Your Instructions** — Introduces the terminal, file system navigation, and the concept of machine instructions. No hardware required. Sets up the prerequisite skills (terminal, `cd`, `ls`, `geany`) that Labs 2–4 depend on.
2. **Lab 2 · Analog Inputs** — Introduces the breadboard, MCP3008, joystick, and analog reading. Students wire the circuit and write their first sensor read.
3. **Lab 3 · Digital I/O & Motors** — Adds the L293 motor driver and the motor. Students configure pin modes and drive the motor with direction and speed control.
4. **Lab 4 · AI Inside & Out** — Connects the webcam and AI pipeline. Students discover what the `HandState` fields mean by experimenting, then use that data to control the motor.
5. **Bonus · LED Speedometer** — An open-ended extension for students who finish early or want a deeper challenge.

Labs 2–4 are cumulative: each builds directly on the hardware and code from the previous session.

---

## Standards alignment

The following alignment is drawn from the Lab 4 handout.

### NGSS (Next Generation Science Standards)

| Standard | Connection |
|---|---|
| HS-ETS1-2 | Design a solution to a complex real-world problem using engineering design principles |
| HS-ETS1-3 | Evaluate a solution to a complex real-world problem based on prioritized criteria and trade-offs |
| HS-PS3-3 | Design, build, and refine a device that works within given constraints to convert energy |

### CSTA (Computer Science Teachers Association)

| Standard | Connection |
|---|---|
| 3A-CS-01 | Explain how abstractions hide the underlying implementation details of computing systems |
| 3A-AP-13 | Create prototypes that use algorithms to solve computational problems |
| 3A-AP-17 | Decompose problems into smaller components through systematic analysis |
| 3B-IC-27 | Predict how computational innovations that have revolutionized aspects of our culture might evolve |

### ISTE (International Society for Technology in Education)

| Standard | Connection |
|---|---|
| 1.5 — Computational Thinker | Students decompose problems and extract key information to develop algorithmic solutions |
| 1.6 — Creative Communicator | Students use technology tools to create and share their work |
| 1.7 — Global Collaborator | Students use technology to work with others and solve problems |

---

## Raspberry Pi image setup

Refer to the `INSTALL.txt` file in the `Arenile/hotis-projects-starter` repository for instructions on setting up the Raspberry Pi image, installing the MemryX drivers, and configuring the camera pipeline.

---

## About this site

This site is intentionally a *reference*, not a walkthrough. Every page gives students the building blocks they need — function signatures, concept explanations, worked examples — but withholds the exact solution code for each lab step. The goal is that students consult this site the same way programmers use real documentation: look up what a function does, understand how it works, and apply it to their own situation.

The wiring diagram is provided inline (it is a given resource, not a puzzle). The hand-state field mappings are not provided (discovering them is Lab 4's core exercise). The Lab 1 instruction counts are not provided (students measure them with `perf stat`).
