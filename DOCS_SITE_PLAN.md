# Build Plan — "HOTIS Projects" Student Documentation Site

A handoff spec for Claude Code. This describes a documentation website for a
high-school AI + electronics project (Raspberry Pi, joystick, motor, and a
camera-based hand-gesture AI). The audience is students in grades 9–12, **some
of whom have never written code before.**

The site is a *reference and concept guide* — a "field manual" the students
consult while working through paper lab handouts. It is **not** a walkthrough and
**not** an answer key. The whole point is that students find the building blocks
here and assemble the solution themselves, so they feel like real programmers.

---

## 0. Read this first — the one rule that governs everything

When you write any page, you are writing **documentation, not a solution.**

- ✅ DO explain how a tool/function/concept works in general, with a worked
  example that is *different* from the lab task.
- ✅ DO point students at the right reference page and ask guiding questions.
- ✅ DO give them every fact they need.
- ❌ DON'T paste the exact line(s) of code that solve a lab step.
- ❌ DON'T fill in tables or answers the handout asks students to complete
  themselves (notably the Lab 4 hand-state table — see §6.4).
- ❌ DON'T arrange a lab page as a copy-this-then-that recipe.

**Litmus test:** a student should be able to read a reference page, learn the
concept, and still have to *think* to apply it to their lab. If they could copy a
block verbatim and be done, the page is wrong.

Concrete example of the right altitude:

> The motor's direction is controlled by two pins that must always be set to
> *opposite* values. Use `digitalWrite()` to set them. Try it one way; if the
> motor spins the wrong direction, what's the smallest change that would flip it?

vs. the wrong altitude (do **not** write this):

> ```c
> digitalWrite(L293_INPUT1, LOW);
> digitalWrite(L293_INPUT2, HIGH);
> ```

The reference pages may show *generic* signatures and *unrelated* examples
(e.g. `pinMode()` demonstrated with an LED on some arbitrary pin). That's fine —
that's what real API docs do. Just never demonstrate with the specific lab answer.

---

## 1. Tech stack decision

**Use MkDocs with the Material for MkDocs theme.** Build it as a standard MkDocs
project (Markdown content + one `mkdocs.yml`) and deploy to GitHub Pages.

Why this is the right pick for this project:

- **Search is the killer feature and it's built in.** Material's search indexes
  every page title, every section heading, and body text, runs fully client-side
  (lunr.js), and works perfectly on static `github.io` hosting with zero external
  services. Type "joystick lab part 2" or "pwmWrite" and you jump straight there.
  This is exactly the behavior the project owner asked for.
- **Pure Markdown.** Easy to author and maintain by a non-web-developer; no React
  build to babysit.
- **Beginner-friendly reading experience.** Admonition callouts (note / tip /
  warning / "try it"), code blocks with copy buttons, content tabs, a light/dark
  toggle, and clean navigation — all out of the box.
- **Deploys to `github.io` in one command / one CI workflow.**

Runner-up (mention to the owner only if they ask): **Starlight (Astro) with
Pagefind** has comparably excellent search and is gorgeous, but it's a heavier,
React/Astro build that's more to maintain. MkDocs Material wins on
simplicity-for-the-maintainer here. Do not use Docsify (weaker search) or a bare
Jekyll theme (worse search + clunkier authoring).

### Versions / dependencies

Pin these in `requirements.txt`:

```
mkdocs-material
mkdocs-material[imaging]   # optional, for social cards; drop if it complicates CI
pymdown-extensions
```

(Let pip resolve current versions; Material pulls in MkDocs itself.)

---

## 2. Repository & file structure

Create this layout. One Markdown file per page; section folders mirror the nav.

```
.
├── mkdocs.yml
├── requirements.txt
├── README.md                      # how to run/build locally + deploy
├── .github/
│   └── workflows/
│       └── deploy.yml             # GitHub Actions → Pages
└── docs/
    ├── index.md                   # Welcome / how to use these docs
    ├── assets/
    │   ├── images/                # wiring diagram (from PDF → PNG), AI-pipeline diagram, hardware photos
    │   └── stylesheets/extra.css  # small theming tweaks
    ├── getting-started/
    │   ├── orientation.md         # your toolkit / the hardware
    │   ├── using-the-terminal.md  # open terminal + navigate (cd, cd .., ls -al)
    │   ├── exploring-your-system.md # lscpu, /proc/meminfo, df -h
    │   ├── editing-code.md
    │   ├── build-and-run.md
    │   ├── resetting-your-work.md
    │   ├── reading-errors.md
    │   └── shutting-down.md       # shutdown now + never-yank-power warning
    ├── programming-basics/
    │   ├── how-a-c-program-works.md
    │   ├── variables-and-types.md
    │   ├── printing-with-printf.md
    │   ├── making-decisions.md     # if / else if / else
    │   ├── scaling-numbers.md      # mapping one range to another (map pattern)
    │   └── bit-operators.md        # for the binary-LED bonus
    ├── reference/
    │   ├── pins-and-constants.md
    │   ├── pinmode.md
    │   ├── digitalwrite.md
    │   ├── pwmwrite.md
    │   ├── analogread.md
    │   ├── delay.md
    │   └── hand-state.md           # get_handstate + the HandState struct
    ├── concepts/
    │   ├── analog-vs-digital.md
    │   ├── what-is-pwm.md
    │   ├── what-is-an-adc.md
    │   ├── motor-driver.md
    │   ├── compiled-vs-interpreted.md  # machine instructions, Python vs C++ (Lab 1)
    │   └── how-the-ai-works.md
    ├── labs/
    │   ├── lab-1-count-your-instructions.md
    │   ├── lab-2-analog-inputs.md
    │   ├── lab-3-digital-io-and-motors.md
    │   ├── lab-4-ai-inside-and-out.md
    │   └── bonus-led-speedometer.md
    ├── glossary.md
    ├── troubleshooting.md
    └── for-educators.md            # standards alignment etc. (teacher-facing)
```

