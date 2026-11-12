---
title: Cyber Defence Hackathon 2026
parent: Cybersecurity
grand_parent: Hackathon Tracks
nav_order: 5
---

# CYBER DEFENCE HACKATHON 2026
# Zetech University  |  12–13 November 2026

## Supporting bank-lab guide: read the current task cards first

This guide contains broader bank-security practice material. The repository
does not establish that all of those activities are approved components of the
current competition. The **[nine Wazuh task cards](challenges.md)** and
**[Track Rules](rules.md)** define the required technical work; treat the
additional bank scenarios as supplementary unless the Technical Lead explicitly
approves them.

The focus is **defensive monitoring**, not general penetration testing.
Only supplied or explicitly authorized lab systems may be used. University
infrastructure outside the lab, unrelated public targets and other teams'
systems without permission are prohibited. Keep credentials and sensitive
logs private; follow approved simulation and cleanup instructions.

Existing guidance recommends **two or three selected cards**. A formal
completion minimum, compulsory platform mix and named mandatory cards still
require Technical Lead confirmation at the briefing. No slides or formal
Track-Level pitch are required.

---

## What you will be doing

1. Confirm the selected cards, authorized endpoints and their required log sources.
2. Verify collection, develop the Wazuh detections and use only the approved test events.
3. Validate positive, benign and changed-input cases, then investigate the alerts.
4. Preserve rule/configuration changes, permitted evidence and reproduction notes.

Blocking, active response and extra bank-lab exercises are not mandatory
deliverables for the current nine cards. Optional practice does not create
extra points or authorize additional targets.

---

## Your lab

```
                    ┌──────────────────────────────┐
   Your attack VM ─►│  The machine you defend      │
                    │  • Sysmon (records what runs)│
                    │  • Wazuh agent (sends logs)  │
                    └──────────────┬───────────────┘
                                   │ logs + network alerts
                                   ▼
                    ┌──────────────────────────────┐
                    │  WAZUH — every alert lands   │
                    │  here. This is your screen.  │
                    │  SURICATA watches the network│
                    │  and sends alerts into Wazuh │
                    │  too. One dashboard.         │
                    └──────────────────────────────┘
```

The diagram illustrates the broader bank lab, not a guarantee of supplied
infrastructure. Confirm the actual environment and access at the briefing.
Suricata is supplementary; process telemetry is required only where a
selected card needs it.

### Tools and their roles

- **Wazuh.** Where your alerts appear and where you write rules.
- **Suricata (supplementary).** Network monitoring if explicitly provided and
  approved; no current card requires universal Suricata deployment.
- **Sysmon (source-dependent).** Configured Windows telemetry can supply
  process/parent/command-line context for W2B. Collection depends on its
  configuration; do not assume it records every action.

**First thing you do:** open the Wazuh dashboard and check your machine says
**Active**, then confirm the selected source's events actually arrive.
A green connection alone does not establish that every required channel is collected.

---

## Getting a Windows machine

Use an approved, compatible Windows lab image with the channels needed for
your selected cards. The options below are possible packaging formats, not
a promise of an allocated image or a requirement to install your own:

- A Windows ISO in VirtualBox, VMware, or Hyper-V
- A Vagrant box from vagrantcloud.com
- A ready-made OVA image

Confirm:

1. The **Wazuh agent** installed and connected
2. The selected card's event channels/process telemetry; Sysmon is not universal
3. An approved isolated lab network with no unintended external routes

The Technical Lead must verify isolation. A host-only/private adapter by itself
does not prove that another NAT, bridged or host-access route is absent.

---

## Where to run Wazuh

Use the organizer-approved Wazuh setup. Confirm monitoring access and
telemetry before the assessment; you are not required to purchase cloud
hosting. Do not expose deliberately vulnerable targets or lab services to
the public internet. Any remote monitoring arrangement must preserve the
approved lab isolation and access restrictions in the [Track Rules](rules.md).

---

## The five rules

1. **Submit the rule AND evidence of it working.** Export the alert with
   the required fields; screenshots can support it. An unverified rule
   cannot earn full credit for detection or evidence.
2. **You may be asked to repeat an approved task with changed lab inputs.**
   A rule that memorizes one command, address or account does not demonstrate
   the required behavior.
3. **Blocking is not a detection substitute.** Optional controls must not
   disrupt legitimate use or required monitoring.
4. **Support claims with evidence.** Sample rule replay and live endpoint
   collection are different results; report which one you demonstrated.
5. **False alarms affect detection credit.** Test benign activity on the
   designated endpoint during an approved benign test window.

Partial credit reflects demonstrated parts of the detection/evidence chain.
Authorization and integrity violations remain subject to the General Rules.

---

## Using AI

Use AI tools during the event. That's encouraged.

- Ask what a Windows event means
- Share a sanitized rule/sample and ask why it is not firing; never upload credentials or sensitive lab logs
- Ask what MITRE technique your detection covers

**But:** AI-generated rules still need explanation and validation. Technical
assessment may repeat the selected task with approved changed inputs; it is
not permission for an undisclosed or out-of-scope attack. Be able to explain
the conditions, required fields and limitations of your rule.

---

## Supplementary bank-lab scenarios, not additional task cards

