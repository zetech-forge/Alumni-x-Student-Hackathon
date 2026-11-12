---
title: Scoring Rubric
parent: IoT & Robotics
grandparent: Hackathon Tracks
nav_order: 5
---

# IoT & Robotics: Scoring Rubric

Use this rubric with the [Judge Score Sheet](judge-sheet.md). Each team selects one technical tier and completes the same real-world application brief. Scores are based on demonstrated evidence and clear reasoning. A simulation and a physical prototype are assessed against the same required behavior; hardware access is not a scoring advantage.

## Final score: 100 points

| Component | Maximum | Calculation |
| --- | ---: | --- |
| Selected technical tier | 70 | Raw tier score out of 100 × 0.70 |
| From Prototype to Real-World Impact brief | 30 | Sum of the seven shared criteria below |
| **Final score** | **100** | Normalized technical score + brief score |

Do not add stretch-goal points beyond the stated maximums. Judges score independently first, then may discuss evidence to resolve large differences. If the event uses multiple judges, use the arithmetic mean of the judges’ final scores for the team.

## A. Technical tier rubric — 100 raw points, normalized to 70

| Criterion | Points | Evidence to assess |
| --- | ---: | --- |
| Functionality and correctness | 40 | Required inputs, processing/control logic, outputs, repeatability, and safe behavior meet the selected tier objectives. |
| Code, system explanation, documentation, and testing | 20 | Team explains its own implementation, setup/run instructions are usable, diagram is understandable, and relevant tests are shown. |
| Creativity, practical use, and SDG connection | 20 | Design choices suit the stated user need, improve the solution in a purposeful way, and explain a relevant SDG link and limitations. |
| Demonstration and presentation | 20 | Demo is clear and repeatable; team communicates decisions, evidence, and limitations within the event time. |
| **Raw technical total** | **100** | Multiply by 0.70 for the final score contribution. |

### Technical performance bands

Use the exact tier checkpoint to judge what counts as successful behavior. Award one of the bands below for each criterion; use the criterion’s maximum as the scale.

| Band | Description | For a 40-point criterion | For a 20-point criterion |
| --- | --- | ---: | ---: |
| Not demonstrated | No relevant evidence, or the required behavior is absent/unsafe. | 0 | 0 |
| Early attempt | Some relevant work is visible, but the core behavior is mostly absent or cannot be repeated. | 10 | 5 |
| Partly demonstrated | Core behavior works in some cases; gaps, inconsistent results, or important explanation is missing. | 20 | 10 |
| Mostly demonstrated | Core behavior is repeatable with a minor gap; tests and explanation are largely clear. | 30 | 15 |
| Fully demonstrated | Required behavior is repeatable, tested, clearly explained, and limitations are represented honestly. | 40 | 20 |

### Tier-specific functionality checkpoints

- **Beginner — Room Activity & Energy Cue:** trigger the PIR input more than once; verify the indicator shows activity and returns to idle after the team’s stated timeout. Do not treat motion as proof that a person is present or absent.
- **Intermediate — Safer Campus Environment Monitor:** review at least three documented input cases (including normal, alert, and recovery/boundary behavior); verify the stated alert output and safe user guidance. Thresholds and sensor limitations must be explained. No real gas, smoke, or flame testing.
- **Advanced — Rover Rescue Run:** use the same marked route and obstacle event for each test; verify movement, obstacle response, destination/stop, and repeatability over at least three runs. A simulated or operator-triggered obstacle event is acceptable if no suitable sensor is allocated; no unlisted sensor is required. Keep the physical rover controlled and supervised.

For a simulation, judges should change a relevant input or scenario and observe the corresponding output. Do not require physical calibration, exact real-world sensor readings, or unavailable components.

## B. Mandatory real-world application brief — 30 points

Every team submits a concise plan connecting its prototype to a specific real-world need. It is not a fourth build and does not require deployment during the hackathon. Judge the quality and credibility of the reasoning, not the size of the claimed impact.

| Criterion | Points | Full-credit evidence |
| --- | ---: | --- |
| Problem, sector, and intended users | 5 | Specific problem/context, relevant sector, intended beneficiaries, and why the problem matters. |
| Solution relevance and suitability | 5 | Clear link from the demonstrated prototype to the problem and a plausible value proposition. |
| Technical architecture and stack | 5 | Readable system diagram; explains components, interactions, and what is simulated versus physical. |
| Feasibility and scalability | 5 | Credible next steps, resources/infrastructure, operating or maintenance needs, and realistic scaling/stakeholder considerations. |
| SDG alignment and societal impact | 4 | Relevant SDG(s), expected benefit, and inclusion/sustainability considerations. |
| Risks, safety, and sustainability | 4 | Identifies relevant risks (for example privacy, security, connectivity, power, reliability, safety, or environmental constraints) and reasonable mitigations. |
| Measurable outcomes | 2 | Names at least one relevant success indicator and a credible way to measure it. |
| **Brief total** | **30** | |

### Brief scoring bands

For each 5-point criterion, award 0 (no evidence), 1 (weak or generic), 2 (partial), 3 (credible but incomplete), 4 (strong), or 5 (specific and well-supported). For each 4-point criterion, use 0–4 with the same descriptions. For the 2-point indicator criterion, use 0 (absent), 1 (named but unclear), or 2 (relevant and measurable). Do not award full credit for unsupported cost, scale, or impact claims.

## Tie-break order

Follow the event’s general rules. For this track, compare in order: (1) technical functionality and repeatability; (2) feasibility and risk handling in the impact brief; (3) practical use and SDG reasoning; (4) clarity of the demonstration. If still tied, use the event organizer’s published tie-break procedure.

## Judge process

1. Read the selected tier and its objectives before the demo.
2. Ask the team to demonstrate the required behavior; request one repeat test or safe input change.
3. Score each technical criterion out of 100 raw points using the bands above.
4. Score each impact-brief criterion, then total the brief out of 30.
5. Calculate **(raw technical total × 0.70) + brief total**.
6. Record observed evidence and comments on a separate [Judge Score Sheet](judge-sheet.md) for each team.

The prototype is an educational demonstration, not a certified safety, security, access-control, or emergency-response system.
