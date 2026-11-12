---
title: Track Rules & How to Compete
parent: Cybersecurity
grand_parent: Hackathon Tracks
nav_order: 3
---

# Cybersecurity: Track Rules & How to Compete

## Format

This is a **task-based defensive security track**, not a difficulty-tier or flags competition. Work from the **nine published lab tasks: five Windows and four Linux**. Build behavior-based Wazuh detections, validate them and investigate the evidence. More tasks do not automatically earn more points.

Follow the [General Rules](../../general-rules.md) for team size, eligibility, the Alumni/Finalist Collaborator requirement and conduct. Divide reproduction, detection, defense and reporting work within your team; one person should keep the evidence and report current. Connect the defensive use case to a relevant SDG.

Use the [challenge cards](challenges.md) as the required task definitions and the [student guide](1_STUDENT_GUIDE.md) and [Wazuh manual](3_WAZUH_MANUAL.md) for supporting practice. Additional practice scenarios are not extra mandatory tasks; obtain organizer approval before substituting a task.

### Task selection and confirmation

- The existing cards/guide recommend **two or three selected exercises**. This is the documented planning target, not evidence of an approved pass/fail completion minimum.
- The materials do not explicitly define a compulsory minimum number of completed cards, required Windows/Linux combination or named compulsory card. The Technical Lead must confirm these conditions at the briefing, before teams rely on them.
- Declare your intended task IDs and confirm access to their prerequisites. One-platform pairings are already listed, so do not assume every team must complete both Windows and Linux.
- Additional cards are optional practice unless the Technical Lead publishes a different approved selection rule. They do not increase the 100-point maximum or automatically outweigh stronger evidence.
- The published selection conditions and rubric apply consistently across Windows/Linux teams; technical complexity does not introduce a multiplier. Do not assume credit simply for attempting more cards.

## Lab access and readiness

| Component | Purpose | What to confirm before starting |
|---|---|---|
| Wazuh manager/server, indexer and dashboard | Decode/evaluate events, store and investigate alerts. | Assigned address/account, installed version, visible team agents and the permitted rule-deployment route. A shared server or cloud instance is not guaranteed by this repository. |
| Endpoint agent | Forward the chosen Windows/Linux telemetry. | Assigned endpoint, enrollment/connection, permitted agent-configuration access and recent events from that agent. |
| Windows endpoint | Security/System events, selected process telemetry, Defender channel and/or FIM according to the card. | Correct audit/channel collection and the fields required by the selected tasks. Sysmon is a possible source for W2B, not a universal extra exercise. |
| Linux endpoint | SSH authentication, FIM, web access or audit records according to the card. | Log paths, monitored directories and the supplied/approved audit configuration for L4B. DVWA is needed only for the existing web cards. |
| Approved event source/test VM | Generate the card's permitted lab test or provide an approved event sample. | Written scope, accounts, addresses, timing and cleanup instructions. Never substitute a live external target. |