---

## 3. `mkdocs.yml` — starting configuration

Use this as the baseline. Set `site_url` once the owner confirms the repo name
(see §5 for user-page vs project-page).

```yaml
site_name: HOTIS Projects — Student Field Manual
site_description: A reference guide for the Raspberry Pi AI + motor labs.
site_url: https://USERNAME.github.io/REPO/   # update per §5
repo_url: https://github.com/Arenile/hotis-projects-starter
edit_uri: ""   # hide "edit this page" unless the owner wants it

theme:
  name: material
  features:
    - navigation.instant      # SPA-like fast nav
    - navigation.tracking
    - navigation.sections
    - navigation.top
    - navigation.indexes
    - toc.follow
    - search.suggest          # autocomplete in the search box
    - search.highlight        # highlight the matched term on the page
    - search.share
    - content.code.copy       # copy button on code blocks
    - content.tabs.link
  palette:
    - scheme: default
      primary: indigo
      accent: indigo
      toggle:
        icon: material/weather-sunny
        name: Switch to dark mode
    - scheme: slate
      primary: indigo
      accent: indigo
      toggle:
        icon: material/weather-night
        name: Switch to light mode
  icon:
    repo: fontawesome/brands/github

markdown_extensions:
  - admonition
  - pymdownx.details
  - pymdownx.superfences
  - pymdownx.tabbed:
      alternate_style: true
  - pymdownx.highlight:
      anchor_linenums: true
  - pymdownx.inlinehilite
  - pymdownx.snippets
  - attr_list
  - md_in_html
  - toc:
      permalink: true

plugins:
  - search:
      separator: '[\s\-,:!=\[\]()"`/]+|\.(?!\d)|&[lg]t;|(?!\b)(?=[A-Z][a-z])'
  - tags          # lets pages carry tags like "Lab 2", "motor", "joystick"

extra_css:
  - assets/stylesheets/extra.css

nav:
  - Home: index.md
  - Getting Started:
      - Your toolkit: getting-started/orientation.md
      - Using the terminal: getting-started/using-the-terminal.md
      - Exploring your system: getting-started/exploring-your-system.md
      - Opening & editing code: getting-started/editing-code.md
      - Building & running: getting-started/build-and-run.md
      - Resetting your work: getting-started/resetting-your-work.md
      - Reading error messages: getting-started/reading-errors.md
      - Shutting down safely: getting-started/shutting-down.md
  - Programming Basics:
      - How a C program works: programming-basics/how-a-c-program-works.md
      - Variables & types: programming-basics/variables-and-types.md
      - Printing with printf: programming-basics/printing-with-printf.md
      - Making decisions (if/else): programming-basics/making-decisions.md
      - Scaling numbers: programming-basics/scaling-numbers.md
      - Bit operators: programming-basics/bit-operators.md
  - Reference:
      - Pins & constants: reference/pins-and-constants.md
      - pinMode(): reference/pinmode.md
      - digitalWrite(): reference/digitalwrite.md
      - pwmWrite(): reference/pwmwrite.md
      - analogRead(): reference/analogread.md
      - delay(): reference/delay.md
      - Hand state (AI): reference/hand-state.md
  - Concepts:
      - Analog vs digital: concepts/analog-vs-digital.md
      - What is PWM?: concepts/what-is-pwm.md
      - What is an ADC?: concepts/what-is-an-adc.md
      - The motor driver: concepts/motor-driver.md
      - Compiled vs interpreted: concepts/compiled-vs-interpreted.md
      - How the AI works: concepts/how-the-ai-works.md
  - The Labs:
      - "Lab 1 · Count Your Instructions": labs/lab-1-count-your-instructions.md
      - "Lab 2 · Analog Inputs": labs/lab-2-analog-inputs.md
      - "Lab 3 · Digital I/O & Motors": labs/lab-3-digital-io-and-motors.md
      - "Lab 4 · AI Inside & Out": labs/lab-4-ai-inside-and-out.md
      - "Bonus · LED Speedometer": labs/bonus-led-speedometer.md
  - Glossary: glossary.md
  - Troubleshooting: troubleshooting.md
  - For Educators: for-educators.md
