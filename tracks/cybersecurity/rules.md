---
title: Track Rules & How to Compete
parent: Cybersecurity
grand_parent: Hackathon Tracks
nav_order: 3
---

# Cybersecurity: Track Rules & How to Compete

## Format

This is a **task-based defensive security track**, not a difficulty-tier or flags competition. Select **two or three of the nine published lab tasks**: five Windows and four Linux. You may work on one platform or both. Build behavior-based Wazuh detections, document the relevant weakness, and demonstrate appropriate prevention without breaking legitimate use. More tasks do not automatically earn more points.

Follow the [General Rules](../../general-rules.md) for team size, eligibility, the Alumni/Finalist Collaborator requirement and conduct. Divide reproduction, detection, defense and reporting work within your team; one person should keep the evidence and report current. Connect the defensive use case to a relevant SDG.

Use the [challenge cards](challenges.md) as the required task definitions and the [student guide](1_STUDENT_GUIDE.md) and [Wazuh manual](3_WAZUH_MANUAL.md) for supporting practice. Additional practice scenarios are not extra mandatory tasks; obtain organizer approval before substituting a task.

## Allowed tools and environments

- Use the designated lab VMs, Wazuh, supplied Sysmon/Suricata telemetry and approved supporting tools or scripts.
- Keep vulnerable targets on the approved isolated lab network. Confirm the Wazuh agent is active and the needed event channels arrive before developing detections.
- Do not assume you must purchase cloud hosting or expose vulnerable machines to the internet. Use the organizer-approved monitoring setup.
- Credit external rules, scripts and references; disclose significant AI assistance and explain the logic you submit.
- Use lab accounts and synthetic data only. Do not publish dashboard credentials, private keys, tokens or personal data. Redact secrets from exported evidence without removing fields needed to explain the detection.

## Authorized targets (mandatory)

Security testing is permitted **only on the designated lab environment, supplied systems and targets explicitly authorized by organizers in writing**. A personally owned or newly created system is not automatically an approved target. Stay within the authorized network, task and time window. This means no:
- Scanning or testing university infrastructure
- Attacking public websites not provided for this event
- Testing external IP addresses or other teams' systems without explicit authorization
- Exploiting third-party systems

Use supplied benign simulations, not real malware. Do not collect real credentials or disable protection outside the isolated authorized lab. This scope overrides any broader examples in supporting material.

## Submission and assessment preparation

Submit through the announced event channel by the published freeze. Prepare:

- An accessible GitHub repository with the organized submission folder, selected task IDs, lab setup and run/reproduction instructions.
- Your custom Wazuh rule XML and relevant agent, logging and prevention configuration changes, without credentials.
- A short README section per task: authorized scenario, weakness and threat/technique, detection logic, evidence, prevention, benign test and limitations.
- Exported alerts with the required fields, timestamps and task mapping; screenshots may support the exports.
- Evidence of the original behavior, detection, a changed-input rerun, a benign/false-positive test and the effect of prevention on both the attack and legitimate use. Clearly label incomplete steps.
- The common **2-3 minute backup demo video**, team details, SDG statement, Alumni Contribution note and AI/external-resource acknowledgments.

Have the approved lab and dashboard accessible for inspection. You may be asked to reproduce a task with a different lab IP, username or filename to verify that the rule detects behavior rather than memorized values. No slide deck or formal pitch is required.

## Judging criteria

Your selected task set is assessed **once out of 100**, not 100 per task. The established defensive rubric applies:

| Criterion | Points | What your team must demonstrate |
|---|---:|---|
| Detection engineering | 25 | Rules identify each selected behavior and still work when relevant lab inputs change; explain false-positive handling. |
| SIEM evidence quality | 25 | Reproducible, task-linked alert exports with the fields required by each card, relevant event context and threat/technique mapping. |
| Vulnerability identification | 20 | Correctly explain the weakness, prerequisites and observed authorized reproduction; distinguish evidence from assumptions. |
| Prevention and containment | 20 | Show targeted controls preventing or containing the behavior, with legitimate use and necessary monitoring still working. |
| Reporting and reproducibility | 10 | Clear task IDs, rule/configuration files, setup steps, benign-test results and honest limitations. |
| **Total** | **100** | **Technical assessment only; no presentation marks.** |

The [task checkpoints](challenges.md#technical-assessment-checkpoints) define the evidence for each task. Credit depends on the demonstrated completeness and quality of your selected set, not task count. Missing or unsupported parts receive no credit for those parts; incomplete detection/control chains can receive partial credit. Blocking everything does not demonstrate a valid prevention control.

Every team receives technical inspection of rules, configurations, source files, outputs and documentation. Short implementation questions and live reruns verify correctness. Demonstration clarity is not a separately scored presentation; speaking style, slides and pitch quality do not earn points.

## Scoring and tie-breakers

Approximately **two to three judges** may evaluate each team. Each independently applies the 100-point rubric; their scores are averaged for your official Track-Level score. For example: `(85 + 90 + 88) / 3 = 87.67/100`. Teams rank by their final average scores.

Ties use the higher average **Detection engineering** sub-score, then **Prevention and containment**, then **SIEM evidence quality**, followed by panel deliberation on technical evidence where necessary.

The **top three teams** qualify for the **Grand Finale**. The highest-ranked team receives **Best Cybersecurity Solution**.

## Timeline

Follow the [event schedule](../../schedule.md) and announced submission freeze. On Day 1, verify telemetry, select tasks and establish detections. On Day 2, test changed and benign inputs, apply controls, preserve evidence and prepare the technical demonstration.
