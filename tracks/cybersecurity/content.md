---
title: Content & Curriculum
parent: Cybersecurity
grand_parent: Hackathon Tracks
nav_order: 1
---

# Cybersecurity: Content & Curriculum

Prepare to **collect, detect, validate and investigate** security events for the [nine Wazuh detection exercises](challenges.md). Choose learning relevant to your **two or three approved cards**; this page is a practical pathway, not a requirement to finish every module before building.

**Use only the designated isolated lab and explicitly authorized systems.** This is defensive security learning, not general penetration testing. The [Track Rules](rules.md) define authorization, task selection, submissions and assessment.

## Learning objectives

After preparation and the bootcamp, you should be able to:

- Explain defensive cybersecurity, security monitoring and the role of a Security Operations Centre (SOC).
- Describe how a Security Information and Event Management (SIEM) system collects, processes and presents events.
- Follow a log from an endpoint through Wazuh decoding, rule matching and alert investigation.
- Read relevant Windows and Linux records, including event IDs, timestamps, accounts and source information.
- Explain custom rule conditions, parent rules, severity and event correlation.
- Use authentication monitoring and File Integrity Monitoring (FIM) where required by your cards.
- Validate detections with positive, benign and changed-input tests.
- Preserve useful evidence, explain uncertainty and restore the lab safely.

Professional cybersecurity experience is not required. Basic computer knowledge, Windows or Linux familiarity, networking concepts such as IP addresses/ports, and some command-line confidence are useful foundations.

## Learning modules

### Module 1: Introduction to Cybersecurity and SOC Operations

**Applies to: all cards.**

Learn how defensive teams protect systems, applications and information. Blue-team work includes monitoring, investigating alerts and communicating findings; a SOC analyst connects events to context rather than treating every alert as proof of compromise.

- Distinguish an event, an alert and a confirmed incident.
- Identify the affected system, observed activity and possible legitimate explanations.
- Explain what further evidence would be needed before drawing a conclusion.

**Learning checkpoint:** describe what one permitted sample event shows and what it does not establish.

### Module 2: Introduction to SIEM and Wazuh

**Applies to: all cards.**

A SIEM brings security events together for analysis. In Wazuh, **agents** collect endpoint telemetry, the **manager** decodes events and evaluates rules, the **indexer** stores searchable data, and the **dashboard** supports monitoring and investigation.

- Trace collection, processing, rule matching and alert delivery.
- Find the assigned agent, relevant time range and alert details.
- Distinguish an Active agent from verified collection of a particular event source.

**Learning checkpoint:** locate a recent event from the assigned endpoint and identify its source, decoded fields and matching rule.

### Module 3: Security Logs and Event Analysis

**Applies to: all cards; source-specific study follows the selected OS.**

Learn to read Windows Event Logs, Linux authentication logs, and relevant system/application logs. An event ID has meaning within its provider/channel; the same number in another source is not interchangeable.

- Inspect raw records alongside decoded fields.
- Identify event time, collection time, timezone, endpoint, account and source address where available.
- Check whether a field is missing, genuinely empty or simply named differently by the installed decoder.

**Learning checkpoint:** annotate a permitted record with its source, time, important fields and a short interpretation. Do not fabricate unavailable values.

### Module 4: Wazuh Detection Rules

**Applies to: all cards; frequency/timeframe correlation is central to W1B and L1B.**

Understand XML rule structure, allocated **rule IDs**, **levels**, parent rules and event/field conditions. Parent rules identify previously matched event families; verify them against the installed source and ruleset rather than copying an unrelated ID.

- Match relevant decoded fields and explain why those conditions identify the required behavior.
- Understand frequency and timeframe as correlation concepts; validate the actual trigger count/window in the installed version.
- Recognize overly broad rules, false positives and literal-value-only matching.

For illustration, consider this fictional application event, not an additional exercise:

```json
{"service": "training-app", "state": "degraded", "host": "lab-demo"}
```

Matching the appropriate source and `state` expresses a condition; matching only the demonstration hostname memorizes an example. No complete challenge rule is supplied here.

**Learning checkpoint:** explain a proposed rule's source, parent, conditions and expected output before testing it.

### Module 5: Windows Security Monitoring

**Applies to: W1B, W2B, W3B, W4B and W5B.**

