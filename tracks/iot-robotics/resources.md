---
title: Curated Resources
parent: IoT & Robotics
grandparent: Hackathon Tracks
nav_order: 2
---

# IoT & Robotics: Curated Resources

These official references support **Room Activity & Energy Cue (Beginner)**, **Safer Campus Environment Monitor (Intermediate)** and **Rover Rescue Run (Advanced)**. Documentation is free to read; check simulator account/sharing limits before relying on a feature. Learn only the parts required by your selected challenge.

| Challenge | Start with | Use next |
|---|---|---|
| Beginner | Arduino/Wokwi setup and board pin reference. | PIR behavior, LED output and the documented inactivity timer tests. |
| Intermediate | Board analog/digital input and the selected MQ-2 or NTC reference. | Threshold/alert tests and optional output guidance. Two sensors are not mandatory. |
| Advanced | Controller/motor-interface documentation for the actual allocated kit, or an approved virtual setup. | Virtual obstacle input, repeatable route/control trace and stop tests. No particular physical obstacle sensor is guaranteed. |

Follow the [step-by-step simulation setup](challenges.md#starting-a-simulation). It covers project creation, board selection, wiring, code execution, observing outputs and saving test evidence.

## Getting started and simulation

| Resource | Type | Cost | Why it is useful |
| --- | --- | --- | --- |
| [Getting Started with Arduino](https://docs.arduino.cc/learn/starting-guide/getting-started-arduino/) | Tutorial | Free | Introduces boards, sketches, the IDE, and the basic ideas behind a microcontroller project. |
| [Arduino UNO R3 documentation](https://docs.arduino.cc/hardware/uno-rev3/) | Board reference | Free | Shows the Uno pinout, capabilities, and board-specific information for the three available Uno R3 boards. |
| [Arduino Learn](https://docs.arduino.cc/learn/) | Tutorials | Free | Offers practical guides to digital pins, analog input, PWM, sketches, and Arduino programming. |
| [Wokwi simulator documentation](https://docs.wokwi.com/) | Simulator guide | Free for personal use | Introduces browser-based simulation for Arduino and ESP32 and explains how to start a project. |
| [Wokwi supported hardware](https://docs.wokwi.com/getting-started/supported-hardware) | Compatibility reference | Free | Check whether a board or component is available in the simulator before designing around it. |
| [Arduino-ESP32 Getting Started](https://docs.espressif.com/projects/arduino-esp32/en/latest/getting_started.html) | Board setup | Free | Explains the Arduino framework supported by Espressif for programming ESP32 boards. |

## Sensors and outputs

| Resource | Type | Cost | Why it is useful |
| --- | --- | --- | --- |
| [Wokwi PIR motion sensor](https://docs.wokwi.com/parts/wokwi-pir-motion-sensor) | Part guide | Free for personal use | Shows how to trigger simulated motion and explains the sensor's output and timing behavior. |
| [Wokwi MQ-2 gas sensor](https://docs.wokwi.com/parts/wokwi-gas-sensor) | Part guide | Free for personal use | Demonstrates analog and threshold outputs for the MQ-2. Treat simulation readings as sample values, not calibrated safety measurements. |
| [Wokwi NTC thermistor](https://docs.wokwi.com/parts/wokwi-ntc-temperature-sensor) | Part guide | Free for personal use | Explains the analog temperature input and how to interpret it in a simple prototype. |
| [Wokwi HC-SR04 ultrasonic sensor](https://docs.wokwi.com/parts/wokwi-hc-sr04) | Part guide | Free for personal use | Optional virtual distance input for proximity/control tests; this link does not confirm a physical HC-SR04 in the event inventory. |
| [Wokwi relay module](https://docs.wokwi.com/parts/wokwi-relay-module) | Part guide | Free for personal use | Shows relay control behavior. For this event, use it only with a low-voltage demonstration load. |

## Simulation and hardware notes

Wokwi supports circuit/controller experiments with documented virtual parts such as PIR, MQ-2, thermistor, distance inputs, LEDs and relay. **Simulator support and physical inventory are different lists.** Check the supported-hardware page and the [allocation note](challenges.md#shared-hardware-planning-note) separately; confirm cabling, power and shared booking slots with the mentor.

The existing track permits equivalent suitable simulators; a different electronic circuit or virtual robotics environment needs mentor approval for the selected outcomes. No additional named robotics platform, paid service or hardware purchase is required.

Wokwi does not provide a complete moving rover/chassis physics model. Use an approved virtual robotics run or an explicit controller route/obstacle test scenario showing progress, movement outputs and stop behavior. Agree the equivalent scenario with the mentor before assessment. LEDs or Serial Monitor alone show commands, not measured physical movement. The single physical rover can be booked for optional supervised validation; simulation-only participation remains valid.

For physical builds, use the actual board, sensor and motor-driver documentation rather than copying a virtual pinout blindly. Uno and ESP32 logic levels differ. Never connect motors directly to GPIO, never use mains loads, and follow the [electrical/battery/movement safety rules](rules.md#physical-safety-mandatory).

Simulation helps teams develop and demonstrate control logic. It does not validate real-world sensor calibration, wiring, battery performance, motor behavior, or safety. Clearly identify what you simulated and what you tested on hardware.