```

---

## 4. Making search match the handouts (important)

The owner specifically wants students to "search the name of the lab and the part
they're on." Material search indexes headings, so the structure of each lab page
is what makes this work. Follow these rules:

1. **Lab page titles carry both names + the lab number.** First H1 of each lab
   page, e.g. `# Lab 2 · Analog Inputs — Reading the Joystick`. That single line
   has to surface whether a student searches "Lab 2", "analog inputs", or
   "joystick".
2. **Use the handout's own section words as headings.** The handouts are
   organized into `Part 1: Setting up the hardware`, `Part 2: Programming…`, and
   numbered `Step` items. Mirror that wording in `##` / `###` headings so a search
   for "joystick part 2" or "motor step 3" lands on the right section.
3. **Add a `tags:` front-matter block** to each lab page with the searchable
   aliases, e.g.:
   ```yaml
   ---
   tags:
     - Lab 2
     - Analog Inputs
     - joystick
     - analogRead
   ---
   ```
4. **Boost the lab pages** so they rank above incidental mentions:
   ```yaml
   ---
   search:
     boost: 2
   ---
   ```
5. Reference pages should be titled by the exact function name (`# pwmWrite()`),
   so a student who half-remembers a function name finds it instantly.

---

## 5. Deployment to `github.io`

The owner is hosting on a personal `github.io` subdomain. Two cases — **ask which
one applies** (or detect from the repo name) before setting `site_url`:

- **User/organization page** — repo is named `USERNAME.github.io`. Site serves at
  `https://USERNAME.github.io/`. Set `site_url` to that root.
- **Project page** — any other repo name. Site serves at
  `https://USERNAME.github.io/REPO/`. Set `site_url` to include `/REPO/`.

Add this GitHub Actions workflow at `.github/workflows/deploy.yml` (the official
Material-recommended CI). In repo Settings → Pages, set the source to "GitHub
Actions."

```yaml
name: Deploy docs
on:
  push:
    branches: [main]
permissions:
  contents: read
  pages: write
  id-token: write
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
        with:
          python-version: '3.x'
      - run: pip install -r requirements.txt
      - run: mkdocs build --strict
      - uses: actions/upload-pages-artifact@v3
        with:
          path: site
  deploy:
    needs: build
    runs-on: ubuntu-latest
    environment:
      name: github-pages
    steps:
      - id: deployment
        uses: actions/deploy-pages@v4
```

In `README.md`, document the local loop: `pip install -r requirements.txt`, then
`mkdocs serve` (live preview at `http://127.0.0.1:8000`), then push to `main` to
publish.

---

## 6. Page-by-page content spec

For every page: open with a one-sentence "what this page is for," define jargon on
first use, prefer one worked example, and end reference/concept pages with a "See
also" linking related pages. Keep the §0 answer-withholding rule in force
everywhere. Reading level: ~9th grade — short sentences, concrete language,
explain before you abbreviate.

### 6.0 Source of truth — use these exact facts (do not invent)

These come from the starter repo (`Arenile/hotis-projects-starter`), the five lab
handouts (Labs 1–4 plus the LED bonus), and the official wiring diagram PDF. Get
every name, number, and signature right.

**Context:** "HOTIS" = *Hands-On Trainings In Semiconductors* (a University of
Michigan program). The DC motor in Labs 3–4 physically spins a **fan blade** —
mention this once in `orientation.md` so the "motor" feels concrete, but keep
"motor" as the primary term since that matches the code and handouts.

**Lab 1 files (NOT in the motor starter repo — they live elsewhere on the Pi
image):**

| File | What it is |
|---|---|
| `HOTIS-count-till-py.py` | A small Python counting program students run and inspect. |
| `HOTIS-count-till-cpp.cc` | The equivalent program written in C++. |
| `HOTIS-count-till-cpp.o` / `.out` | The compiled C++ object file / executable. |

Lab 1 is a *systems/architecture* lab, not a hardware build — it has no wiring and
doesn't touch the motor starter repo. Its job is to introduce the terminal and the
idea of machine instructions. See §6.6 and the new concept page §6.5.

**Lab 1 terminal commands to document (all real, keep them exact):**
`lscpu` (CPU info) · `cat /proc/meminfo` (memory) · `df -h` (storage) ·
`ls -al` (list all files) · `cd <dir>` / `cd ..` (navigate) ·
`geany <file>` (open in editor) · `objdump -d <file>.o` (disassemble to machine
instructions) · `python <file>.py <N>` and `./<file>.out <N>` (run) ·
`perf stat -e instructions:u <command>` (count machine instructions executed) ·
`shutdown now` (safe shutdown). ⚠️ Never unplug the Pi while it's on — it can
corrupt the file system.

**Files students edit (from the `hotis-projects-starter` repo — Labs 2–4):**

