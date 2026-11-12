---
title: Challenges
parent: IoT & Robotics
grand_parent: Hackathon Tracks
nav_order: 4
---

# IoT & Robotics: Challenges

Choose **one** challenge tier that fits your team's experience and ambition. Every tier is designed for a working prototype during the two-day hackathon. Start with the required core objectives; stretch goals are optional. Teams may build with the available hardware, use a simulator such as Wokwi, or combine both. A simulation is a valid prototype and will be judged on the same stated behavior as a physical build.

Each tier is assessed directly out of **100 technical points**, without difficulty multipliers. Approximately two to three judges may score each team independently; their scores are averaged for ranking. The top three teams qualify for the Grand Finale. **No slides or formal pitch are required, and technical demonstrations have no separate presentation marks.** See the [rules](rules.md) for the rubric, submissions and tie-breakers.

All teams must explain the campus or community need their prototype addresses and connect it to at least one Sustainable Development Goal (SDG). The prototype is an educational demonstration, not a certified safety, security, or emergency-response device.

## Shared expectations

- Use only hardware your team has been allocated. The available inventory is limited, so ask a mentor to schedule shared equipment such as the rover, ESP32, MQ-2, PIR, thermistor, and fingerprint module.
- Teams may use Arduino Uno R3 or ESP32 where suitable. Clearly state what was simulated and what was tested on physical hardware.
- Submit original, understandable code and credit any libraries, examples, or starter material you use.
- Do not connect the relay to mains electricity. Use an LED or another low-voltage demonstration load only.
- Do not use real fingerprints or store biometric data. The fingerprint module is optional; simulate an access decision if it is not available.
- Provide a safe live demonstration. Judges may ask you to repeat the core test or change a sensor input.

## Starting a simulation

1. Follow the [Wokwi setup and part references](resources.md) and create an Arduino Uno or ESP32 project matching your intended controller.
2. Add only the selected challenge's supported virtual inputs/outputs. Check each part's documented pin names and behavior; a component in the simulator is not a promise of physical availability.
3. Connect power, ground and signals in the virtual diagram, using an LED resistor and the correct sensor interface where applicable. Record the pin mapping in your README.
4. Enter or import your code, declare needed libraries and start the simulation. For physical hardware, use the matching board/port and mentor-checked wiring before uploading.
5. Observe Serial Monitor, state indicators and output commands. Change the simulated motion, sensor or obstacle input and compare the response with your expected result.
6. Save a shareable project/configuration and record repeatable test cases. Identify the simulated parts and limitations.

An equivalent approved circuit or virtual robotics environment is acceptable. **Wokwi simulates circuits/controllers, not a complete rover moving through a physical course.** Rover control simulation must include an explicit route/obstacle test scenario and evidence of the required movement commands, progress and stop behavior, or a suitable virtual robotics run. Confirm the equivalent scenario with the mentor; do not claim that a controller trace validates real motor dynamics.

