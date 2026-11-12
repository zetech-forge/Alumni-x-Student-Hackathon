---
title: Track Rules & How to Compete
parent: IoT & Robotics
grandparent: Hackathon Tracks
nav_order: 3
---

# IoT & Robotics: Track Rules & How to Compete

Every project must connect to at least one UN Sustainable Development Goal (SDG), fit the two-day build window, and be identified as an educational prototype. Team size, eligibility, the Alumni/Finalist Collaborator requirement and conduct follow the [General Rules](../../general-rules.md).

## Format

- Select one challenge from the [Beginner, Intermediate, or Advanced tiers](challenges.md). Teams may complete the core objectives and add stretch goals if time allows.
- Build and test a working prototype during the event. A shareable simulation is an acceptable demonstration; physical hardware is optional and is not an automatic scoring advantage.
- Day 1 is for the challenge briefing, ideation and initial build. Day 2 is for development, testing, documentation and technical demonstrations. Follow the [Schedule](../../schedule.md) and announced submission freeze.
- The rover challenge uses one shared physical rover. Organizers will coordinate test slots; teams can develop and demonstrate rover control logic in simulation while waiting.

## Allowed tools and technology

- Arduino Uno R3 or ESP32 and the components allocated by the organizers.
- Arduino IDE or another suitable development environment and programming language.
- Wokwi or another suitable simulator for code and circuit behavior. Clearly identify what was simulated and what was tested physically.
- Teams may use documentation and code libraries, but must credit external libraries, examples, and other reused material and explain their own contribution.
- Do not assume that every team will receive a particular sensor or module. Ask organizers about shared parts and schedule scarce equipment before building a design that depends on it. Optional components must not be required for a valid submission.
- The fingerprint module is optional. Use a simulated access decision if it is unavailable; do not collect or store real fingerprints.
- Disclose significant AI assistance and explain your own code and design decisions. Use synthetic sample data and never publish passwords, API keys or private device credentials.

## Physical safety (mandatory)

- Follow organizer guidance for power, wiring, batteries, soldering, and equipment use. Report damaged or malfunctioning equipment instead of attempting repairs during the competition.
- Keep moving parts secured when the rover is not being tested. Run it at controlled speed on a clear, marked course with an accessible stop or power-off method, under organizer supervision.
- Never connect the relay to mains electricity. Use only a low-voltage demonstration load such as an LED.
- Do not release gas, create smoke, or use an open flame to test a gas or flame sensor. Use simulator controls or safe, organizer-approved test inputs.
- Do not bring personal hardware that organizers have not safety-checked.

## Submission requirements

Follow the event-wide submission process and deadline in the [General Rules](../../general-rules.md). Each IoT & Robotics team must include:

1. Project title and selected challenge tier.
2. Source code and a README with setup, run, and demonstration instructions.
3. A wiring diagram or system diagram showing the main inputs, controller, outputs, and power arrangement.
4. A live demonstration or a shareable simulation link. If hardware is used, explain which parts were physically tested.
5. Brief test evidence showing the core behavior under at least three relevant input or route conditions.
6. A short README explanation of the user need, design decisions, selected SDG and prototype limitations.
7. The common 2-3 minute backup demo video, team details, Alumni Contribution note and AI/external-resource acknowledgments.

Before assessment, have the source files, simulation or approved hardware, test inputs, diagram and test log accessible. Explain any environment configuration without exposing credentials. **No slide deck or formal pitch is required for Track-Level Judging.**

Do not claim that an educational prototype is a certified safety, security, access-control, or emergency-response system. Sensor readings from uncalibrated modules or simulation are not certified measurements.

## Judging criteria

Beginner, Intermediate and Advanced are each scored directly out of **100 points**, with no difficulty multiplier or automatic advantage for selecting a harder tier. The [challenge-specific checkpoints](challenges.md) explain the expected outcomes.

| Criterion | Points | What your team must demonstrate |
| --- | ---: | --- |
| Functionality and correctness | 40 | Required sensor/control inputs produce the specified outputs and state transitions for the selected tier. |
| Code quality, documentation and testing | 20 | Understandable source code, reproducible setup, system diagram and test evidence for the stated cases. |
| Creativity, practical use and SDG connection | 20 | A justified design serving a specific campus/community need, a relevant SDG and honest limits. |
| Reliability and safety | 20 | Repeatable behavior, relevant boundary/changed-input checks and safe outputs, wiring or equivalent simulated controls. |
| **Total** | **100** | **Technical assessment only; no presentation marks.** |

Physical and simulated builds are assessed against equivalent behavior. Hardware access alone is not a scoring advantage; a simulation-only submission can earn full marks. Complete evidence can earn full credit for a requirement, partial/inconsistent behavior earns partial credit, and missing or unsupported work earns none for the affected requirement.

### What to expect

Every team undergoes technical inspection of its implementation, source code, wiring/configuration, documentation and test outputs. You may be asked to repeat a run, change a safe input or explain a design choice. A demonstration verifies implementation; it is **not a separately scored presentation**. Slides, speaking style and pitching quality do not contribute to the score.

## Scoring and tie-breakers

Approximately **two to three judges** may assess each team. Each independently awards a score out of 100 using the selected tier's criteria. Their scores are averaged for your official Track-Level score; teams rank by that final average.

Example: `(85 + 90 + 88) / 3 = 87.67/100`.

Ties use the higher average **Functionality and correctness** sub-score, then **Reliability and safety**, then **Code quality, documentation and testing**, followed by panel deliberation on technical evidence where necessary.

The **top three teams** qualify for the **Grand Finale**. The highest-ranked team receives **Best IoT and Robotics Solution**.

## Timeline

The Day 1 briefing introduces challenge selection and hardware booking. Use Day 2 for final tests and evidence preparation. Organizers will communicate rover test slots and any track-specific cut-off.

## Hardware allocation reminder
The [Challenges page](challenges.md#shared-hardware-planning-note) lists the known inventory and quantities. Confirm allocated components, cable/power compatibility and booking slots before relying on physical equipment. Simulation can replace unavailable shared parts; teams are not required to buy hardware.
