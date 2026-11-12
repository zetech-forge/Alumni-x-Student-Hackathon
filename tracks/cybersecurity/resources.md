---
title: Curated Resources
parent: Cybersecurity
grand_parent: Hackathon Tracks
nav_order: 2
---

# Cybersecurity: Curated Resources

Use these defensive references for your selected [task cards](challenges.md), not as a requirement to install every tool. **Interact only with supplied or explicitly authorized lab systems.** A resource describing a technique does not authorize its use against university infrastructure, unrelated public systems or other teams.

## Security monitoring, installation and access

| Resource | Use and exercise mapping |
|---|---|
| [Wazuh quickstart and sizing](https://documentation.wazuh.com/current/quickstart.html) | Understand the server/indexer/dashboard and installation requirements. All cards; install only when approved, not on the assumption each team must provision a server. |
| [Wazuh agent installation](https://documentation.wazuh.com/current/installation-guide/wazuh-agent/index.html) | Supported endpoint setup/enrollment. All cards, according to assigned permissions and installed version. |
| [Wazuh dashboard guide](https://documentation.wazuh.com/current/user-manual/wazuh-dashboard/index.html) | Find agents/alerts, set the time range and inspect event fields. All cards. |

## Log collection and detection rules

| Resource | Use and exercise mapping |
|---|---|
| [Wazuh log-collection configuration](https://documentation.wazuh.com/current/user-manual/capabilities/log-data-collection/configuration.html) | Collect Windows channels and relevant Linux log files. W1B-W4B, L1B, L3B and the approved L4B feed. |
| [Wazuh decoders](https://documentation.wazuh.com/current/user-manual/ruleset/decoders/index.html) | Understand raw logs versus extracted fields before choosing rule conditions. All cards. |
| [Custom Wazuh rules](https://documentation.wazuh.com/current/user-manual/ruleset/rules/custom.html) | Rule files, appropriate custom IDs and safe changes. All cards; use the assigned team range/deployment route. |
| [Testing decoders and rules](https://documentation.wazuh.com/current/user-manual/ruleset/testing.html) | `wazuh-logtest` for permitted samples and correlation checks. All cards; it does not by itself prove endpoint-to-dashboard delivery. |
| [Wazuh File Integrity Monitoring](https://documentation.wazuh.com/current/user-manual/capabilities/file-integrity/index.html) | Baselines, monitored files/registry and change evidence. W5B, L2B and L3B. |

## Windows and Linux source references

| Resource | Use and exercise mapping |
|---|---|
| [Microsoft: Event 4625](https://learn.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4625) | Interpret failed-logon fields for W1B. A failed event is not evidence of successful access. |
| [Microsoft Sysmon](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon) | Process/parent/command-line telemetry where configured for W2B. It is not a mandatory extra installation for every card. |
| [Ubuntu auditd manual](https://manpages.ubuntu.com/manpages/noble/man8/auditd.8.html) | Understand Linux auditing for L4B's approved feed. Use documentation matching the allocated OS; do not invent or deploy new audit rules on shared endpoints. |

## Alert investigation and responsible practice

Start with the task's raw event and decoded fields, then ask what the alert establishes, what legitimate activity could explain it and what remains unknown. Preserve endpoint/rule IDs, timestamps, required fields and test context. Redact secrets and sensitive content, not the information necessary to understand the detection.

- [Track rules and authorized scope](rules.md): access, selection confirmation, deliverables and the 100-point rubric.
- [Wazuh analyst playbook](3_WAZUH_MANUAL.md): collection, rule testing, investigation and troubleshooting.
- [Curriculum](content.md): essential learning and task-specific preparation.
- [Bank-lab participant guide](1_STUDENT_GUIDE.md): supplementary background, not a second mandatory assignment. Suricata, blocking/SCA and extra simulations are not required by the nine cards.

The existing [ransomware-behaviour VM definition](labs/ransomware-sim/Vagrantfile) is an **optional, separate lab artifact**, not the current nine-task installer. Do not run it without Technical Lead approval and verified isolation; neither a private adapter nor the file's comments establish the absence of other network routes. It has not been validated as part of this documentation update.

Documentation access is free. Actual VM/server allocation, permissions and software versions require organizer confirmation; no purchased hosting, offensive toolkit, shared API key or production credential is required.