| File | Lab | What the student does |
|---|---|---|
| `joystick.c` | Lab 2 | Read & print a joystick value with `analogRead`. |
| `motor.c` | Lab 3 | Set motor pin modes; drive direction + speed. |
| `joymotor.c` | Lab 3 bonus | Reference example: joystick drives the motor (already complete in repo — use as a teaching reference, not something to paste). |
| `ai-motor.c` | Lab 4 | Use `get_handstate()` hand data to drive the motor. |
| `core.c` / `core.h` | — | Provided plumbing. Contains the hidden `main()`, `open_process`, `get_handstate`, and the `HandState` struct. Students don't edit these. |

**Pin constants (`#define`s in the .c files):**

| Name | Value | Meaning |
|---|---|---|
| `L293_ENABLE` | 26 | PWM pin — motor *speed*. |
| `L293_INPUT1` | 21 | Motor *direction* pin A. |
| `L293_INPUT2` | 22 | Motor *direction* pin B. |
| `PWM_MAXVAL` | 1024 | Full-speed PWM value (ratios are X/1024). |
| `X_INPUT` | 100 | Joystick X channel on the ADC (pinBase 100). |

**wiringPi functions students use (signatures to document):**

- `wiringPiSetup()` / `wiringPiSetupPinType(WPI_PIN_WPI)` — already in the
  provided `setup()`; mention but they don't call it themselves.
- `pinMode(pin, mode)` — modes seen: `OUTPUT`, `PWM_OUTPUT`.
- `digitalWrite(pin, value)` — values: `HIGH`, `LOW`.
- `pwmWrite(pin, value)` — value `0`–`1024`.
- `analogRead(pin)` — returns `0`–`1023` (10-bit ADC via the MCP3008). For the
  joystick X channel the pin is `X_INPUT` (100).
- `delay(ms)` — pause in milliseconds.
- `mcp3004Setup(pinBase, spiChannel)` — already in provided setup; explain only at
  a high level.

**The AI interface (from `core.h`):**

```c
struct HandState {
  int x, y;     // a position
  int theta;    // an angle
  int mag;      // a magnitude
};
void get_handstate(FILE *fp, struct HandState *lHand, struct HandState *rHand);
```

You may explain, conceptually, that `(x, y)` is a Cartesian position and
`(theta, mag)` is the polar form (angle + length) of the same kind of idea — that
is general math/CS knowledge. **But do not state which specific field corresponds
to which real-world hand motion** — Lab 4 has students discover that by running
the program and filling in a table. See §6.4.

**Build & run:** `make <target>` (e.g. `make joystick`), then run the binary
(`./joystick`; the motor labs use `sudo ./motor` etc. — some programs need root
for GPIO). Always tell students to follow the run command printed in their
handout for that lab.

**The wiring diagram (provided as `HOTIS_Joystick_Fan_Wiring_Diagram.pdf`):** this
is the single source of truth for hardware wiring in Labs 2–4. It shows the
joystick module (pins `GND`, `+5V`, `VRX`, `VRY`, `SW`), the MCP3008 and L293 chips
seated on the breadboard, the fan/motor, the power supply, and the labeled
Raspberry Pi header pins. **Embedding this diagram is expected and is NOT an
answer-withholding violation** — the handouts explicitly tell students to "connect
everything according to the wiring diagram." Wiring is a provided resource, not the
programming puzzle. Convert the PDF to a web image (PNG/SVG) for inline display and
also link the original PDF for download/zoom. Do **not** hand-transcribe a
pin-by-pin wiring table from the image — embed the authoritative diagram and let
students read it.

**Lab 1 (`Count Your Instructions`) is the real first lab** and replaces the old
placeholder. It also establishes the prerequisite skills Labs 2–4 lean on (opening
the terminal, `cd`, `ls`, `geany`). The terminal/navigation/shutdown skills it
teaches are written up as reusable `getting-started/` reference pages; the Lab 1
page itself (§6.6) mirrors the handout's Step structure and links to them. Open
question for the owner: where do the `HOTIS-count-till-*` files live on the Pi
(which directory / are they pre-installed on the image)? — see §10.

### 6.1 Home — `index.md`

Welcome + framing. State plainly: *this site is your field manual, not an answer
key.* Real programmers don't memorize everything — they look things up in docs and
piece solutions together, and that's exactly what you'll do here. Briefly orient
them to the three areas: **Getting Started** (tools), **Reference/Concepts** (look
things up), **The Labs** (guidance for each handout). Show how to use search.
Encouraging, plain-spoken tone.

### 6.2 Getting Started section

