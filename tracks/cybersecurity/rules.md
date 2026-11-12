---
title: Track Rules & How to Compete
parent: Cybersecurity
grand_parent: Hackathon Tracks
nav_order: 3
---

# Cybersecurity: Track Rules & How to Compete

## Track format

The Cybersecurity track is a **defensive Wazuh detection-engineering competition** with **nine exercises: five Windows and four Linux**. Teams investigate controlled security activities, configure the necessary monitoring, build custom detections and validate their alerts. This is not a capture-the-flag or open-ended penetration-testing competition.

Complete **two or three approved exercises** from the [challenge cards](challenges.md). Focus on working detections, reliable evidence and clear explanations rather than task count. The selected set receives **one assessment out of 100 points**.

Team size, eligibility, the Alumni/Finalist Collaborator requirement, originality and conduct follow the [General Rules](https://zetech-forge.github.io/Alumni-x-Student-Hackathon/general-rules.html). Explain your team's own contribution and connect the defensive use case to a relevant SDG.

### Task selection and confirmation

- Declare the two or three card IDs your team intends to complete and confirm their prerequisites with the Technical Lead.
- The operating-system selection policy and any named compulsory cards are **not confirmed here**. Obtain the Technical Lead's decision before relying on either a mixed-platform or single-platform selection; do not assume one is compulsory.
- [Recommended pairings](challenges.md#recommended-pairings) are **optional suggestions**, not mandatory selections or proof of an approved operating-system restriction. They help teams combine related authentication, integrity or web-monitoring skills.
- Use the nine existing card objectives. Supporting bank-lab material does not create extra mandatory exercises, and substituting an exercise requires explicit approval.
- More exercises, a particular operating system or a more complex setup do not automatically increase the maximum score.

## Authorized targets (mandatory)

**All offensive or simulated security activities must remain within systems supplied by organizers or explicitly authorized in writing for this competition.** Use only the approved attacker VM, monitored endpoints, lab applications and authorized infrastructure, within the assigned network, task and time window.

The following are prohibited:

- Scanning or testing University infrastructure outside the designated lab.
- Testing public websites not provided and authorized for the competition.
- Attacking external IP addresses outside the authorized lab scope.
- Exploiting third-party systems.
- Accessing another team's lab environment without explicit permission.
- Running simulated attack activities against personal or production devices.
- Collecting, using or sharing unauthorized credentials or sensitive system data.

A reachable target or personally owned VM is not automatically authorized. A callback destination must be an approved host on the isolated lab network, not an unrelated internet address.

Testing serves **defensive learning and detection validation only**. Use harmless artifacts, never real malware. Do not expose vulnerable applications publicly, disrupt shared infrastructure or bypass security controls beyond the approved exercise. Temporary Defender changes are allowed only on the designated disposable VM and must be reversed immediately after the test.

Preserve evidence before cleanup, remove your test artifacts and restore the approved clean state. Stop and report accidental out-of-scope contact, exposed credentials or unexpected disruption to the Technical Lead. These boundaries override broader examples in supporting guides.

## Lab access and readiness

Confirm what is supplied before installing anything. The repository does not establish a complete, ready-to-run nine-exercise lab or promise each team a dedicated server.

| Component | Purpose | Supplied access or participant setup |
|---|---|---|
| Wazuh manager, indexer and dashboard | Evaluate rules, store events and investigate alerts. | Obtain the assigned access route privately if supplied. Install central components only when explicitly required and approved. |
| Windows monitored endpoint and agent | Collect Security/System events, Defender events and selected process/FIM telemetry. | Confirm the allocated VM or approved installation instructions, version and collection permissions. |
| Linux monitored endpoint and agent | Collect SSH, FIM, web and audit events for selected cards. | Confirm the endpoint, actual log paths, permissions and required sources. |
| Approved attacker/test VM | Generate only the selected cards' authorized test activities. | Use the assigned image/account and bounded test procedures; no unrelated offensive toolkit is required. |
| DVWA application | Provide the controlled web-upload and outbound-activity scenarios. | Needed for the relevant web cards only; confirm its lab address, upload path and server logs. |
| Windows channels and Sysmon where configured | Provide authentication, service, Defender and process fields. | Inspect existing settings; add only missing, authorized collection. Sysmon is not universally required. |
| auditd and FIM configurations | Provide the audit/process/network or file/registry evidence required by a card. | Verify the actual supplied configuration and decoded events. L4B's expected preconfigured feed must not be assumed present. |

The Technical Lead must verify **actual versions, access procedures, isolation, source configurations and deployment permissions**. Obtain credentials through the private organizer channel; do not publish them or private infrastructure details.

Computer and virtualization requirements depend on the confirmed architecture. A remotely accessed lab and locally hosted VMs have different needs. Follow the confirmed image/hypervisor and CPU/RAM/storage requirements if local virtualization is required; **no unverified universal hardware minimum is specified here**. Do not assume every laptop must host the full stack or that participants must buy cloud hosting.

Before developing a rule, verify the agent identity and recent events from the selected source. Active agent status alone is not proof of correct collection. Raise missing fields or inaccessible infrastructure with the mentor rather than inventing evidence or silently changing the exercise.

## Allowed tools and technologies

Within the approved lab and your assigned permissions, you may use:

- Wazuh monitoring, its dashboard, custom XML rules and permitted rule-testing tools such as `wazuh-logtest`.
- Windows Security/System Event Logs, the Defender Operational channel and approved process telemetry such as configured Sysmon or process-creation auditing.
- Linux authentication logs, the approved auditd feed and relevant web-server logs.
- Wazuh syscheck/FIM for the assigned files, directories and Registry locations.
- The supplied DVWA instance and approved Windows/Linux administration tools needed for the existing exercise procedures.
- An editor, Git and documentation tools to maintain rules, configurations, results and explanations.

You may develop custom detections and modify relevant monitoring configurations **only as required by selected cards and within your assigned scope**. Use allocated rule IDs/files; do not overwrite another team's rules, restart a shared manager or change shared network/collection settings without explicit permission.

Credit reused rules, libraries and references, disclose significant AI assistance and be able to explain your implementation. Never send credentials or sensitive logs to hosted AI services. Additional offensive tools, active response, SCA hardening, Suricata and supplementary bank scenarios are not requirements of the nine exercises.

## Task completion requirements

For **each of your two or three approved exercises**, demonstrate:

1. The authorized original test activity.
2. Its relevant security event or log reaching the monitoring system.
3. A functioning custom detection rule.
4. A generated Wazuh alert with the card's required fields.
5. A changed-input test showing that the rule detects behavior, not one memorized account, address or filename.
6. A benign comparison, recorded expected/observed results and an explanation of limitations.
7. Completion of the approved cleanup/restoration procedure.

Use the [full challenge cards](challenges.md) for source requirements and procedures. The measurable acceptance outcomes are:

| Card | Required technical outcome |
|---|---|
| **W1B** | Detect five or more Windows 4625 failures from one source within two minutes; alert includes source IP and username. Validate the count/window and changed input. |
| **W2B** | Detect the specified PowerShell/download family using the configured process source; alert includes full command line and parent process. Demonstrate another supported download form. |
| **W3B** | Detect System Event 7045 for a service binary outside the approved Windows directory; include service name, binary path and account. Validate changed service/path inputs. |
| **W4B** | Detect Defender Operational Event 5001 and verify protection restoration. Event 5000 re-enable detection is optional within the same rubric, not extra points. |
| **W5B** | Detect harmless changes in the monitored protected location, distinguish baseline entries and validate changed artifacts. The additional Run-key Registry component contributes to complete task coverage. |
| **L1B** | Detect five or more SSH failures from one source within two minutes; include source IP and username. Validate the actual trigger count, window and changed input. |
| **L2B** | Configure and validate FIM for both `/etc/passwd` and `/etc/shadow`, with relevant change alerts and a temporary-account variation. Do not expose sensitive content or hashes. |
| **L3B** | Demonstrate upload-directory FIM and PHP/PHTML request detection in the web logs. Either working approach gives partial coverage; both are needed for full coverage, with the required evidence/tests. |
| **L4B** | Detect approved outbound activity attributable to the web-server identity using verified telemetry and destination context. Execution-only records must not be presented as proof of a successful connection. |

Use assigned rule/source details, not unverified copied rule numbers. If an approved sample replaces live activity, label it clearly and obtain approval for that arrangement; sample replay alone does not demonstrate live collection.

## Submission and assessment preparation

Submit through the announced event channel by the published freeze in the [Schedule](../../schedule.md). Follow the main [General Rules submission requirements](https://zetech-forge.github.io/Alumni-x-Student-Hackathon/general-rules.html#what-every-team-submits), including:

- A GitHub repository, README with setup/run instructions, technology stack and known limitations.
- The required **2-3 minute backup demo video**, even when a live demonstration is planned; a live URL only if applicable.
- Team details, the Alumni/Finalist Collaborator's identity, an Alumni Contribution note, SDG statement and AI-tool disclosure.

Add these Cybersecurity-specific materials:

- Selected card IDs and a short section per exercise explaining the authorized scenario, source, implementation, required fields and investigation findings.
- Custom Wazuh rule XML and relevant non-secret endpoint/collection/FIM/audit configurations or documented configuration changes.
- Sanitized alert exports/source context with required fields, timestamps and task mapping. Screenshots may support the records, not replace missing required information.
- Positive, benign and variation-test results, including relevant count/window, scan-timing or process/network checks.
- Reproduction instructions, expected/observed outcomes, known limitations and cleanup/restoration evidence.

Do not submit real passwords, tokens, private keys, password hashes, personal information or unauthorized system data. Redact secrets without removing the information needed to understand the detection. Keep restricted lab evidence within its approved audience rather than publishing it in a public repository.

Have the approved lab, dashboard, source files and test evidence ready for inspection. **The backup video is a submission artifact, not a separately scored pitch. No pitch deck or formal oral presentation is required for Track-Level Judging.** A reference to presentation materials for another event stage does not create a Track-Level presentation requirement.

## Judging criteria

Use this **100-point technical rubric** for the selected exercise set. The challenge cards define the required outcomes; they do not create additional point pools.

| Criterion | Points | What your team must demonstrate |
|---|---:|---|
| **Detection functionality and accuracy** | 35 | The selected cards' required behaviors produce the expected alerts. Show the original activity, matching event and correct detection; distinguish what happened from unsupported compromise or connection claims. |
| **Detection rule quality and required fields** | 20 | Appropriate event/source conditions, correlation and readable rule logic, with every field required by the selected cards present and correctly interpreted. |
| **Generalization and variation testing** | 15 | Repeat the required detections with approved changed accounts, addresses, filenames, commands or paths as appropriate. Rules must not depend on one test artifact; fixed required monitoring scope is legitimate. |
| **Log-source configuration and telemetry** | 10 | Correct source/channel/FIM/audit configuration and functioning collection, with the fields and process context needed by the selected detections. |
| **False-positive handling and reliability** | 10 | Repeatable results, appropriate benign comparisons and documented count/window or scan behavior. Explain noise and failures; do not suppress required cases merely to make the dashboard quiet. |
| **Evidence, documentation and reproducibility** | 10 | Traceable sanitized records, selected card IDs, rules/configurations, expected/observed results, clear run steps, interpretation, limitations and restoration evidence. |
| **Total** | **100** | **Technical assessment only; no presentation marks.** |

Full credit requires the relevant outcomes and evidence across the declared selection. Incomplete or inconsistent work receives partial credit for supported requirements; missing or unsupported work earns no credit for the affected requirement. A legitimate activity can still match a card's required condition: explain its context rather than silently excluding it.

### How the selected exercises are assessed together

Each judge applies the rubric **once to the whole selected task set**:

1. Review the required outcomes and evidence across the two or three declared cards.
2. Award one score for each of the six criteria above, within its point limit.
3. Add those six criterion scores to obtain that judge's team score out of 100.

**Do not add per-exercise scores or average equally weighted task scores.** Three selected cards do not create a higher maximum than two. The current method does not assign equal numerical weights to cards; any future equal-task-weighting proposal requires Technical Lead confirmation of comparable effort and publication before teams rely on it.

Judges verify rules, configurations, alert outputs, source evidence and reproducibility through technical inspection and short implementation questions. You may be asked to repeat an approved activity or variation. Demonstrations are evidence, not separately scored presentations; speaking style, slides and pitch quality do not earn points.

## Scoring and tie-breakers

Approximately **two to three judges** may assess each team independently. Each awards one team score out of 100 as described above. The **average of the individual judges' scores** is the official Track-Level score, and teams rank from highest to lowest average.

For example: `(85 + 90 + 88) / 3 = 87.67/100`.

If teams tie, apply these priorities:

1. Higher average **Detection functionality and accuracy** sub-score.
2. Higher average **Generalization and variation testing** sub-score.
3. Panel deliberation on technical evidence if the tie remains.

The **top three teams qualify for the Grand Finale**. The highest-ranked team receives **Best Cybersecurity Solution**. Presentation quality is not a scoring criterion or tie-breaker.

## Event preparation

- **Day 1:** attend the introduction/bootcamp and briefing, confirm task-selection conditions and lab access, verify sources and develop the first working detections.
- **Day 2:** complete implementation, validate positive/benign/changed-input behavior, preserve evidence, restore temporary changes and prepare for technical inspection before the announced freeze.

Use the [curriculum](content.md), [curated resources](resources.md) and [Wazuh Analyst Playbook](3_WAZUH_MANUAL.md) for support. Supporting material does not expand the authorized scope or add mandatory exercises.