Use the allocated/preconfigured environment where available. If installing central components is explicitly approved, follow the version-matched [official quickstart](https://documentation.wazuh.com/current/quickstart.html): its smallest listed all-in-one deployment recommends **4 vCPU, 8 GiB RAM and 50 GB storage for 1-25 agents/90 days of data**. This is sizing guidance, not a promise of event hardware or a requirement for each laptop. Confirm capacity and network isolation with the Technical Lead; you are not required to buy hosting.

No complete nine-task lab installer is published in this track. The separate ransomware-behaviour VM is supplementary and does not establish that Wazuh, endpoint agents, required event channels or isolation are ready. Do not boot or use optional lab definitions without approval and a network-scope check.

## Allowed tools and environments

- Use the designated endpoints, Wazuh and the log sources needed for your selected cards. Sysmon/equivalent telemetry, auditd or web logs depend on the card; Suricata, SCA and active response are not mandatory components of the current nine-card set.
- Keep vulnerable targets on the approved isolated lab network. Confirm the Wazuh agent is active and the needed event channels arrive before developing detections.
- Do not assume you must purchase cloud hosting or expose vulnerable machines to the internet. Use the organizer-approved monitoring setup.
- Credit external rules, scripts and references; disclose significant AI assistance and explain the logic you submit.
- Use lab accounts and synthetic data only. Do not publish dashboard credentials, private keys, tokens or personal data. Redact secrets from exported evidence without removing fields needed to explain the detection.
- Use only your allocated rule IDs/files and deployment permissions. Do not overwrite another team's rules, restart a shared manager or change shared collection/network settings without explicit permission.

## Authorized targets (mandatory)

Security testing is permitted **only on the designated lab environment, supplied systems and targets explicitly authorized by organizers in writing**. A personally owned or newly created system is not automatically an approved target. Stay within the authorized network, task and time window. This means no:
- Scanning or testing university infrastructure outside the designated authorized lab
- Attacking public websites not provided for this event
- Testing external IP addresses or other teams' systems without explicit authorization
- Exploiting third-party systems

Use only the supplied or approved exercise procedure and harmless lab artifacts, not real malware. Unauthorized scanning, exploitation and disruption are prohibited even if a target is reachable. Do not collect real credentials or disable protection outside the isolated authorized lab. Keep logs/access details within their approved audience, restore lab changes as instructed and report accidental out-of-scope contact immediately. This scope overrides broader examples in supporting material.

## Submission and assessment preparation

Submit through the announced event channel by the published freeze. Prepare:

- An accessible GitHub repository with the organized submission folder, selected task IDs, lab setup and run/reproduction instructions.
- Your custom Wazuh rule XML and the relevant agent/log-collection/FIM configuration changes, without credentials.
- A short README section per task: authorized scenario, log source, configuration, detection logic, required event fields, investigation findings, tests and limitations.
- Exported alerts with the required fields, timestamps and task mapping; screenshots may support the exports.
- Evidence of the approved test event, detection, a changed-input rerun and a benign/false-positive test. Include expected/actual results and explain missing detections, noise and incomplete steps.
- The common **2-3 minute backup demo video**, team details, SDG statement, Alumni Contribution note and AI/external-resource acknowledgments.

Have the approved lab and dashboard accessible for inspection. You may be asked to reproduce a task with a different lab IP, username or filename to verify that the rule detects behavior rather than memorized values. No slide deck or formal pitch is required.

**Supplementary:** screenshots help illustrate alert exports; extra dashboards, threat mappings, prevention/containment experiments and the broader bank-lab scenarios are not additional mandatory deliverables. Any optional activity still requires authorization. Do not submit credential files, password hashes, real personal data or logs from systems outside the lab.

## Judging criteria

Your selected task set is assessed **once out of 100**, not 100 per task. The same maximum applies to every permitted Windows/Linux selection:

| Criterion | Points | What your team must demonstrate |
|---|---:|---|
| Detection accuracy and coverage | 30 | Detect the selected cards' required behaviors and fields; demonstrate coverage rather than merely showing a rule exists. |
| Detection rule quality, specificity and robustness | 20 | Appropriate conditions/correlation, useful severity, changed-input resilience and controlled false positives without hardcoding one test artifact. |
| Validation, testing and evidence quality | 15 | Repeatable positive, benign and changed-input tests with timestamps, expected/observed results and traceable alerts/logs. |
| Investigation quality and alert interpretation | 15 | Explain affected endpoint, event context, significant fields, security meaning, uncertainty and legitimate alternatives; an alert alone is not proof of compromise. |
| Log-source collection and system configuration | 10 | Correct source/channel/FIM/audit setup, functioning collection and fields needed to support the selected detections. |
| Documentation and reproducibility | 10 | Clear task IDs, rule/configuration files, run/test steps, evidence mapping and honest limitations. |
| **Total** | **100** | **Technical assessment only; no presentation marks.** |

The [task checkpoints](challenges.md#technical-assessment-checkpoints) define the evidence for each task. Credit depends on the demonstrated completeness and quality of the confirmed selection, not task count. Missing or unsupported parts receive no credit for those parts; incomplete detection/evidence chains can receive partial credit. Blocking everything is not a substitute for detection and cannot be used to manufacture a successful result.

Every team receives technical inspection of rules, configurations, source files, outputs and documentation. Short implementation questions and live reruns verify correctness. Demonstration clarity is not a separately scored presentation; speaking style, slides and pitch quality do not earn points.

## Scoring and tie-breakers

Approximately **two to three judges** may evaluate each team. Each independently applies the 100-point rubric; their scores are averaged for your official Track-Level score. For example: `(85 + 90 + 88) / 3 = 87.67/100`. Teams rank by their final average scores.

Ties use the higher average **Detection accuracy and coverage** sub-score, then **Detection rule quality, specificity and robustness**, then **Validation, testing and evidence quality**, followed by panel deliberation on technical evidence where necessary.

The **top three teams** qualify for the **Grand Finale**. The highest-ranked team receives **Best Cybersecurity Solution**.

## Timeline

Follow the [event schedule](../../schedule.md) and announced submission freeze. On Day 1, confirm selection rules/lab access, verify telemetry and establish detections. On Day 2, test changed and benign inputs, investigate alerts, preserve evidence and prepare the technical demonstration.
