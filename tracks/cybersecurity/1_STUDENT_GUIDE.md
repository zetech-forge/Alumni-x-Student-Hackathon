---
title: Cyber Defence Participant Guide
parent: Cybersecurity
grand_parent: Hackathon Tracks
nav_order: 5
---

# Cyber Defence Participant Guide

## What this guide covers

This is the public working guide for the **nine Wazuh detection-engineering cards: five Windows and four Linux**. It supports the [Challenges](challenges.md) and [Track Rules](rules.md); it is not an answer key, a lab installer or a separate bank-security assignment.

Complete **two or three approved cards**. The Technical Lead must confirm any compulsory cards or operating-system selection restrictions. [Recommended pairings](challenges.md#recommended-pairings) are optional suggestions, not selection rules.

Historical bank-lab scenarios are not additional approved exercises. Port scanning, reverse shells, ransomware-behavior simulations, success-after-failures detections, SCA hardening and active response are not required by the current cards. Their presence in older supporting material does not authorize them.

## 1. Confirm access and safe scope

- Obtain assigned lab access through the private organizer channel: endpoints, Wazuh dashboard, authorized test VM/application, permissions and cleanup procedure.
- Confirm actual versions and sources. A diagram or repository file is not proof that a ready environment is supplied.
- Use only supplied or explicitly authorized lab systems. Do not test University infrastructure outside the lab, unrelated internet targets, other teams' systems or personal/production devices.
- Confirm the lab's isolation with the mentor. A private VM adapter alone does not establish containment.
- Never publish credentials, private infrastructure details or sensitive logs.

The [lab-readiness guidance](rules.md#lab-access-and-readiness) distinguishes assigned components from installation work. Do not assume every laptop must run the full stack, both operating systems or DVWA.

## 2. Understand the monitoring path

```text
Authorized endpoint/test activity
            |
            v
Required Windows/Linux log or FIM source
            |
            v
Wazuh collection -> decoding -> rule matching
            |
            v
Indexed alert -> dashboard investigation -> sanitized evidence
```

Wazuh agents collect the configured endpoint sources. The manager decodes events and evaluates rules; the indexer/dashboard support searching and investigation. Sysmon and auditd are source-dependent, not universal extra installations. Suricata is not required by the nine cards.

Check the assigned agent identity and recent source events. **Active status alone does not prove that the required channel or fields arrive.**

## 3. Use the actual card requirements

| Cards | Focus and important distinction |
|---|---|
| **W1B / L1B** | Five or more failures from one source within two minutes, with source IP and username. Failures only; no successful login afterwards is required. Verify the installed parent and actual trigger count. |
| **W2B** | The download-behavior family, with full command line and parent context from the configured process source. Use benign lab files. |
| **W3B** | Event 7045 service installation outside the approved Windows directory, with name/path/account. Legitimate software can meet this condition too. |
| **W4B** | Defender Operational Event 5001, immediate restoration and verified protection status. Event 5000 detection is optional, not extra points. |
| **W5B** | Harmless protected-location changes, baseline distinction and the additional Run-key Registry component for complete coverage. Confirm Registry view and scan timing. |
| **L2B** | FIM on both account files, using approved temporary-account changes and metadata-only evidence. Never export contents or password hashes. |
| **L3B** | Upload-directory FIM and PHP/PHTML request detection in the designated DVWA environment. One approach is partial coverage; both support full coverage. No real shell is needed. |
| **L4B** | Outbound activity associated with the web-server identity using verified audit/process/network fields. Execution alone does not establish a successful connection. |

Use the [full cards](challenges.md) for precise telemetry, field, variation and cleanup requirements. No validated L4B audit sample or complete nine-card installer is supplied by this guide; ask the Technical Lead to resolve missing prerequisites.

## 4. Build, validate and investigate

For each selected card:

1. Locate a permitted source event and inspect its raw/decoded fields.
2. Explain the behavior your rule must identify and the required alert information.
3. Configure only authorized collection/rule changes, using allocated IDs/files.
4. Test with the approved Wazuh tools and deployment procedure. Do not restart a shared manager independently.
5. Generate the original approved activity and inspect the resulting alert.
6. Repeat with an approved changed account, address, filename, command or path, as appropriate.
7. Compare benign behavior; record missed detections, unintended matches and relevant count/window or scan timing.
8. Explain the endpoint, activity, significant fields, legitimate alternatives and what remains uncertain.
9. Preserve permitted evidence, then clean up and restore the approved state.

Match behavior rather than memorizing one sample. Required fixed monitoring paths are valid scope. `wazuh-logtest` proves sample matching, not live collection or dashboard delivery; distinguish these results.

AI assistance is allowed with disclosure. Share only sanitized, permitted information and be able to explain and validate every submitted rule.

## 5. Organize your evidence

An illustrative structure, not a supplied starter bundle:

```text
team_submission/
  README.md        selected cards, setup, logic, tests, findings, limitations
  rules/           custom Wazuh XML
  configs/         relevant non-secret configuration changes
  evidence/        sanitized events/alerts and expected/observed test results
```

Keep required fields, timestamps, endpoint/rule IDs and task mapping. Screenshots may illustrate exports; they do not replace missing required information. Include variation/benign results and restoration evidence. Protect restricted records rather than putting them into a public repository.

Follow the [submission requirements](rules.md#submission-and-assessment-preparation), including the common backup video, team details, SDG statement, Alumni Contribution note and AI/external-resource acknowledgments.

## 6. Work through the two days

- **Day 1:** introduction/bootcamp, task briefing, selection/access confirmation, source verification and initial working detections.
- **Day 2:** complete the approved cards, validate results, investigate alerts, preserve evidence and restore temporary changes before assessment.

Divide collection, detection, testing and documentation work sensibly. Dedicated attacker/defender/scribe roles are not extra eligibility requirements. Ask a mentor promptly if telemetry or access is missing.

## 7. Prepare for technical assessment

The **whole selected task set is scored once out of 100**, using the current [Track Rules rubric](rules.md#judging-criteria), not by adding or equally averaging per-card scores. Individual judges' team scores are averaged; the top three teams qualify for the Grand Finale and the highest-ranked team receives **Best Cybersecurity Solution**.

Be ready to show the approved activity, source event, custom rule, generated alert, required fields and variation test, and explain the result. **No slides or formal pitch are required; demonstrations are technical evidence, not separately scored presentations.**

Continue with [Content & Curriculum](content.md), [Curated Resources](resources.md) and the public [Wazuh Analyst Playbook](3_WAZUH_MANUAL.md).