| Card | Topics to learn |
|---|---|
| **W1B** | Security Event **4625**, failed-logon fields and same-source authentication correlation. |
| **W2B** | PowerShell/download behavior; configured Sysmon process creation or another approved source with full command line and parent context. |
| **W3B** | System Event **7045**, service name/path/account and the approved Windows-directory boundary. |
| **W4B** | Defender Operational events **5001** (disabled) and **5000** (re-enabled); collection and immediate protection restoration. Re-enable detection is optional. |
| **W5B** | Windows FIM baselines, monitored directories, change types and scan timing. Distinguish file monitoring from the additional Run-key Registry component using `<windows_registry>` under `<syscheck>`. |

**Learning checkpoint:** verify the selected card's event channel or FIM scope and required fields before implementing its detection. Do not assume Sysmon is configured or that Registry monitoring is instantaneous.

### Module 6: Linux Security Monitoring

**Applies to: L1B, L2B, L3B and L4B.**

| Card | Topics to learn |
|---|---|
| **L1B** | SSH failures in the actual authentication log/journal, source/account fields and custom count/window correlation. |
| **L2B** | The roles of `/etc/passwd` and `/etc/shadow`, FIM baselines and metadata-only evidence for controlled account changes. |
| **L3B** | The designated DVWA upload directory, FIM file events, web-server access logs and the relationship between upload and request evidence. |
| **L4B** | The supplied auditd feed, process execution/arguments, effective user and outbound-activity investigation. Distinguish the `www-data` account from an executable name. |

For L4B, process execution does **not** by itself prove a successful connection. Learn which actual audit/network fields establish intended destination, attempted connection or observed success, and identify missing telemetry.

**Learning checkpoint:** identify the selected source and explain what its records can support. Never export account-file contents or password hashes.

### Module 7: Detection Testing and Validation

**Applies to: all cards.**

Use the approved procedure to generate a controlled event, test the custom rule and inspect the resulting alert.

1. Record the expected behavior and required fields.
2. Use permitted rule-testing tools such as `wazuh-logtest`, then verify live collection/alert delivery where required. Sample replay alone is not an end-to-end test.
3. Check endpoint, timestamp, rule identity and card-specific information.
4. Vary an authorized account, address, filename, command or path, as appropriate.
5. Compare benign activity and record missed detections, unintended matches and repeatability.
6. Preserve sanitized source/alert evidence with expected and observed results.

Fixed monitoring scope required by a card is valid; memorizing one test artifact is not. Reducing false positives must not suppress behavior the exercise requires you to detect.

**Learning checkpoint:** produce a small positive/benign/variation test record with evidence references and an honest result.

### Module 8: Cybersecurity Ethics and Safe Lab Practices

**Applies to: all cards; cover authorization before any test activity.**

- Confirm authorized targets, actions and timing. Do not test unrelated public systems, University infrastructure outside the lab, other teams' environments, or personal/production devices.
- Verify the approved isolation arrangement; a private VM adapter alone does not establish containment.
- Use harmless artifacts and bounded, approved simulations. No real malware or unrelated offensive training is required.
- Protect credentials and private infrastructure details; redact sensitive evidence and never upload restricted logs to hosted AI services.
- Preserve evidence, remove temporary accounts/files/services and restore approved settings or snapshots. Re-enable Defender immediately after its authorized test.
- Report accidental exposure, unexpected behavior or an out-of-scope finding privately to the Technical Lead. Do not investigate further or publish sensitive details without authorization.

**Learning checkpoint:** explain the selected card's authorization boundary, evidence-handling rules and restoration procedure.

## Challenge preparation guide

### Supplied environment versus participant setup

Confirm the lab architecture, software versions, access procedures and supplied components with the Technical Lead. **No complete current-lab installer or verified inventory of provisioned sources is published here.** The inputs below are prerequisites to confirm, not promises that every component is already supplied.

- Obtain the assigned Wazuh access, endpoint/test-VM access, permitted rule IDs/files and cleanup instructions through the approved channel.
- Use existing agents and source configurations where provided. Configure missing channels, monitored paths or rules only within your permissions.
- Install endpoint/virtualization software only if the confirmed architecture requires participant installation. Do not assume each laptop must host the full Wazuh stack, both operating systems or DVWA.
- Resolve missing telemetry before relying on the card. Never invent field names, credentials, versions or evidence.

Modules **1-4 and 7-8** provide shared foundations. Add **Module 5** for selected Windows cards or **Module 6** for selected Linux cards:

| Card | Prepare and confirm | Configure and implement | Be ready to demonstrate |
|---|---|---|---|
| **W1B** | Windows log-reading basics; Security 4625 auditing/collection with source/account fields. | Verified Windows failure parent and custom same-source correlation. | Five or more failures within two minutes, count/window boundaries, required fields and a changed account/source. |
| **W2B** | Process/parent concepts; actual Sysmon or equivalent approved command-line telemetry. | Relevant collection and download-family detection. | Full command line and parent, a supported alternative download form and benign comparison using only lab files. |
| **W3B** | Service/path concepts; System 7045 collection and permission for a benign test service. | Service-event matching and the approved Windows-directory exclusion. | Name/path/account, changed service/path behavior and service cleanup. |
| **W4B** | Defender channel access, disposable VM and approved disable/restore procedure. | Missing channel collection and Event 5001 detection; optional 5000 rule. | Disabled alert, verified protection restoration and repeatability without bypassing other safeguards. |
| **W5B** | FIM/baseline basics; approved directory and Run key/view. | File monitoring plus the additional Registry component, appropriate alerts and documented scan timing. | Harmless changes, baseline distinction, changed artifacts and safe removal/restoration. |
| **L1B** | SSH log-reading basics; actual authentication feed with source/account fields. | Custom five-attempt same-source correlation, not an unverified stock threshold. | Five or more failures within two minutes, boundaries, required fields and variation. |
| **L2B** | Account-file roles; disposable VM, FIM baseline and temporary-account permissions. | Both protected paths and metadata-only change detection. | Required file-change alerts, another approved temporary account and cleanup without exposing hashes. |
| **L3B** | Upload/request concepts; designated DVWA, actual upload path and web access logs. | Scoped upload FIM and PHP/PHTML request detection. | Each signal, their path/time relationship and changed filename. Either approach is partial coverage; both support full coverage. |
| **L4B** | Process/effective-user basics; the actual supplied audit feed and approved lab listener. | Map real decoded fields to identity, executable/arguments and available destination/network evidence. | Approved outbound activity and variation, with claims limited to what execution/network records establish. |

The [challenge cards](challenges.md) contain the full acceptance criteria and safety procedures. Recommended pairings are optional; confirm any operating-system restrictions before selecting your two or three cards.

## Day 1 bootcamp and event alignment

### Essential bootcamp topics

The bootcamp should get teams started, **not attempt all eight modules in full**:

1. **Safe scope first:** the essential authorization and credential/restoration points from Module 8.
2. **Monitoring foundations:** a short introduction to SOC work and the Wazuh event-to-alert path from Modules 1-2.
3. **Read one permitted event:** source, fields, timestamp and interpretation from Module 3.
4. **Explain and test a condition:** rule structure and one simple non-solution example from Module 4, followed by the validation loop from Module 7.
5. **Move into selected-card work:** consult only the relevant Windows/Linux material from Modules 5-6 and verify its prerequisites.

**First working checkpoint:** locate the selected source event, explain the proposed rule and generate an initial validated alert. Ask a mentor promptly if the source is missing; a full SIEM installation is not assumed to fit into the introductory session.

### Recommended pre-event preparation

- Read the [Challenges](challenges.md) and [Track Rules](rules.md), identifying likely cards and relevant operating-system skills.
- Refresh basic Windows/Linux administration, networking, command-line use and reading structured records.
- Arrange the confirmed tools/access and practice opening a permitted sample log. Do not run simulations on personal devices to prepare.
- Review the relevant sections of [Curated Resources](resources.md) rather than installing every listed tool.

These are preparation recommendations, not extra assessed exercises or permission to complete a finished competition solution in advance. If joining on the day, prioritize the essential bootcamp sequence and mentor-supported setup.

### Development and additional learning

**Day 1:** attend the briefing, confirm selection and access, verify sources and build the first working detections. Deepen the selected Module 5/6 topics as needed.

**Day 2:** finish the approved cards, validate positive/benign/variation cases, investigate alerts, preserve evidence and restore temporary changes before assessment.

Advanced decoder work, broader threat mapping and supplementary bank-lab material are additional study, not extra mandatory cards. Suricata, SCA hardening, active response and extra simulations are not prerequisites for the nine exercises and still require explicit authorization if used.

## Preparing for assessment

Keep the selected card IDs, rules/configuration changes, required alert fields, test records, investigation notes and limitations together. Your **whole selected task set is assessed once out of 100**, using the current [published rubric](rules.md#judging-criteria); individual judges' scores are averaged.

Technical demonstrations verify the implementation. **No slide deck or formal Track-Level pitch is required, and presentation quality earns no marks.** Follow the [submission requirements](rules.md#submission-and-assessment-preparation), including the common backup video.

Continue with [Curated Resources](resources.md) for official references and the [Wazuh Analyst Playbook](3_WAZUH_MANUAL.md) for supporting operating guidance.
