---
title: Challenges
parent: IoT & Robotics
grandparent: Hackathon Tracks
nav_order: 4
---

# IoT & Robotics: Challenges

Choose **one** challenge tier that fits your team's experience and ambition. Every tier is designed for a working prototype during the two-day hackathon. Start with the required core objectives; stretch goals are optional. Teams may build with the available hardware, use a simulator such as Wokwi, or combine both. A simulation is a valid prototype and will be judged on the same stated behavior as a physical build.

All teams must explain the campus or community need their prototype addresses and connect it to at least one Sustainable Development Goal (SDG). The prototype is an educational demonstration, not a certified safety, security, or emergency-response device.

## Shared expectations

- Use only hardware your team has been allocated. The available inventory is limited, so ask a mentor to schedule shared equipment such as the rover, ESP32, MQ-2, PIR, thermistor, and fingerprint module.
- Teams may use Arduino Uno R3 or ESP32 where suitable. Clearly state what was simulated and what was tested on physical hardware.
- Submit original, understandable code and credit any libraries, examples, or starter material you use.
- Do not connect the relay to mains electricity. Use an LED or another low-voltage demonstration load only.
- Do not use real fingerprints or store biometric data. The fingerprint module is optional; simulate an access decision if it is not available.
- Provide a safe live demonstration. Judges may ask you to repeat the core test or change a sensor input.

## Beginner — Room Activity & Energy Cue

### Scenario

A campus room is sometimes left lit or treated as occupied when nobody is using it. Build a simple indicator that responds to detected movement and makes the room's activity state easy to understand.

### Objectives

1. Read a PIR motion sensor or simulate its output.
2. Turn an LED indicator on when motion is detected and return it to the idle state after a chosen timeout.
3. Show at least two understandable states, such as **Activity detected** and **No recent activity**.
4. Explain one way this information could help a campus user make a better energy-use decision.

**Stretch goals:** Add a second status LED, a buzzer that can be muted, or a short event counter in the Serial Monitor.

### Constraints

- The core build must use a PIR sensor (or a simulated PIR input), an LED, and a microcontroller or equivalent simulation.
- Do not claim that a PIR sensor identifies a person or proves that a room is occupied. It detects motion and can miss a stationary person.
- The design must not switch building lighting or other mains-powered equipment.

### Deliverables

- A live demonstration or shareable simulation link.
- Source code and a short README with setup and test instructions.
- A simple wiring/system diagram.
- A two-minute explanation of the user need, state behavior, limitations, and chosen SDG.

### Points — 100

- Functionality and correctness — 40: Motion input triggers the indicator, and the system returns to idle after the stated timeout.
- Code quality, documentation, and testing — 20: The code is understandable, setup steps are clear, and the team demonstrates repeated tests.
- Creativity, practical use, and SDG connection — 20: The indicator supports a sensible campus energy-use decision and the team explains its limits.
- Demonstration and presentation — 20: The team clearly demonstrates the behavior and gives a concise pitch.

**Judging note:** Judges should trigger motion more than once and check that the indicator returns to idle as described. Score a simulation on its demonstrated behavior, not on whether hardware was available.

## Intermediate — Safer Campus Environment Monitor

### Scenario

A campus workshop or shared room needs an affordable way to flag a possible environmental hazard to people nearby. Build a prototype that monitors a sensor input and provides a clear, staged alert.

### Objectives

1. Use the MQ-2 gas sensor, thermistor, or both; simulation is acceptable.
2. Define a normal state and at least one warning/alert threshold. If using both sensors, explain how their readings combine in the decision.
3. Give an understandable local alert using LEDs and/or a buzzer.
4. Explain what a user should do when an alert appears and what the prototype cannot determine.

**Stretch goals:** Add a distinct warning and urgent state, a reset/acknowledge action, a relay-driven low-voltage indicator, or a timestamped event log.

### Constraints

