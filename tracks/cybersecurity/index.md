---
title: Cybersecurity
nav_order: 5
parent: Hackathon Tracks
has_children: true
---

# Cybersecurity

## About the Cybersecurity Track

Cybersecurity helps protect the digital infrastructure, systems, applications and information that people rely on every day. At the Zetech Forge Alumni & Student Hackathon 2026, this track brings students and alumni together to practice **defensive security, security monitoring, threat detection, log analysis and detection engineering**.

You will work like a **Security Operations Centre (SOC)** team: examine events, identify suspicious activity and explain what the evidence shows. **Wazuh** is the primary **Security Information and Event Management (SIEM)** platform. Endpoint agents collect events, the manager evaluates detection rules, and the dashboard makes alerts available for investigation.

The exercises cover Windows and Linux environments. Teams investigate controlled, simulated security activities, develop detection rules and validate alerts. This is **not a general penetration-testing competition**.

**Test only supplied or explicitly authorized lab systems.** University infrastructure outside the designated lab, unrelated public systems and other teams' systems without permission are out of scope. Use harmless lab artifacts and never publish credentials or sensitive logs.

## Who Should Participate?

This track welcomes students interested in cybersecurity and defensive security, aspiring SOC analysts, SIEM and security-monitoring enthusiasts, Windows/Linux administrators, and anyone curious about digital forensics, threat detection or incident investigation. **Professional cybersecurity experience is not required.**

Useful foundations are basic computer-system knowledge, familiarity with Windows or Linux, basic networking concepts such as IP addresses and ports, some command-line familiarity, and an interest in investigating events.

The event bootcamp introduces authorized lab practice, SIEM concepts, Wazuh navigation, reading events, basic detection-rule development and alert validation. Learn the additional log sources needed for your selected exercises as you build; you do not need to master every tool first.

## What You Will Learn

Through your selected exercises, you will gain practical experience in:

- SIEM systems and Wazuh deployment, agent, collection and monitoring concepts.
- Security event and log analysis in Windows and Linux.
- Custom Wazuh detection rules and authentication monitoring.
- PowerShell and process monitoring using the available telemetry.
- File Integrity Monitoring (FIM) for protected files and registry locations.
- Web application security monitoring using the designated lab.
- Alert validation, changed-input testing and false-positive reduction.
- Evidence collection and security investigation, including uncertainty and legitimate explanations for an alert.

The exercises provide different pathways through these topics; no team is expected to complete every learning area or install the entire monitoring stack independently.

## Challenge Structure

There are **nine Wazuh detection exercises**, organized by operating system rather than difficulty:

| Category | Exercises |
|---|---|
| **Windows: five cards (W1B-W5B)** | Failed logons, PowerShell download behavior, service installation, Defender protection changes, and file/registry integrity monitoring. |
| **Linux: four cards (L1B-L4B)** | SSH failures, account-file changes, web upload/request activity, and outbound web-server connections. |

**Complete two or three approved exercises properly**, with working detections and clear evidence, rather than rushing through all nine. The operating-system selection policy still requires Technical Lead confirmation: do not assume a compulsory Windows/Linux mix or named mandatory card.

For each selected exercise:

1. Understand the controlled scenario and authorized target.
2. Identify and verify the relevant event or log source.
3. Develop or modify a Wazuh detection rule.
4. Generate the expected alert using the approved lab procedure.
5. Verify its accuracy, required fields and investigation context.
6. Test an approved variation of the activity and compare benign behavior.

The [recommended pairings](challenges.md#recommended-pairings), such as authentication or integrity-focused combinations, are **optional suggestions**, not mandatory selections. The existing challenge cards define the required behavior.

## Technologies and Tools

Use the tools relevant to your selected cards and the **actual approved lab configuration**:

| Tool or source | Role and official reference |
|---|---|
| **Wazuh SIEM and custom rules** | Collect, analyze and investigate events. Start with the [Wazuh quickstart](https://documentation.wazuh.com/current/quickstart.html) and [custom-rule guide](https://documentation.wazuh.com/current/user-manual/ruleset/rules/custom.html). |
| **Windows Security Event Logs and Windows Defender** | Authentication and protection-change telemetry. See [Microsoft's failed-logon event reference](https://learn.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4625) and the [task-specific collection guidance](resources.md#windows-and-linux-source-references). |
| **Sysmon, where configured** | Process, command-line and parent context. See [Microsoft Sysmon](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon). |
| **Linux authentication logs and auditd** | SSH events and approved audit/process records. See [Wazuh log collection](https://documentation.wazuh.com/current/user-manual/capabilities/log-data-collection/configuration.html) and the [Ubuntu auditd manual](https://manpages.ubuntu.com/manpages/noble/man8/auditd.8.html). |
| **File Integrity Monitoring** | Detect changes to selected files and Windows registry locations. See [Wazuh FIM](https://documentation.wazuh.com/current/user-manual/capabilities/file-integrity/index.html). |
| **DVWA** | The deliberately vulnerable web application used only for designated lab exercises. See the [official DVWA repository](https://github.com/digininja/DVWA). Never expose it publicly. |
| **Windows and Linux virtual machines** | Isolated endpoints for approved activities and event collection. See [Wazuh agent installation](https://documentation.wazuh.com/current/installation-guide/wazuh-agent/index.html) for supported endpoint setup. |

Confirm VM/server allocation, permissions and required log sources before starting. Sysmon, auditd and DVWA are source-dependent, not universal installation requirements. A complete nine-exercise installer is not published here; no paid hosting or production credentials are required.

## How the Competition Works

The hackathon takes place on **12-13 November 2026**:

- **Day 1:** introduction, foundational bootcamp, challenge briefing, environment preparation and solution development.
- **Day 2:** continued implementation, positive/benign/changed-input testing, evidence preparation, technical demonstrations and Track-Level Judging.

Your selected exercise set receives **one technical score out of 100**, not 100 per exercise. Approximately **two to three judges** independently assess the implementation, detection rules, alert outputs, configuration and supporting evidence. Their scores are **averaged**, and teams rank by that final average.

Use the current [100-point rubric](rules.md#judging-criteria) for detection functionality, rule quality/fields, generalization, telemetry, reliability and reproducible evidence, and the [published tie-breakers](rules.md#scoring-and-tie-breakers). The whole selected set is assessed once, not by adding or equally averaging per-exercise scores.

**No formal slide presentation or pitch is required.** Demonstrations and technical questions verify implementation; presentation quality earns no separate marks. The **three highest-scoring teams qualify for the Grand Finale**, and the highest-ranked team receives **Best Cybersecurity Solution**.

Prepare rule/configuration files, task-linked alert/log exports, test results and investigation notes, together with the common submission items in the rules. Extra task count, blocking and supplementary bank-lab scenarios do not automatically earn additional points.

## Navigation

- [Challenges](challenges.md): the nine cards, expected detections and optional pairings.
- [Track Rules & How to Compete](rules.md): authorization, task selection, submissions and scoring.
- [Content & Curriculum](content.md): foundations and task-specific preparation.
- [Curated Resources](resources.md): official references and configuration guidance.
- [Cyber Defence Participant Guide](1_STUDENT_GUIDE.md): the practical access-to-evidence workflow for the nine cards.
- [Wazuh Analyst Playbook](3_WAZUH_MANUAL.md): supporting operating instructions for the assigned environment; supplementary sections do not add mandatory tasks.
