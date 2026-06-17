---
tags:
  - glossary
  - definitions
---

# Glossary

Plain-language definitions of every term used on this site.

---

**ADC (Analog-to-Digital Converter)**
A chip that converts a continuously-varying analog voltage into a discrete integer a computer can process. The MCP3008 in these labs is a 10-bit ADC with a range of 0–1023. → [What is an ADC?](concepts/what-is-an-adc.md)

**Analog signal**
A signal that varies continuously across a range — like the voltage output of a joystick as you push it around. Contrast with *digital signal*. → [Analog vs digital](concepts/analog-vs-digital.md)

**Assembly language**
A human-readable representation of machine instructions. `objdump -d` shows you assembly. Each line corresponds to one CPU operation.

**Binary**
A base-2 number system using only the digits 0 and 1. All data in a computer is stored and processed in binary. → [Bit operators](programming-basics/bit-operators.md)

**Bit**
A single binary digit — either 0 or 1. The smallest unit of data.

**Breadboard**
A plastic board with a grid of holes used to build circuits without soldering. Internally, the holes in each short row are connected, so plugging wires into the same row connects them. → [Your toolkit](getting-started/orientation.md)

**Compiler**
A program that translates source code (like C or C++) into machine instructions before the program runs. Contrast with *interpreter*. → [Compiled vs interpreted](concepts/compiled-vs-interpreted.md)

**C / C++**
Compiled, general-purpose programming languages. The motor labs use C. C++ is the same language with object-oriented extensions. Both compile to native machine code.

**Cartesian coordinates**
A way to describe a position using (x, y) values — horizontal and vertical distances from an origin point. One of the coordinate systems used in `HandState`.

**Compile**
To translate source code into machine instructions using a compiler. In these labs you compile with `make <target>`. → [Building & running](getting-started/build-and-run.md)

**Duty cycle**
In PWM, the fraction of each cycle the signal spends in the HIGH state. A 50% duty cycle means the signal is HIGH half the time. → [What is PWM?](concepts/what-is-pwm.md)

**Digital signal**
A signal with only two possible states: HIGH (on) or LOW (off). GPIO pins are digital. Contrast with *analog signal*. → [Analog vs digital](concepts/analog-vs-digital.md)

**Function**
A named, reusable block of code. `analogRead()`, `digitalWrite()`, `printf()` are all functions. You call a function by writing its name followed by parentheses (and any arguments).

**geany**
A simple code editor available on the Raspberry Pi. Open a file with `geany filename.c`. → [Opening & editing code](getting-started/editing-code.md)

**get_handstate()**
The function provided in `core.h` that retrieves the latest hand position data from the AI pipeline. → [Hand state (AI)](reference/hand-state.md)

**git**
A version control system that tracks changes to files. The starter code lives in a git repository. `git reset --hard` restores files to the original version. → [Resetting your work](getting-started/resetting-your-work.md)

**GPIO (General Purpose Input/Output)**
The row of programmable pins on the Raspberry Pi that can be set as digital inputs or outputs. "GPIO" is both the name of the pins and the concept.

**HandState**
A struct defined in `core.h` that holds four values describing one hand's position: `x`, `y`, `theta`, and `mag`. → [Hand state (AI)](reference/hand-state.md)

**HIGH**
A constant equal to 1, representing the "on" state for a digital GPIO pin (~3.3 V).

**HOTIS**
Hands-On Trainings In Semiconductors — the University of Michigan program that created these labs.

**Interpreter**
A program that reads and executes source code line by line at run time. Python uses an interpreter. Contrast with *compiler*. → [Compiled vs interpreted](concepts/compiled-vs-interpreted.md)

**L293**
The motor driver chip used in Labs 3 and 4. It takes small control signals from the Pi and provides enough current to drive the motor. → [The motor driver](concepts/motor-driver.md)

**LOW**
A constant equal to 0, representing the "off" state for a digital GPIO pin (0 V).

**Machine instruction**
One primitive operation executed directly by the CPU — add two numbers, move data, compare values, jump to another location. High-level language statements compile into many machine instructions. → [Compiled vs interpreted](concepts/compiled-vs-interpreted.md)

**make**
A build tool that compiles your program using rules defined in a `Makefile`. Run `make <target>` (e.g., `make joystick`) to compile. → [Building & running](getting-started/build-and-run.md)

**MCP3008**
The Analog-to-Digital Converter chip used in these labs. It reads the joystick's analog voltage and converts it to a 10-bit integer (0–1023). → [What is an ADC?](concepts/what-is-an-adc.md)

**MediaPipe**
A library by Google for real-time video analysis. In Lab 4 it runs a hand-tracking model that detects the positions of hand landmarks in each webcam frame. → [How the AI works](concepts/how-the-ai-works.md)

**MemryX**
An AI accelerator chip that runs machine learning models much faster than a general-purpose CPU. Used in Lab 4 to run the MediaPipe hand-tracking model in real time. → [How the AI works](concepts/how-the-ai-works.md)

**Model (machine learning)**
A program that has been trained on data to recognize patterns. The hand-tracking model was trained on many images of hands so it can identify hand landmarks in new images it has never seen. → [How the AI works](concepts/how-the-ai-works.md)

**OUTPUT**
A `pinMode` mode constant. Set a pin to `OUTPUT` when you will use `digitalWrite()` to write `HIGH` or `LOW` to it.

**Parameter**
A value passed into a function when you call it. `analogRead(X_INPUT)` passes `X_INPUT` as the parameter.

**Polar coordinates**
A way to describe a direction and distance using an angle (`theta`) and a magnitude (`mag`) from an origin point. One of the coordinate systems used in `HandState`.

**PWM (Pulse-Width Modulation)**
A technique for delivering variable power through a digital pin by rapidly switching it on and off. The fraction of time the pin spends HIGH is the duty cycle. → [What is PWM?](concepts/what-is-pwm.md)

**PWM_OUTPUT**
A `pinMode` mode constant. Set a pin to `PWM_OUTPUT` when you will use `pwmWrite()` on it.

**Python**
An interpreted programming language. Lab 1 includes a Python counting program to compare with the C++ equivalent.

**Raspberry Pi**
A small single-board computer that runs Linux. These labs use a Raspberry Pi 5.

**Root / sudo**
Administrator-level permissions on Linux. Some programs that directly access hardware need root access. Prefix the command with `sudo` to run with those permissions. → [Building & running](getting-started/build-and-run.md)

**Struct**
A C construct that groups related variables together under one name. `HandState` is a struct with fields `x`, `y`, `theta`, and `mag`. Access fields with a dot: `lHand.theta`.

**Variable**
A named storage location in your program. You declare it with a type and a name, and you can read and write its value while the program runs. → [Variables & types](programming-basics/variables-and-types.md)
