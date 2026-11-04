---
title: Curated Resources
parent: IoT & Robotics
grandparent: Hackathon Tracks
nav_order: 2
---

These free official references support the Beginner, Intermediate, and Advanced challenges. Start with the Arduino and Wokwi introductions, then use the part-specific guide for the sensor or output in your prototype.

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
| [Wokwi HC-SR04 ultrasonic sensor](https://docs.wokwi.com/parts/wokwi-hc-sr04) | Part guide | Free for personal use | Lets teams change simulated distance values to develop and demonstrate proximity logic. |
| [Wokwi relay module](https://docs.wokwi.com/parts/wokwi-relay-module) | Part guide | Free for personal use | Shows relay control behavior. For this event, use it only with a low-voltage demonstration load. |

## Simulation and hardware notes

Wokwi is useful for testing the Uno/ESP32 code and the documented sensor or output parts before using the shared physical kits. The current listed parts include PIR, MQ-2, thermistor, HC-SR04, LEDs, and relay. Check the supported-hardware list before depending on a particular module. The fingerprint reader and the complete rover chassis are not required for a Wokwi submission; simulate the access decision or rover control inputs where needed, then book the physical rover for an optional test slot.

Simulation helps teams develop and demonstrate control logic. It does not validate real-world sensor calibration, wiring, battery performance, motor behavior, or safety. Clearly identify what you simulated and what you tested on hardware.