- **orientation.md** — "Your toolkit." Photo/diagram-friendly tour of the
  hardware: Raspberry Pi, breadboard (explain it as "an extension of the chips'
  pins so wires don't fall off" — language drawn from the handouts), the MCP3008
  (analog-to-digital chip), the L293 (motor driver), the joystick, the DC motor
  (note it spins a **fan blade**), and the webcam + AI accelerator. One paragraph
  each, what it's *for*, not how to wire it. Note the recurring handout warning:
  watch the orientation of the semicircular divot when seating a chip. Embed the
  wiring diagram here too (or link to it) as the "big picture" of how it connects.
  One line on what HOTIS stands for (Hands-On Trainings In Semiconductors).
- **using-the-terminal.md** — opening the terminal (the grey box with a white
  `>_`), the prompt, and **navigating the file system**: `ls -al` (list all
  files), `cd <dir>` to move in, `cd ..` to move up, and `cd hotis-projects-starter`
  for the build labs. This is introduced in Lab 1 and reused constantly afterward.
- **exploring-your-system.md** — the Lab 1 system-inspection commands as a quick
  reference: `lscpu` (what CPU you have), `cat /proc/meminfo` (memory), `df -h`
  (storage). Briefly say what each output means at a beginner level.
- **editing-code.md** — opening a file with `geany <filename>`, saving, closing.
- **build-and-run.md** — what "compiling" means in friendly terms, `make
  <target>`, running with `./<target>`, when/why `sudo` is needed, reading the
  "it built with no errors" success state. Also mention running a program *with an
  argument* (`./program <number>`), since Lab 1 passes a number to its programs.
- **resetting-your-work.md** — `git reset --hard`. ⚠️ Put a prominent **warning**
  admonition: this permanently discards your edits and restores the original
  starter file. Frame it as a "start this file over from scratch" button.
- **reading-errors.md** — the "feel like a real programmer" page. How to read a
  compiler error: it usually tells you the file, line number, and roughly what's
  wrong; common beginner errors (missing `;`, unmatched `{ }`, typo'd name).
  Encourage: every programmer reads error messages constantly; it's a skill, not a
  failure.
- **shutting-down.md** — how to power down safely with `shutdown now`, and a strong
  ⚠️ **warning** admonition: never unplug the Pi while it's running, because that
  can corrupt the file system (drawn straight from the Lab 1 handout). Short and
  prominent — students will look for this at the end of every session.

### 6.3 Programming Basics section

General C, taught with examples unrelated to the lab answers.

- **how-a-c-program-works.md** — `#include`, `#define` (use the repo's own
  comment analogy: `#define PI 3.14`), and the `setup()`-runs-once /
  `loop()`-runs-forever structure. Explain that `main()` lives in the provided
  `core.c` and calls these for them.
- **variables-and-types.md** — `int`, `unsigned`; declaring, assigning, reusing.
  Example with something neutral (a score counter), not a joystick read.
- **printing-with-printf.md** — `printf`, the `%d` / `%4d` format specifiers, and
  `\n`. Explain `%4d` = "print this number, at least 4 digits wide" and `\n` =
  newline. Use a neutral example.
- **making-decisions.md** — `if`, `else if`, `else`, and comparison operators
  (`<`, `>`, `==`). Use a neutral scenario (e.g. grading a score), **not** the
  motor-direction example from the Lab 4 handout. The students should transfer the
  pattern themselves.
- **scaling-numbers.md** — the most important building block. Teach the general
  idea of mapping a value from an input range to an output range — e.g. turning a
  0–1023 reading into a 0–100 percentage, or an angle into a speed. Present the
  general formula `out = (value - inMin) * (outMax - outMin) / (inMax - inMin) +
  outMin` and one neutral worked example. Students reuse this for joystick→speed
  and angle→speed without being handed those specific lines.
- **bit-operators.md** — for the binary-LED bonus. Explain `<<`, `>>`, `&`, `|`
  and "reading bit N of a number" generically. Keep it optional/advanced (use a
  `???+ note "Advanced"` collapsible).

### 6.4 Reference section ("the API docs")

Terse, accurate, real-docs feel. Each page: signature, parameters, return value,
one *neutral* example, "see also."

- **pins-and-constants.md** — table of the `#define`s from §6.0 with plain-English
  meanings, plus `HIGH`/`LOW`/`OUTPUT`/`PWM_OUTPUT`.
- **pinmode.md** — `pinMode(pin, mode)`; modes `OUTPUT` and `PWM_OUTPUT`; neutral
  example (an LED on an arbitrary pin).
- **digitalwrite.md** — `digitalWrite(pin, HIGH|LOW)`; neutral example.
- **pwmwrite.md** — `pwmWrite(pin, value)`, value `0`–`1024`; link to the PWM
  concept page.
- **analogread.md** — `analogRead(pin)` returns `0`–`1023`; note the MCP3008 ADC;
  link to the ADC concept page.
- **delay.md** — `delay(ms)`; short.
- **hand-state.md** — the AI interface. Show the `HandState` struct and the
  `get_handstate(fp, &lHand, &rHand)` call. Explain accessing a field with
  `lHand.theta`, `lHand.x`, etc. Explain Cartesian `(x,y)` vs polar `(theta,mag)`
  *as a math concept.* **Do NOT state which field maps to which real hand motion;
  point students to run the program and observe** (this is the Lab 4 discovery
  task). Mention motor speed max is 1024 and angles are roughly `[-180, 180]`, so
  some scaling is needed — link to `scaling-numbers.md`.

### 6.5 Concepts section (the "AI inside and out" depth)

Explainer pages that build intuition. Diagrams encouraged (put images in
`docs/assets/images/`).

- **analog-vs-digital.md** — continuous vs on/off signals; the joystick is analog,
  an LED is digital.
- **what-is-pwm.md** — how rapidly switching a pin on/off "fakes" partial power;
  why `pwmWrite` uses 0–1024.
- **what-is-an-adc.md** — why a digital computer needs the MCP3008 to read an
  analog joystick; where the 0–1023 range comes from (10-bit).
- **motor-driver.md** — what the L293 does; why the two direction pins must be
  opposite (one HIGH, one LOW); how ENABLE + PWM sets speed.
- **compiled-vs-interpreted.md** — the conceptual heart of Lab 1, age-appropriate.
  What a *machine instruction* is (the tiny steps a CPU actually runs); the
  difference between an *interpreted* language (Python — translated as it runs) and
  a *compiled* language (C/C++ — translated ahead of time into machine
  instructions); why the same task can take very different instruction counts in
  each. Explain what `objdump -d` shows (the machine instructions inside a compiled
  program) and what `perf stat -e instructions:u` measures (how many instructions
  actually ran). Tie it to the Lab 1 "who guessed closest?" game. Keep numbers
  open — let students discover that Python typically runs far more instructions
  than the C++ equivalent rather than stating a specific result. This page also
  quietly sets up *why* the later labs are written in C.
- **how-the-ai-works.md** — the headline "AI inside and out" story, age-appropriate
  and accurate: the webcam captures frames → a MediaPipe hand-tracking model runs
  on the MemryX AI accelerator → it finds the hand and reports its position/angle →
  that streams into your C program via `get_handstate()` → your code turns it into
  motor commands. Demystify ML at a high level (it's a trained pattern-recognizer,
  not magic) and connect to the "hard-coding vs. AI-driven behavior" framing the
  Lab 4 handout opens with. A simple pipeline diagram here is high value.

### 6.6 The Labs section (mirrors handouts, NO answers)

Each lab page mirrors its handout's Part/Step structure (for search), but each
step is reframed as *orientation + guiding questions + links to the reference*,
never the solution. Pull the exact wording of section headings from the handouts.
Use "Try it" admonitions for the challenges. Below, the spec per lab — the
parenthetical reference facts are for you, the builder; surface them as links, not
as pasted solutions.

- **lab-1-count-your-instructions.md** (Python & C++ counting programs; no wiring)
  - This is a *systems* lab, not a build — set expectations: today you explore what
    the computer is actually doing, no breadboard yet. Mirror the handout's Step
    structure for search.
  - Steps 1–6 (terminal + system inspection + navigation): reframe as "explore your
    machine." Link `using-the-terminal.md` and `exploring-your-system.md` for
    `lscpu`, `cat /proc/meminfo`, `df -h`, `ls -al`, `cd`, `cd ..`. Explain at a
    high level what each command tells you, not just the keystrokes.
  - Steps 7–8 (look at & run the programs): opening the Python and C++ source in
    `geany`; disassembling with `objdump -d` (link `compiled-vs-interpreted.md` to
    explain what the disassembly *is*); running each program with a number argument.
    The handout's "how many machine instructions do you think it ran?" is a **"Try
    it" guess** — present it as a prediction prompt, don't reveal a number.
  - Step 9 (count instructions): `perf stat -e instructions:u …` for both programs;
    frame the Python-vs-C++ comparison as the discovery, linking
    `compiled-vs-interpreted.md`. Let students find that the counts differ a lot;
    don't state the figures.
  - Step 10 (shut down): link `shutting-down.md` with the ⚠️ never-unplug warning.
  - Open question to surface gently (a `!!! note`): where the `HOTIS-count-till-*`
    files live, if the owner confirms a path (see §10).

- **lab-2-analog-inputs.md** (`joystick.c`)
  - Part 1 · Setting up the hardware: **embed the wiring diagram** (the converted
    PNG, with a link to the full PDF) as the primary reference; repeat the
    divot-orientation and MCP3008-placement cautions; explain the breadboard
    analogy. (Reset step: `git reset --hard` before editing — link
    resetting-your-work.md.)
  - Part 2 · Programming the joystick: the goal is read a value and print it.
    Link `analogRead()` and `printing-with-printf.md`. Ask: which constant names
    the joystick's X channel? Where does the read value need to go so you can
    print it? (Don't write the two lines.)
  - Bonus · "y always reads 0": frame as a mystery to solve. Hint (from handout):
    figure out which pin the y-wire is plugged into and read *that* channel. Link
    `analogread.md`. Don't reveal the channel number.

- **lab-3-digital-io-and-motors.md** (`motor.c`, plus `joymotor.c` as reference)
  - Part 1 · Hardware: two chips now (MCP3008 + L293), placement + divot caution,
    power supply, and the fan/motor. **Embed the wiring diagram** as the reference
    (same converted image as Lab 2; the diagram already shows both chips and the
    fan).
  - Part 2 · Setup function: students must set three pin modes — which pins are
    `OUTPUT` and which is `PWM_OUTPUT`? Link `pinmode.md` and
    `pins-and-constants.md`. Explain (concept) what ENABLE vs INPUT1/INPUT2 do via
    `motor-driver.md`. (Don't paste the three `pinMode` lines.)
  - Part 2 · Loop function: drive the motor with `digitalWrite` (direction) +
    `pwmWrite` (speed). Pose the handout's question: to reverse direction, what's
    the smallest change to the two direction writes? Mention `delay()`. Link the
    references. (Don't paste the loop body.)
  - Challenge (handout Step 5): "spin one way 5s, the other 5s, then settle at 60%
    forever." Present as a "Try it" challenge with pointers (you'll need `delay`,
    and a fraction of `PWM_MAXVAL` for 60%), not a solution.
  - Bonus · joystick → motor: explain conceptually how a joystick reading could
    set speed and direction; you may *reference* `joymotor.c` as a worked example
    that already exists in the repo for them to study, but don't reproduce it
    inline. Mention the handout's angle conversion only as "there's a way to turn
    the 0–1023 reading into an angle — see scaling-numbers."

- **lab-4-ai-inside-and-out.md** (`ai-motor.c`)
  - Open with the handout's hook: hard-coded behavior always does the same thing;
    AI lets the *environment* (your hand) change behavior without changing code.
  - Step-by-step framing mirrors the handout: plug in the webcam; set the motor
    pin modes (link Lab 3 / `pinmode.md`); use `get_handstate(fp, &lHand, &rHand)`
    (link `hand-state.md`); run it first to watch the printout.
  - **The exploration table:** the handout gives students a table to fill in
    describing what `theta`, `mag`, `x`, `y` mean for each hand, by editing the
    `printf` and observing. **Reproduce the table as empty/for-them-to-fill (or
    just link to their handout), and explicitly do NOT fill it in.** You may
    explain *how* to investigate (swap `theta` for `mag`/`x`/`y` in the `printf`
    and watch what changes) — that's method, not answer.
  - Mapping + control: motor speed maxes at 1024; hand angle is about [-180,180],
    so scaling is needed (link `scaling-numbers.md`); direction needs an
    `if/else` (link `making-decisions.md`). Pose it as "you're the designer —
    decide which gesture does what," echoing the handout. No solution code.
  - "What to try next" challenges from the handout (control speed with your hand;
    then both speed and direction) as "Try it" callouts.

- **bonus-led-speedometer.md**
  - Two approaches, exactly as the handout frames them: (a) easier/less precise —
    5 LEDs lighting in 20% thresholds; (b) harder/precise — a binary counter
    across N LEDs. Let students pick.
  - Wiring an LED (short leg → ground rail, long leg → a numbered row; wire to a
    GPIO pin). Tell them to look up a "Raspberry Pi 5 pinout diagram" and use any
    GPIO pin, recording the number.
  - Driving an LED: `pinMode(pin, OUTPUT)` then `digitalWrite(pin, HIGH/LOW)` —
    link the references with a neutral example. For approach (b), link
    `bit-operators.md` and frame bit-shifting as the thing to research. Keep it
    open-ended; no full solution.

### 6.7 Glossary — `glossary.md`

Plain-language definitions of every term used on the site: breadboard, GPIO, ADC,
PWM, compile, function, variable, parameter, struct, `HIGH`/`LOW`, analog,
digital, machine learning model, MediaPipe, MemryX, etc. Alphabetical. Link terms
from other pages here on first use where practical.

### 6.8 Troubleshooting — `troubleshooting.md`

Common failure modes as a FAQ: program won't compile (read the first error;
missing `;` / brace / typo — link reading-errors.md); "permission denied" when
running (try `sudo`); motor doesn't spin (power supply? direction pins both set?
ENABLE driven?); joystick reads garbage or one axis stuck (wiring / wrong
channel); camera window doesn't open (webcam plugged in? give it a few seconds).
Solutions stay at the "what to check" level, consistent with §0.

### 6.9 For Educators — `for-educators.md`

Teacher-facing, kept out of the student flow. Include the **Standards Alignment**
tables from the Lab 4 handout (NGSS / CSTA / ISTE), a note on the lab sequence
(2 → 3 → 4 → bonus), and a pointer to the repo's `INSTALL.txt` for Raspberry Pi /
MemryX setup. This is the one place answer-y teacher content can live; still don't
post student solution code.

---

## 7. Style & voice guide (apply to every page)

- **Audience:** 9th–12th grade, possibly zero programming background. Encouraging,
  never condescending. "You can do this; here's how to find out."
- **Define before you abbreviate.** First use of any acronym gets expanded.
- **Short sentences, concrete nouns, active voice.**
- **One idea per page; one worked example per concept.** Examples must be neutral
  (not the lab solution).
- **Use admonitions deliberately:** `!!! note` for context, `!!! tip` for shortcuts,
  `!!! warning` for footguns (e.g. `git reset --hard`, `sudo`), and a custom
  `!!! question "Try it"` style for challenges. Define the "Try it" admonition in
  `extra.css` if you want it visually distinct.
- **Code blocks** are for *generic* syntax and signatures only, never lab answers.
- **Cross-link generously** — every lab step should link out to the reference and
  concept pages it depends on. That linking *is* the "piece it together"
  experience.
- **Keep the real-programmer framing** subtly present: reading docs, reading
  errors, looking up functions, designing your own approach — name these as the
  things real programmers actually do.

---

## 8. Build order for Claude Code

1. Scaffold the repo, `mkdocs.yml`, `requirements.txt`, `extra.css`, and the GH
   Actions workflow. Confirm `mkdocs serve` runs and the nav renders with stub
   pages.
2. Confirm with the owner: user-page vs project-page repo (sets `site_url`), and
   the location of the `HOTIS-count-till-*` Lab 1 files on the Pi (for accuracy of
   the Lab 1 page).
3. Convert `HOTIS_Joystick_Fan_Wiring_Diagram.pdf` to a web image (PNG at high
   resolution, or SVG) and place it in `docs/assets/images/`; keep the original PDF
   in the repo and link it for download/zoom.
4. Write **Getting Started** and **Programming Basics** (the foundation everything
   links to).
5. Write the **Reference** and **Concepts** pages (the link targets), including the
   new `compiled-vs-interpreted.md`.
6. Write the **Labs** pages last (Lab 1 → bonus), wiring their guiding questions to
   the reference links and embedding the wiring diagram in the hardware sections.
7. Write Glossary, Troubleshooting, For Educators.
8. Add the AI-pipeline diagram and any hardware photos to `docs/assets/images/`
   (owner to supply photos if wanted; leave captioned placeholders otherwise).
9. Run `mkdocs build --strict` (catches broken links/nav), fix, then push to
   `main` to deploy.

---

## 9. Acceptance criteria (definition of done)

- [ ] `mkdocs build --strict` passes with no warnings (no broken internal links).
- [ ] Site deploys to the correct `github.io` URL and search works on the live
      site.
- [ ] Searching "Lab 1" / "Lab 2" / "analog inputs" / "joystick" each reach the
      right lab page; same pattern holds for Labs 3, 4, and the bonus.
- [ ] Searching a function name (`pwmWrite`, `analogRead`, `get_handstate`) reaches
      its reference page.
- [ ] **No page contains the exact solution code for any lab step.** Spot-check all
      five lab pages against §0.
- [ ] The Lab 4 hand-state table is left for students to fill in (not answered);
      Lab 1 instruction-count figures are likewise left for students to discover.
- [ ] The wiring diagram renders inline on the Lab 2/3 hardware sections, and the
      original PDF is downloadable.
- [ ] Every acronym is expanded on first use; the glossary covers all jargon.
- [ ] Every lab step links to at least one reference or concept page.
- [ ] All pin names, constants, value ranges, and function signatures match §6.0
      exactly.
- [ ] Light/dark toggle, code-copy buttons, and mobile layout all work.

---

## 10. Notes / open questions for the owner

- **Lab 1 program files:** the `HOTIS-count-till-py.py` / `.cc` / `.o` / `.out`
  files are referenced by the Lab 1 handout but are **not** in the
  `hotis-projects-starter` repo — they live somewhere else on the Pi image.
  Confirm the directory (and whether they ship pre-installed) so the Lab 1 page can
  tell students exactly where to `cd`.
- **Wiring diagram:** now provided (`HOTIS_Joystick_Fan_Wiring_Diagram.pdf`).
  Convert to PNG/SVG for inline display and keep the PDF for download (see §8 step
  3). This is the authoritative hardware reference for Labs 2–4.
- **`sudo` vs not:** handouts are inconsistent (`./joystick` and `./ai-motor` but
  `sudo ./motor`); `INSTALL.txt` uses `sudo` for everything. The build-and-run
  page should explain *why* GPIO access may need root and tell students to follow
  the exact command in their handout, rather than asserting one rule.
- **Repo naming:** confirm the `github.io` setup (user page vs project page) so
  `site_url` and the Pages source are configured correctly.

### Handing the source documents to Claude Code

Yes — give Claude Code the source files; it will produce far more accurate pages
with them in hand. Recommended: commit them into the docs repo under a
non-published `_source/` folder (add `_source/` to MkDocs' ignore so it isn't built
into the site), or attach them directly in the Claude Code session. Specifically:

- All five lab handouts (Labs 1–4 + the LED bonus) — so headings and step wording
  match exactly for search.
- `HOTIS_Joystick_Fan_Wiring_Diagram.pdf` — required; it gets converted and
  embedded.
- The `Arenile/hotis-projects-starter` repo — Claude Code should clone it to read
  the real `.c`/`.h` files rather than trusting §6.0 alone.

§6.0 of this plan captures the critical facts, but the originals are the ground
truth; when in doubt, Claude Code should defer to the handouts and the repo.