- This is a demonstration of alert logic, not a calibrated gas detector or certified fire/safety system. Do not test by releasing gas, creating smoke, or using an open flame.
- MQ-2 and thermistor readings in simulation or from an uncalibrated module must be described as sample/relative readings, not reliable parts-per-million or certified temperature measurements.
- If using the relay, connect only a low-voltage demo load such as an LED. Never connect mains electricity.
- Teams must document their threshold choice and demonstrate both normal and alert conditions.

### Deliverables

- A live demonstration or shareable simulation link showing normal and alert conditions.
- Source code, README, and wiring/system diagram.
- A small test table listing the input condition, expected state, and observed output for at least three cases.
- A two-minute explanation of the use case, response guidance, limitations, and chosen SDG.

### Points — 100

- Functionality and correctness — 40: Sensor thresholds produce the expected normal and alert states, with a clear local warning.
- Code quality, documentation, and testing — 20: The team documents thresholds and demonstrates at least three relevant test cases.
- Creativity, practical use, and SDG connection — 20: The alert fits a real campus need and includes sensible user guidance and honest limitations.
- Demonstration and presentation — 20: The demo clearly shows state changes and the pitch explains the intended response.

**Judging note:** Judges may change the simulated sensor value or use a safe test input. Reward clear state transitions and honest limitations; do not reward claims that the prototype guarantees safety.

## Advanced — Rover Rescue Run

### Scenario

A campus support rover must travel through a short route, avoid a simulated or physical obstacle, and stop at a marked destination to represent delivering a small item or reaching a help point.

### Objectives

1. Build or simulate a rover control system using the available car chassis/rover, motors, motor driver, battery, and a suitable microcontroller. Teams may simulate the control logic if the shared rover is in use.
2. Complete a marked route and stop at the destination.
3. Detect and respond safely to at least one obstacle. A sensor-based obstacle response is preferred; teams using a simpler control method must explain its limits.
4. Demonstrate a repeatable start, movement, obstacle response, and stop sequence.

**Stretch goals:** Add a second route, manual override, status LEDs, a low-battery indicator, or a simulated delivery/arrival message.

### Constraints

- Only the single physical rover is available; teams must book a test slot with the organizers. Simulation-first development is encouraged so all teams can progress in parallel.
- Keep the physical course short, clear, and safe. The rover must move at a controlled speed, remain within the marked area, and have an accessible stop/power-off method.
- Do not add unlisted physical parts unless organizers approve their availability. A simulated sensor or motor-control component is acceptable and must be identified in the submission.
- Teams are responsible for demonstrating their chosen control and obstacle inputs; the challenge does not require autonomous mapping or advanced navigation.

### Deliverables

- A physical run, shareable simulation, or both. State clearly which parts were tested physically.
- Source code, README with setup/run steps, and a wiring/system diagram.
- A short test log with at least three runs, noting route completion and obstacle behavior.
- A two-minute explanation of the campus use case, design choices, limitations, and chosen SDG.

### Points — 100

- Functionality and correctness — 40: The rover or simulated controller completes the route, responds to an obstacle, and stops safely.
- Code quality, documentation, and testing — 20: Setup and control logic are explained, with a log of at least three runs or equivalent simulated tests.
- Creativity, practical use, and SDG connection — 20: The route task addresses a plausible campus need and the design explains its limitations.
- Demonstration and presentation — 20: The team demonstrates the sequence clearly and gives a concise pitch.

**Judging note:** Judges should use the same marked route and obstacle placement for each physical run. A simulation-first team can earn full points by demonstrating the required logic clearly; physical access is not a scoring advantage by itself.

## Submission checklist

Before the track deadline, make sure your team has submitted:

- Challenge tier and project title.
- Source code and README with setup and demonstration steps.
- A wiring/system diagram.
- A working demonstration or simulation link.
- Test evidence and a brief statement of what was simulated versus physically tested.
- A short pitch that names the user need, chosen SDG, and the prototype's limitations.

Teams should follow the event's general submission deadline and the IoT & Robotics track rules for demonstration and judging logistics.