The examples below are historical/supporting practice, not a second approved
assignment. Confirm the selection conditions in [Track Rules](rules.md).
Use these examples only when the Technical Lead explicitly approves the
scenario, target and procedure; they do not substitute for a selected card
automatically. In particular, W1B/L1B require failures only, not the broader
success-after-failures scenario below.

**1. Port scan.** Run `nmap -sV` at your machine from the attack VM.
Suricata should see it. Your job: tell "real recon" from "one ping".

**2. A program phones home.** A reverse shell connects back to your attacker
machine, then keeps connecting on a rhythm. Suricata sees the traffic.
Sysmon sees the process. Join them if you can.

**3. Too many failed logins.** Brute force SSH, RDP, or SMB: fail 10 times,
then succeed. Your rule should fire on the **success that comes after the
failures**, not just on the failures.

**4. PowerShell downloads something.** Run a PowerShell command that pulls
a file from your attacker machine. Your rule should catch the *pattern*
(a download command), not the exact string.

**5. A service appears from nowhere.** Install a Windows service pointing at
a file you placed in a temp folder. Detect it — without firing on
legitimate installs.

**6. Someone edits a password file.** On Linux: `useradd backdoor`. File
integrity monitoring (FIM) should catch the `/etc/passwd` change.

**7. A web shell is uploaded.** Upload a PHP file to the web app, then open
it. Detect the upload, the request, or the shell running.

**8. The ransomware simulation — how to run it, and what it does.**

An optional [VM definition](labs/ransomware-sim/Vagrantfile) exists separately.
It is not the nine-task installer or a promise of an allocated, working VM.
The following describes its intended exercise, not a validated safety guarantee.
Do not run it without Technical Lead approval and verified isolation.
The provisioned `simulate-ransomware.ps1` is a PowerShell simulation script,
not a mandatory competition artifact.

- The VM boots, and a folder called `C:\LabFiles` is filled with 80 dummy
  documents (40 in the root, 20 in `Finance`, 20 in `HR`).
- The script selects up to 80 files recursively. It does not explicitly
  exclude the simulation script itself or unrelated files already in that
  directory; the selected set needs review before any approved run.
- It **reads** each file — real ransomware does this too, and it's part of
  what you detect.
- It **renames the last part of each name** — `document_1.docx` becomes
  `document_1.encrypted`. The content never changes. Nothing is deleted.
- It **pauses 400 milliseconds** between files. Real ransomware would do
  thousands per minute. That pause is your window to catch it.
- Each iteration performs a path-prefix check against `C:\LabFiles`.
  This is not a verified containment boundary, especially for redirected
  paths or directory links.

**To run it:** arm your detection first, then inside the VM run
`powershell -ExecutionPolicy Bypass -File C:\LabFiles\simulate-ransomware.ps1`.
It takes about 30 seconds to finish all 80 files. Watch Wazuh while it runs.

**Reset:** follow the Technical Lead's approved restore procedure. Do not
assume an arbitrary existing folder contains only disposable simulation files.

**Safety limitation:** isolation, exact file selection and containment must
be verified before any optional run. The file's comments or a private adapter
do not prove those properties. This documentation update did not execute it.

This is outside the current nine cards. Any approved optional behavior
analysis must use the events actually available; do not assume a particular
Sysmon configuration exposes every read or rename.

**9. Only legitimate programs, used badly.** Attack using only Windows'
own trusted tools — `msbuild.exe`, `rundll32`, `certutil`. Nothing
malicious is ever installed — the *behaviour* is the problem. This is why
signature rules aren't enough.

---

## Suggested roles for the broader bank exercise

3–4 people:

- **Attacker** — runs the attacks, writes down exactly what was run
- **Detection** — writes and tunes the Wazuh rules
- **Defender** — applies the controls: blocking, allowlists
- **Scribe** — writes everything down as it happens and owns
  the final report. Not a spare role.

These roles are suggestions, not extra eligibility or deliverable requirements
for the nine cards. Follow the General Rules for team composition; distribute
collection, detection, testing and documentation work sensibly.

---

## Your day

| When | What |
| --- | --- |
| **Thu 12 Nov** | Briefing, agent checks, pick your scenarios, start detecting |
| **Fri 13 Nov** | Positive/benign/changed-input checks → investigate alerts → preserve evidence → submit for technical assessment |

Stuck for more than 20 minutes? Ask. A question costs a minute; staying
stuck costs an hour.

---

## Submit this

```
team07_submission/
├── README.md      per selected card: source, rule, tests, evidence, findings, limitations
├── rules/         your Wazuh ruleset XML
└── alerts/        alert screenshots / exports
```

Also include relevant configuration changes, alert exports, benign/changed-input
tests and investigation notes as described in the [submission requirements](rules.md#submission-and-assessment-preparation).

The selected task set is scored once out of **100**: detection accuracy/coverage
30, rule quality/robustness 20, validation/evidence 15, investigation 15,
collection/configuration 10 and documentation 10.
Approximately two to three judges may score it independently; their scores
are averaged. For example, `(85 + 90 + 88) / 3 = 87.67/100`.
The top three teams qualify for the Grand Finale, and the highest-ranked
team receives **Best Cybersecurity Solution**. Technical demonstrations and
questions verify evidence, not presentation skills.

Use the [Wazuh manual](3_WAZUH_MANUAL.md) for setup and rule-writing guidance.
