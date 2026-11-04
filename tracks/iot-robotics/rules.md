---
title: Track Rules & How to Compete
parent: IoT & Robotics
grandparent: Hackathon Tracks
nav_order: 3
---

This track contributes to the **Best IoT / Robotics Solution** award. Teams are also eligible for the overall and other event awards described in the [General Rules](../../general-rules.md). Every project must connect to at least one UN Sustainable Development Goal (SDG), fit the two-day build window, and be presented as an educational prototype.

## Format

- Select one challenge from the [Beginner, Intermediate, or Advanced tiers](challenges.md). Teams may complete the core objectives and add stretch goals if time allows.
- Build and test a working prototype during the event. A shareable simulation is an acceptable demonstration; physical hardware is optional and is not an automatic scoring advantage.
- Day 1 is for the challenge briefing, ideation, and initial build. Day 2 is for development, testing, demonstrations, and pitches. Follow the event schedule in the General Rules for exact times and submission deadlines.
- The rover challenge uses one shared physical rover. Organizers will coordinate test slots; teams can develop and demonstrate rover control logic in simulation while waiting.

## Allowed tools and technology

- Arduino Uno R3 or ESP32 and the components allocated by the organizers.
- Arduino IDE or another suitable development environment and programming language.
- Wokwi or another suitable simulator for code and circuit behavior. Clearly identify what was simulated and what was tested physically.
- Teams may use documentation and code libraries, but must credit external libraries, examples, and other reused material and explain their own contribution.
- Do not assume that every team will receive a particular sensor or module. Ask organizers about shared parts and schedule scarce equipment before building a design that depends on it. Optional components must not be required for a valid submission.
- The fingerprint module is optional. Use a simulated access decision if it is unavailable; do not collect or store real fingerprints.

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
6. A short pitch explaining the user need, design decisions, selected SDG, and limitations of the prototype.

Do not claim that an educational prototype is a certified safety, security, access-control, or emergency-response system. Sensor readings from uncalibrated modules or simulation are not certified measurements.

## Judging criteria

Each selected challenge is scored out of 100 points. The specific challenge page explains how the criteria apply to that tier.

| Criterion | Weight | What judges look for |
| --- | ---: | --- |
| Functionality and correctness | 40% | The required behavior works and can be demonstrated or reproduced in simulation or on hardware. |
| Code quality, documentation, and testing | 20% | The team can explain its code and system, gives clear run instructions, and shows relevant tests. |
| Creativity, practical use, and SDG connection | 20% | The idea fits a real campus or community need, has a thoughtful approach, and explains its SDG link. |
| Demonstration and presentation | 20% | The demo is clear, the pitch is understandable, and the team explains limitations honestly. |

Judges should assess the demonstrated behavior and the team's explanation, not the amount of hardware available to them. A simulation-only submission can earn full marks when it meets the challenge objectives.

## Scoring and tie-breakers

The selected challenge's 100-point breakdown is the scoring sheet. If teams tie, compare their functionality and repeatability first, then their practical use and SDG explanation, then their demonstration and pitch. Judges may ask teams to repeat a test or change a simulated input.

## Timeline

Follow the event-wide schedule in the General Rules. The IoT track briefing introduces the challenge tiers and hardware booking process on Day 1; Day 2 includes time for final testing, demonstrations, and pitches. Organizers will communicate rover test slots and any track-specific submission cut-off during the event.
