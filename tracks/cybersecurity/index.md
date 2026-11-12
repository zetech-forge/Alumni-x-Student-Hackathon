---
title: Cybersecurity
nav_order: 5
parent: Hackathon Tracks
has_children: true
---

# Cybersecurity

Build and verify defensive monitoring for an authorized lab's systems. **Wazuh** is a security monitoring/SIEM platform: endpoint agents collect events, the manager decodes and evaluates them against rules, and the indexer/dashboard make alerts searchable for investigation. Teams configure the needed collection, develop detections, validate results and explain what the evidence means. This is **not a general penetration-testing competition**.

Basic Windows or Linux administration, networking and reading structured logs are useful. You do not need to attempt every exercise or install every monitoring tool. Use the [curriculum](content.md) for preparation and the [Wazuh playbook](3_WAZUH_MANUAL.md) for operating guidance.

The track has **nine task cards: five Windows and four Linux**, not difficulty tiers. Existing guidance recommends selecting **two or three**; it does not explicitly establish a formal minimum-completion rule or mandatory Windows/Linux mix. The Technical Lead must confirm those conditions at the briefing. Select your intended cards, declare them and prioritize complete evidence over extra task count. See [selection guidance](rules.md#task-selection-and-confirmation).

Use the assigned Wazuh environment and approved endpoints. Server/VM allocation, access permissions and available telemetry must be confirmed; do not assume everyone has a supplied cloud instance. Sysmon or equivalent process telemetry is relevant to particular cards, while **Suricata and the broader bank-lab activities are supplementary**, not universal requirements.

**Interact only with supplied or explicitly authorized lab systems.** University infrastructure outside the designated lab, unrelated public targets and other teams' systems without permission are prohibited. Do not publish credentials or sensitive logs.

Every team's selected task set is assessed once out of **100 technical points**. Approximately two to three judges may inspect your rules, configurations and evidence, ask technical questions and rerun a selected behavior with changed lab inputs. Their independent scores are averaged for ranking. **No slide deck or formal pitch is required, and presentation quality earns no points.** The top three teams qualify for the Grand Finale; the highest-ranked team receives **Best Cybersecurity Solution**.

The allocation is **30 detection accuracy/coverage + 20 rule quality/robustness + 15 validation/evidence + 15 investigation + 10 collection/configuration + 10 documentation = 100 points**. Prepare rule/configuration files, task-linked alert/log evidence, positive/benign/changed-input results and investigation notes. Blocking, active response and extra bank-lab scenarios are not additional mandatory deliverables for the nine cards.

Read [Challenges](challenges.md) for the task cards and [Track Rules & How to Compete](rules.md) for authorized scope, tools, submissions, the scoring rubric and tie-breakers.