For any physical build, use only compatible allocated parts and the [mandatory safety rules](rules.md#physical-safety-mandatory). Software/controller simulation is acceptable when a physical component or compatible power/interface arrangement is unavailable.

## Beginner — Room Activity & Energy Cue

### Scenario

A campus room is sometimes left lit or treated as occupied when nobody is using it. Build a simple indicator that responds to detected movement and makes the room's activity state easy to understand.

### Objectives

1. Read a PIR motion sensor or simulate its output.
2. Turn an LED indicator on when motion is detected and return it to the idle state after a chosen timeout.
3. Show at least two understandable states, such as **Activity detected** and **No recent activity**.
4. Explain one way this information could help a campus user make a better energy-use decision.

**Stretch goals:** Add a second status LED, a buzzer that can be muted, or a short event counter in the Serial Monitor.

### Components

| Category | Physical or virtual requirements |
|---|---|
| Mandatory | Uno R3, ESP32 or equivalent controller simulation; PIR motion input; LED indicator. Physical builds also need a suitable LED resistor, compatible power and approved wiring. |
| Optional | Second LED, buzzer or Serial Monitor event counter. |
| Alternatives | A virtual PIR/LED/controller circuit when the shared PIR or board is unavailable. A breadboard is useful where needed, not a separate scoring requirement. |

### Implementation steps

1. Choose the controller, PIR and LED; confirm allocation/compatibility or create the virtual circuit.
2. Draw and build the input/controller/output connections using the relevant pin references. Obtain a wiring check before powering physical hardware.
3. Read the PIR's digital motion output and display it in Serial Monitor; allow the physical sensor's documented startup behavior.
4. Define the two states and a chosen inactivity timeout. Explain what happens if motion is detected again during the active period.
5. Implement activity/timer logic: motion activates the LED; no recent motion returns it to idle after the stated timeout.
6. Keep the output limited to the indicator. Explain the energy-use cue, not an unsupported claim that the prototype switches or measures building energy.
7. Test no motion, motion, return to idle and repeated motion; compare elapsed behavior with the documented timer policy.
8. Save source, component/pin diagram, setup instructions and observed results, including the limits of PIR sensing.

### Constraints

- The core build must use a PIR sensor (or a simulated PIR input), an LED, and a microcontroller or equivalent simulation.
- Do not claim that a PIR sensor identifies a person or proves that a room is occupied. It detects motion and can miss a stationary person.
- The design must not switch building lighting or other mains-powered equipment.

### Deliverables

- A live demonstration or shareable simulation link.
- Source code and a short README with setup and test instructions.
- A simple wiring/system diagram.
- Component/pin details and a test log covering at least three input/timing cases.
- A short README explanation of the user need, state behavior, limitations and chosen SDG.

### Points — 100

| Criterion | Points | Required evidence |
|---|---:|---|
| Core functionality and correctness | 35 | PIR input activates the LED, distinguishes activity/idle and returns to idle after the stated inactivity timeout. |
| Technical design and component integration | 20 | Correct input/output mapping, suitable circuit and explained timer/retrigger policy. |
| Testing, reliability and safe operation | 20 | At least three documented cases, repeated motion/no-motion behavior and safe low-voltage outputs or equivalent simulated safeguards. |
| Code quality, diagrams and documentation | 15 | Understandable code, component/pin diagram, reproducible setup and actual test results. |
| Practical relevance and SDG alignment | 10 | A sensible room-energy cue, relevant SDG and honest PIR/energy-impact limitations. |
| **Total** | **100** | **No presentation allocation.** |

**Technical checkpoints:** Be ready to repeat motion/no-motion tests, retrigger during the active period and verify the stated return-to-idle behavior. A simulation is assessed on the same outcomes as hardware.

## Intermediate — Safer Campus Environment Monitor

### Scenario

A campus workshop or shared room needs an affordable way to flag a possible environmental hazard to people nearby. Build a prototype that monitors a sensor input and provides a clear, staged alert.

### Objectives

1. Use the MQ-2 gas sensor, thermistor, or both; simulation is acceptable.
2. Define a normal state and at least one warning/alert threshold. If using both sensors, explain how their readings combine in the decision.
3. Give an understandable local alert using LEDs and/or a buzzer.
4. Explain what a user should do when an alert appears and what the prototype cannot determine.

**Stretch goals:** Add a distinct warning and urgent state, a reset/acknowledge action, a relay-driven low-voltage indicator, or a timestamped event log.

### Components

| Category | Physical or virtual requirements |
|---|---|
| Mandatory | Suitable controller; MQ-2 **or** thermistor input, or both; LED and/or buzzer alert. Physical builds need compatible power, signal interfaces and the appropriate resistors/wiring. |
| Optional | A second sensor, extra alert states, acknowledge/reset control, event log or a relay connected only to a low-voltage demo load. |
| Alternatives | Virtual MQ-2 or NTC input when the physical part is unavailable. Either listed sensor satisfies the core requirement; two sensors are not mandatory. |

### Implementation steps

1. Select the allocated sensor(s) or virtual parts and controller; label the input as gas-related or temperature-related, as appropriate.
2. Build the circuit and document power, signal pins and any required resistor/interface arrangement. Do not assume sensor output voltages are safe for every controller.
3. Read sample values and display them in Serial Monitor; state whether they are simulated, raw/relative or calibrated.
4. Define the normal/alert threshold and its boundary rule, such as whether equality triggers the alert. Justify it as a demonstration setting, not a certified hazard limit.
5. Implement the monitoring logic. If using two sensors, explain how the readings combine; avoid adding a second sensor merely for assumed extra marks.
6. Connect the normal/alert state to the chosen LED/buzzer. Provide clear response guidance and make optional reset/acknowledge behavior explicit.
7. Test at least three cases, including normal, alert and threshold behavior. Use simulator controls or safe organizer-approved inputs only; repeat transitions to check reliability.
8. Document inputs, expected/observed states, threshold policy, setup and limitations. Do not report simulated or uncalibrated values as certified safety measurements.

### Constraints

- This is a demonstration of alert logic, not a calibrated gas detector or certified fire/safety system. Do not test by releasing gas, creating smoke, or using an open flame.
- MQ-2 and thermistor readings in simulation or from an uncalibrated module must be described as sample/relative readings, not reliable parts-per-million or certified temperature measurements.
- If using the relay, connect only a low-voltage demo load such as an LED. Never connect mains electricity.
- Teams must document their threshold choice and demonstrate both normal and alert conditions.

### Deliverables

- A live demonstration or shareable simulation link showing normal and alert conditions.
- Source code, README, component/pin details and wiring/system diagram.
- A small test table listing the input condition, expected state, and observed output for at least three cases.
- A short README explanation of the use case, response guidance, limitations and chosen SDG.

### Points — 100

| Criterion | Points | Required evidence |
|---|---:|---|
| Core functionality and correctness | 35 | The selected sensor input(s) produce the defined normal/alert states and understandable local warning. |
| Technical design and component integration | 20 | Appropriate sensor/interface choice, threshold logic and output integration; explain combined decisions if using both sensors. |
| Testing, reliability and safe operation | 20 | At least three normal/alert/boundary cases, repeatable transitions and safe simulated or approved physical inputs. |
| Code quality, diagrams and documentation | 15 | Clear code, component/pin diagram, reproducible setup, threshold definitions and observed results. |
| Practical relevance and SDG alignment | 10 | A relevant campus use case/SDG, sensible response guidance and explicit measurement/certification limits. |
| **Total** | **100** | **No presentation allocation.** |

**Technical checkpoints:** Have at least three input cases ready, including normal, alert and threshold behavior. Be able to change a simulated or safe sensor input, reproduce the state transition and explain the response guidance and limitations.

## Advanced — Rover Rescue Run

### Scenario

A campus support rover must travel through a short route, avoid a simulated or physical obstacle, and stop at a marked destination to represent delivering a small item or reaching a help point.

### Objectives

1. Build or simulate a rover control system using the available car chassis/rover, motors, motor driver, battery, and a suitable microcontroller. Teams may simulate the control logic if the shared rover is in use.
2. Complete a marked route and stop at the destination.
3. Detect and respond safely to at least one obstacle. A sensor-based obstacle response is preferred; teams using a simpler control method must explain its limits.
4. Demonstrate a repeatable start, movement, obstacle response, and stop sequence.

**Stretch goals:** Add a second route, manual override, status LEDs, a low-battery indicator, or a simulated delivery/arrival message.

### Components

| Category | Physical or virtual requirements |
|---|---|
| Mandatory | Controller, movement/motor-control outputs, a defined obstacle input or approved simpler control method, and route/destination/stop behavior. Physical builds use the allocated rover chassis, motors, compatible driver and approved battery/power arrangement. |
| Optional | An available approved obstacle sensor, status LEDs, second route, manual override or low-battery indication. An accessible stop/power-off method is mandatory for physical safety, even when a software override is optional. |
| Alternatives | Approved virtual rover, or a controller simulation with a documented equivalent route/obstacle scenario and output trace. Simulated distance/obstacle input is valid; the physical inventory does not guarantee an ultrasonic sensor. |

### Implementation steps

1. Agree the marked route, destination and obstacle scenario with the mentor. No universal route length or completion-time limit is currently specified; confirm operational constraints at the briefing rather than inventing them.
2. Identify allocated controller/chassis/driver/power parts or the equivalent virtual setup, and document the chosen obstacle/control input.
3. Configure motor-control outputs and the driver interface. For physical tests, have wiring/power checked and secure moving parts for initial checks; never drive motors directly from GPIO.
4. Connect and inspect the obstacle input, whether an approved sensor, virtual distance value or the permitted simpler method. Explain any detection limitations.
5. Implement start, forward/turn and destination-stop behavior for the agreed route. Check direction commands before attempting a full run.
6. Add the obstacle response: stop or avoid safely according to the scenario, then continue only when the chosen policy permits. Keep control/stop checks responsive.
7. Test the complete route and obstacle sequence at least three times, recording completion, response and stop outcomes. Simulation must show the equivalent route/control sequence, not just code compilation.
8. Debug pin mapping, motor direction, input interpretation and timing using logs or simulated traces. Disconnect physical power before adjustments.
9. Demonstrate a repeatable run ending at the destination; provide code, configuration/diagram, test log and limitations. Keep physical tests at controlled speed inside the supervised course.

### Constraints

- Only the single physical rover is available; teams must book a test slot with the organizers. Simulation-first development is encouraged so all teams can progress in parallel.
- Keep the physical course short, clear, and safe. The rover must move at a controlled speed, remain within the marked area, and have an accessible stop/power-off method.
- Do not add unlisted physical parts unless organizers approve their availability. A simulated sensor or motor-control component is acceptable and must be identified in the submission.
- Teams are responsible for demonstrating their chosen control and obstacle inputs; the challenge does not require autonomous mapping or advanced navigation.

### Deliverables

- A physical run, shareable simulation, or both. State clearly which parts were tested physically.
- Source code, README with setup/run steps, component/pin details and a wiring/system diagram.
- A short test log with at least three runs, noting route completion and obstacle behavior.
- A short README explanation of the campus use case, design choices, limitations and chosen SDG.

### Points — 100

| Criterion | Points | Required evidence |
|---|---:|---|
| Core functionality and correctness | 35 | The rover or equivalent simulation starts, follows the marked route, responds to an obstacle and stops at the destination. |
| Technical design and component integration | 20 | Appropriate controller/driver/movement integration, interpreted obstacle input and explained route/control decisions. |
| Testing, reliability and safe operation | 20 | At least three repeatable runs or equivalent scenarios, verified obstacle/stop behavior and safe physical or simulated controls. |
| Code quality, diagrams and documentation | 15 | Readable control code, component/pin or system diagram, reproducible run instructions and the test log. |
| Practical relevance and SDG alignment | 10 | A plausible campus use case/SDG and honest limits of sensing, navigation and simulated versus physical behavior. |
| **Total** | **100** | **No presentation allocation.** |

**Technical checkpoints:** Be ready to repeat the marked route and obstacle scenario, show start/movement/obstacle/stop behavior and explain the three-run log. Simulation can demonstrate equivalent control logic; hardware access is not a scoring advantage.

## Submission checklist

Before the track deadline, make sure your team has submitted:

- Challenge tier and project title.
- Source code and README with setup and demonstration steps.
- A component list and wiring/pin or system diagram, including the physical or virtual configuration needed to reproduce the build.
- A working demonstration or simulation link.
- Test evidence and a brief statement of what was simulated versus physically tested.
- A README explanation naming the user need, chosen SDG and prototype limitations.
- The common 2-3 minute backup demo video, team details, Alumni Contribution note and AI/external-resource acknowledgments.

Teams should follow the event's general submission deadline and the IoT & Robotics track rules for demonstration and judging logistics.

## How technical evidence earns credit

Each tier's allocation is **35 + 20 + 20 + 15 + 10 = 100 points**. Full credit for a requirement depends on demonstrated behavior and supporting code, tests or documentation; partial or inconsistent evidence receives partial credit, and absent or unsupported evidence receives none for the affected requirement. Stretch goals count only within these allocations. Simulation and hardware use the same evidence standard, with no hardware bonus or separate presentation marks.

### Shared hardware planning note
The listed inventory includes: 3 Arduino Uno R3, 1 ESP32, 1 PIR sensor, 1 MQ-2 gas sensor, 1 fingerprint module, 1 rover/car chassis set (including motors, motor driver, and battery), 1 thermistor, 1 flame sensor, 1 Bluetooth module, 1 relay, 15 red LEDs, 20 resistors, 5 breadboards, and the listed KY modules. Confirm allocation and book shared or single-quantity items with organizers. Jumper wires, USB cables and battery details are not fully specified; confirm compatibility before physical testing. Only the selected tier's core parts are required; disclose simulation substitutions for unavailable equipment. Teams are not expected to buy hardware.
