---
title: Content & Curriculum
parent: Cybersecurity
grand_parent: Hackathon Tracks
nav_order: 1
---

# Cybersecurity: Content & Curriculum

Prepare to **collect, detect, validate and investigate** events for your selected [Wazuh task cards](challenges.md). This is defensive monitoring, not open-ended penetration testing. Work only on supplied or explicitly authorized lab systems; university infrastructure outside the lab, unrelated public targets and other teams' systems without permission are prohibited.

## Before starting

- Be comfortable with basic Windows or Linux administration, IP addresses, timestamps and reading structured logs. Learn the selected platform, not every tool.
- Confirm the lab account, endpoint, Wazuh address, permitted configuration/rule-deployment route and expected log sources with the Technical Lead.
- Existing guidance recommends two or three of nine cards. Confirm the formal completion minimum and any compulsory platform/card selection at the briefing; they are not explicitly established in the materials.
- No complete current-lab installer is published here. A missing agent/channel, audit feed or server allocation must be resolved rather than assumed supplied.

## Essential learning areas

| Area | Practical learning outcome | Applies to |
|---|---|---|
| Authorization and lab handling | Know the allowed targets/actions, protect credentials/logs and follow the approved event/cleanup procedure. | All selected cards |
| Wazuh and SIEM basics | Distinguish endpoint collection, manager decoding/rules, indexing and dashboard investigation. Verify agent identity and recent telemetry. | All |
| Log collection and decoding | Inspect raw and decoded fields, configure only the required channel/path and recognize missing telemetry. | All |
| Detection rules | Explain parent/group/field conditions, correlation windows and severity. Test with `wazuh-logtest` where permitted; distinguish sample replay from live alert delivery. | All |
| Validation and investigation | Compare positive, benign and changed-input results, interpret alerts and preserve evidence without claiming an unobserved compromise. | All |
| Reproducible reporting | Keep rule/configuration changes, test times, evidence IDs, findings and limitations together. | All |

Use the [playbook](3_WAZUH_MANUAL.md) for operating details and the [official resources](resources.md) for version-specific syntax.

## Focus by exercise

| Selected cards | Required preparation and first checkpoint |
|---|---|
| W1B / L1B | Windows failed-logon or Linux SSH fields, source-based correlation and the stated count/time boundary. Locate a failed event before writing the aggregate detection; successful login is not required. |
| W2B | Process creation with command line and parent context. Verify field collection before matching the approved download behavior. |
| W3B | System Event 7045 and its service path/account fields. Separate the specified outside-Windows path from legitimate comparison examples. |
| W4B | Defender Operational channel and approved temporary protection-change/restoration procedure. Verify channel collection before the test. |
| W5B / L2B | FIM baseline, monitored file/registry scope, change metadata and benign account/file administration. Do not collect sensitive account-file content diffs. |
| L3B | Approved DVWA upload path, FIM and web access logs. Link upload/request evidence by path and time without claiming unobserved execution. |
| L4B | The approved audit feed linking web-server process identity to an outbound connection. Confirm the expected preconfiguration with the mentor before developing the Wazuh rule. |

## Event preparation

**Day 1:** Confirm selection conditions and lab scope/access, verify telemetry for the intended cards, inspect sample events and build a first working detection. Ask for help when source fields are missing; installing an entire shared SIEM is not assumed to be a short participant exercise.

**Day 2:** Validate positive, benign and changed-input cases, investigate what the alerts show, preserve permitted exports and finish the README/test evidence before freeze. Restore temporary lab changes as instructed.

Additional agent courses, SCA hardening, active response, Suricata monitoring and the bank/ransomware-behaviour scenarios are **supplementary**, not extra mandatory cards. They still need explicit authorization. The broader guide's dedicated attacker/defender/scribe roles are suggestions, not additional eligibility requirements.

## Assessment preparation

The [rubric](rules.md#judging-criteria) is **30 detection + 20 rule quality + 15 validation/evidence + 15 investigation + 10 collection/configuration + 10 documentation = 100 points** for the selected set. Prepare working rules/configuration, alert/log evidence, test results and investigation notes. No slide deck or formal Track-Level pitch is required; presentation quality earns no points.
