---
title: Content & Curriculum
parent: IoT & Robotics
grandparent: Hackathon Tracks
nav_order: 1
---

# IoT & Robotics: Content & Curriculum

## Learning objectives

By the end of preparation and the hackathon, participants should be able to:

- Describe the basic role of a microcontroller, sensor input, output device, and power source in an IoT prototype.
- Read a digital input such as a PIR output and an analog input such as a thermistor or gas-sensor output.
- Write and explain simple Arduino-style logic that changes an LED, buzzer, relay signal, or motor-control output in response to an input.
- Use simulation to build and demonstrate sensor logic when physical components are shared or unavailable.
- Test normal and alert cases, document what happened, and explain limitations and safe use.
- Present a practical campus or community use case and connect it to at least one Sustainable Development Goal (SDG).

## Prerequisite knowledge

No prior robotics experience is required for every challenge. Basic programming, digital/analog inputs and circuit terminology help with the Beginner build; Intermediate teams should be ready to reason about thresholds, while Advanced teams need motor/control debugging and a repeatable route/obstacle test approach. Use mentor support and simulation to fill gaps rather than treating every component as a prerequisite.

Bring or arrange access to a computer capable of running the chosen tools. Wokwi uses a browser; physical builds use Arduino IDE or an equivalent board toolchain. Confirm connectivity/project-sharing access and any board support packages before relying on them. Teams do not need to buy hardware.

## Topic breakdown

| Module | Topics and hands-on activity | Suggested time |
| --- | --- | ---: |
| 1. Microcontroller and circuit basics | Identify the Uno and ESP32, digital and analog pins, ground, breadboard rows, LEDs, and current-limiting resistors. Build or simulate a blink circuit. | 30–45 min |
| 2. Read a sensor | Read a PIR as a digital input or vary simulated MQ-2/thermistor values; virtual distance/obstacle inputs are useful for rover control. Print readings or state changes to Serial Monitor. | 45–60 min |
| 3. Turn input into behavior | Use conditions, thresholds, and a simple timer to control LEDs or a buzzer. Test both normal and alert states. | 45–60 min |
| 4. Prototype and test | Sketch the system, build in Wokwi or with allocated hardware, test repeatability, and record simulated versus physical behavior. | 60–90 min |
| 5. Explain the solution | Prepare a short demo, README, system diagram, SDG connection, and honest statement of limitations. | 30–45 min |

These are practice estimates, not a requirement to finish every module before building. Use the [simulation setup steps](challenges.md#starting-a-simulation) and the [part references](resources.md) for your chosen challenge.

## Preparation by challenge

| Challenge | Essential preparation | First working checkpoint | Supplementary only |
|---|---|---|---|
| Room Activity & Energy Cue - Beginner | Modules 1-3: board/pin basics, PIR digital input, LED output and a timer. | Trigger simulated motion and show the LED returning to idle after the stated timeout. | Extra LEDs, buzzer and counters. |
| Safer Campus Environment Monitor - Intermediate | Modules 1-4: selected sensor input, threshold/boundary logic, normal/alert output and safe tests. | Vary a simulated reading through normal, threshold and alert cases and record results. | A second sensor, extra alert states, acknowledge/reset or a relay-driven low-voltage indicator. |
| Rover Rescue Run - Advanced | Modules 1, 3-4 plus controller/driver interfaces, route states, obstacle input and stop behavior. | Show start, movement commands, obstacle response and stop in an agreed virtual/control scenario before booking hardware. | Extra routes, richer indicators and more advanced navigation. |

Every team needs Module 5's clear source/diagram/test documentation. Simulation supports full participation but does not certify physical wiring, sensor accuracy, battery behavior or rover dynamics.

## Suggested preparation and event timeline

**Before the event (optional, about 2–3 hours):** Complete Modules 1–3 using the linked Arduino and Wokwi resources. If time is limited, prioritize blinking an LED, reading one input, and changing an output based on that input. Teams do not need to purchase parts or prepare a complete project in advance.

**Day 1 — Understand and build:** Attend the track briefing, select one challenge tier, identify the user need, and divide tasks. Begin with a small working sensor-to-output prototype. Use simulation first if a physical part is not immediately available; ask organizers to schedule shared hardware when needed.

**Day 2 — Test and demonstrate:** Complete the core behavior, test several input cases, improve reliability, and prepare the required code, README, system diagram, test log and backup demo video. Make clear which features were simulated and which were tested physically. Every tier is assessed directly out of 100 technical points; no slides or formal pitch are required, and presentation quality earns no points. Use the [Track Rules](rules.md) and [Challenges](challenges.md) pages for submission and scoring details.

The shared allocation is **35 functionality + 20 design/integration + 20 testing/reliability/safety + 15 code/diagrams/documentation + 10 practical relevance/SDG alignment = 100 points**. A physical component is not an automatic scoring advantage.

## Learning resources

Use the [Curated Resources](resources.md) page for the official board, programming, sensor, and simulation references selected for this track.
