---
title: Challenges
parent: Cybersecurity
grand_parent: Hackathon Tracks
nav_order: 4
---

# NINE WAZUH DETECTION ENGINEERING EXERCISES

Develop effective Wazuh detections for suspicious activities in **controlled Windows and Linux environments**. Each exercise presents a scenario to investigate through custom detection rules, validated alerts and supporting evidence. This is defensive detection engineering, not an open-ended penetration-testing or capture-the-flag competition.

Your rules must detect the specified behavior, generate the expected alert, include the required information and continue working when relevant indicators change. Do not rely on one hardcoded test username, IP address or filename. Fixed monitored directories, registry keys and system files required by a card are legitimate scope.

There are **five Windows cards (W1B-W5B)** and **four Linux cards (L1B-L4B)**, not difficulty tiers. Allow **30-40 minutes per exercise after the lab is operational**, with additional time for investigation, evidence and cleanup. Teams are encouraged to complete **two or three exercises properly** rather than rush through nine.

**Selection policy:** the formal completion minimum, any mandatory cards and whether teams may mix operating systems or must remain within one category require Technical Lead confirmation. The [recommended pairings](#recommended-pairings) are optional suggestions, not selection restrictions or evidence that a policy has been approved. Follow the [published selection guidance](rules.md#task-selection-and-confirmation) and confirm conditions before committing to a task set.

**Authorized scope:** use only the designated isolated lab, disposable VMs, supplied systems and explicitly authorized targets. University infrastructure outside the lab, unrelated internet systems and other teams' systems without permission are prohibited. Use harmless test artifacts, protect credentials and follow the approved restoration procedure.

## Before starting

1. Confirm your selected cards, authorized targets, accounts, test procedures and cleanup permissions.
2. Obtain the actual Wazuh address, assigned endpoints, rule-ID range and permitted configuration/deployment route. Never restart a shared manager independently.
3. Verify the required source events reach Wazuh and inspect their raw records, decoded fields and matching rules. An Active agent alone does not prove source collection works.
4. Confirm the installed version and prerequisites below. No complete nine-exercise installer or verified L4B audit-event sample is published in this track; missing telemetry needs Technical Lead resolution, not an invented substitute.
5. Keep expected and observed results for positive, benign and changed-input tests. Label sample replay honestly: `wazuh-logtest` alone does not demonstrate live endpoint-to-dashboard delivery.

Use the [Wazuh Analyst Playbook](3_WAZUH_MANUAL.md), [curated resources](resources.md) and official [custom-rule](https://documentation.wazuh.com/current/user-manual/ruleset/rules/custom.html), [rule-testing](https://documentation.wazuh.com/current/user-manual/ruleset/testing.html) and [syscheck configuration](https://documentation.wazuh.com/current/user-manual/reference/ossec-conf/syscheck.html) references. The cards describe outcomes, not complete detection-rule solutions.

## Windows

### W1B — Too Many Failed Logins

**Operating system:** Windows.

**Estimated duration:** 30-40 minutes after lab readiness.

**Security scenario:** repeated failed RDP or SMB logins against a designated test account may indicate password guessing. Use the approved failure-only procedure; successful access is not required.

**Objective:** detect repeated authentication failures from one source.

**Detect:** **five or more Event 4625 failures from the same source IP within two minutes**. Include the account involved; do not aggregate unrelated source IPs.

**Log source or event:** Windows Security Event Log, Event ID **4625**.

**Telemetry and prerequisites:** failed-logon auditing and Security-channel collection, with decoded source-IP and username fields. Verify the actual Windows authentication parent in the installed ruleset. Upstream Wazuh's [Windows security rules](https://github.com/wazuh/wazuh/blob/master/ruleset/rules/0580-win-security_rules.xml) include 4625 under **60105**, but that reference is not verification of the lab version. **5710 is an SSHD rule, not a Windows parent.**

**Implement:** a custom correlation rule using the verified Windows failure event, same-source grouping and the required count/window. Test the observed trigger count rather than assuming a copied frequency setting implements five failures.

**Expected alert information:** source IP, username, endpoint, timestamp and custom rule ID/description; retain enough source-event evidence to explain the count and window.

**Validation and testing:** generate the approved bounded failure sequence, normally 10-12 failures. Separately test four failures versus the fifth within the window, failures outside the window and failures split across sources. Use a fresh correlation test state or the approved reset/wait procedure so earlier attempts do not contaminate results.

**Variation test:** repeat with another authorized test account or lab source IP. The same behavior must still match.

**Expected evidence:** rule XML, relevant auditing/collection settings, sanitized events and alert, expected/observed count-window results, benign comparison and interpretation. Failures alone do not prove a successful breach.

**Cleanup and safety:** stop after the approved attempt count; respect account-lockout safeguards. Restore temporary accounts or settings through the mentor's procedure and never guess real users' passwords.

### W2B — PowerShell Ran Something Odd

**Operating system:** Windows.

**Estimated duration:** 30-40 minutes after lab readiness.

**Security scenario:** PowerShell or a utility it launches downloads a benign sample file from an authorized lab host. This behavior can merit investigation but is not automatically malicious.

**Objective:** recognize the download-behavior family rather than one copied command.

**Detect:** supported forms using **Invoke-WebRequest, DownloadFile, DownloadString or curl**, including the approved alternative utility such as `curl.exe`. Preserve the relevant PowerShell/child-process context.

**Log source or event:** configured process-creation telemetry, such as **Sysmon Event 1**, **Security Event 4688**, or another approved source providing the required fields.

**Telemetry and prerequisites:** confirm which source the endpoint actually uses. Command-line collection must be enabled and parent-process context available; a basic process event without those fields is insufficient. Verify the source/channel and decoded field names before writing the rule.

**Implement:** conditions identifying the supported download operations and process relationships. Do not alert on every PowerShell launch or depend on one file name, URL or exact command line.

**Expected alert information:** **full command line and parent process**, plus the process image, endpoint, timestamp and rule identity.

**Validation and testing:** use the approved download procedure and a harmless file served inside the isolated lab. Confirm the required process details appear in the alert; compare ordinary approved PowerShell activity without a download.

**Variation test:** repeat with an alternative supported download command or utility and a changed benign lab filename/URL. Verify the family remains covered.

**Expected evidence:** rule and source configuration, process events/alerts, positive/benign/variation results and an explanation of what the observed command establishes.

**Cleanup and safety:** remove only your test downloads and stop any temporary lab-only file service as instructed. Do not execute downloaded content, contact public download sites or substitute a real payload.

### W3B — A New Program Was Installed

**Operating system:** Windows.

**Estimated duration:** 30-40 minutes after lab readiness.

**Security scenario:** a new service points to a binary outside the approved Windows directory. Unexpected services may indicate persistence or unauthorized modification, although legitimate software can also install there.

**Objective:** identify service installations that meet the specified path condition.

**Detect:** **Event 7045** with a service binary path **outside the approved Windows directory**, normally `C:\Windows`.

**Log source or event:** Windows **System** channel, Service Control Manager Event ID **7045**.

**Telemetry and prerequisites:** System-channel collection and an authorized lab account with permission for the supplied benign service-creation procedure. Confirm the actual Windows directory and event fields. The event is generated on the target VM when the approved service is created; starting it is not required merely to demonstrate installation.

**Implement:** service-event matching and a Windows-directory exclusion with correct path boundaries. Account for the lab's path representation, quoting and arguments; do not mistake a similarly named directory for Windows or exclude every non-Windows location.

**Expected alert information:** **service name, binary path and service account**, plus endpoint, timestamp and rule identity. Include the initiating actor if the source supplies it.

**Validation and testing:** create only the approved benign test service configuration and verify Event 7045 and its alert. Compare an approved Windows-directory example through the permitted live/sample procedure. A legitimate service outside Windows still meets the path condition; explain it rather than claiming malware.

**Variation test:** change the authorized service name and outside-Windows lab path. Detection must not depend on the original service name or filename.

**Expected evidence:** rule, channel settings, relevant service events/alerts, path-comparison results, variation results and investigation notes.

**Cleanup and safety:** remove the test service, remove your harmless artifacts and restore the VM as directed. Do not deploy malware, start untrusted executables or leave persistent unauthorized services.

### W4B — Someone Turned Off the Antivirus

**Operating system:** Windows.

**Estimated duration:** 30-40 minutes after lab readiness.

**Security scenario:** Defender real-time protection is temporarily disabled on a designated disposable VM. This is a security-control change requiring investigation.

**Objective:** detect protection being disabled and verify safe restoration.

**Detect:** **Event 5001** for real-time protection being disabled. Detection of **Event 5000** when protection is re-enabled is an **optional additional component within the same 100-point rubric**, not extra bonus points.

**Log source or event:** **Microsoft-Windows-Windows Defender/Operational**.

**Telemetry and prerequisites:** a disposable Windows VM with Defender and explicit permission for the temporary change. Participants must ensure this channel is configured for collection; add it through the approved route if it is not already supplied. Confirm actual events arrive.

**Implement:** a rule matching the protection-disabled event from the correct provider/channel. An optional second rule can identify re-enabling.

**Expected alert information:** endpoint, event ID, channel/provider, timestamp, protection-change context and rule identity.

**Validation and testing:** first verify protection is active and monitoring is ready. Under the approved procedure, briefly disable real-time protection, observe Event 5001 and its alert, then immediately re-enable protection regardless of the detection result. Verify protection is active again and inspect Event 5000 where available. If policy or tamper protection prevents the exercise, stop and ask the mentor; do not bypass other safeguards.

**Variation test:** repeat the approved disable/restore sequence after restoration, or on another explicitly assigned disposable endpoint. Match the event behavior rather than one hostname or message string.

**Expected evidence:** channel/rule settings, sanitized 5001 event/alert, test timeline and restoration confirmation. Include 5000 evidence if attempting the optional detection.

**Cleanup and safety:** re-enable Defender and restore the VM to its approved clean state after preserving evidence. **Never perform this exercise on personal or production computers.**

### W5B — File Integrity Monitoring on Windows

**Operating system:** Windows.

**Estimated duration:** 30-40 minutes after lab readiness.

**Security scenario:** files change in a monitored protected location, or a new startup Run-key value appears. FIM can reveal these changes without executing their contents.

**Objective:** establish a baseline and detect subsequent file/registry changes.

**Detect:** harmless file additions or modifications in the assigned protected directory. **Registry monitoring remains an additional assessment component for complete task coverage**, not a new exercise or a separate point pool.

**Log source or event:** Wazuh **syscheck/FIM** file and Windows Registry events.

**Telemetry and prerequisites:** assigned directories, permission for harmless changes and a functioning Wazuh agent. Filesystem monitoring uses `<directories>`; Registry monitoring uses **`<windows_registry>` under `<syscheck>`**, not a filesystem directory entry. Confirm the assigned Run startup key, normally `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run`, and the appropriate 32-bit/64-bit registry view.

**Implement:** scoped file monitoring, appropriate change-alert behavior and monitoring of new values in the approved Run key. Record the initial inventory and distinguish it from later changes. Use version-matched [syscheck configuration](https://documentation.wazuh.com/current/user-manual/reference/ossec-conf/syscheck.html#windows-registry), without copying a complete detection solution.

**Expected alert information:** endpoint, timestamp, object path or registry key/value name, change type and rule/severity context. Preserve relevant before/after metadata without exposing secrets.

**Validation and testing:** establish the baseline, create or modify a harmless test file, then verify its FIM event and alert. For the registry component, make only the approved inert test-value change. Document scan interval and observed latency: file realtime monitoring depends on configuration, while Registry monitoring is scheduled and must not be assumed instantaneous. Apply interval/restart changes only with permission.

**Variation test:** repeat with a different harmless filename and, for registry coverage, a different approved value name. Pre-existing baseline entries must not be misreported as new persistence; document initial-scan noise separately.

**Expected evidence:** file/Registry settings, baseline and scan timing, rule/alert behavior, change events, positive/benign/variation results and limitations. File-only evidence is incomplete for the additional Registry component.

**Cleanup and safety:** remove your test files and values, restore original settings and preserve the approved baseline/VM state. Use no malware, malicious DLLs or active startup payloads; do not modify real application binaries or trigger the test Run entry.

## Linux

### L1B — SSH Brute Force Detection

**Operating system:** Linux.

**Estimated duration:** 30-40 minutes after lab readiness.

**Security scenario:** repeated failed SSH attempts against a designated temporary lab account may indicate password guessing. The exercise requires failures only.

**Objective:** correlate failed SSH authentication from one source.

**Detect:** **five or more failed SSH attempts from the same source IP within two minutes**.

**Log source or event:** the endpoint's actual SSH authentication log or journal feed, forwarded to Wazuh.

**Telemetry and prerequisites:** an authorized SSH test endpoint, bounded failure procedure and decoded account/source fields. Inspect the installed SSH failure rules. Upstream [rule 5712](https://github.com/wazuh/wazuh/blob/master/ruleset/rules/0095-sshd_rules.xml) has **`frequency="8"` and `timeframe="120"`**; copying it unchanged does not establish this card's five-attempt behavior.

**Implement:** a custom correlation rule over the appropriate decoded SSH failures, with same-source grouping and validated five-attempt behavior. Retain the published threshold unless the Technical Lead explicitly approves a change; verify observed trigger counts in the installed version.

**Expected alert information:** **source IP and username**, endpoint, timestamp and custom rule identity, with source evidence supporting the count/window.

**Validation and testing:** run the approved bounded failure sequence, normally 10-12 failures. Test four failures versus the fifth within two minutes, events outside the window and separate source IPs. Reset/wait as approved between correlation cases. Compare benign SSH activity without requiring a successful login after failures.

**Variation test:** change the authorized lab source IP or test account and verify continued detection.

**Expected evidence:** rule and collection configuration, sanitized SSH events/alerts, threshold/window and benign/variation results, and interpretation without an unsupported successful-access claim.

**Cleanup and safety:** stop the test at the agreed limit, restore/remove temporary accounts as instructed and avoid disruption or lockouts. Never test real accounts or unrelated SSH servers.

### L2B — Someone Edited the Passwd File

**Operating system:** Linux.

**Estimated duration:** 30-40 minutes after lab readiness.

**Security scenario:** account administration changes `/etc/passwd` and `/etc/shadow`. Unauthorized changes could affect access, but legitimate administration also produces these events.

**Objective:** detect changes to both protected account files without exposing their sensitive contents.

**Detect:** FIM changes to **`/etc/passwd` or `/etc/shadow`**, with both paths configured and validated.

**Log source or event:** Wazuh **syscheck/FIM** events on the designated Linux VM.

**Telemetry and prerequisites:** a disposable endpoint, permission for controlled account changes, an established file baseline and an agreed scan/realtime configuration. Keep sensitive content-diff reporting disabled; do not export password hashes.

**Implement:** monitoring of both files and suitable custom detection/alert behavior. Use the approved account-management procedure, not manual corruption of system files.

**Expected alert information:** endpoint, timestamp, affected path, change type and rule identity; include useful non-secret metadata.

**Validation and testing:** establish the baseline, then create a clearly named temporary account such as `lab-fim-test` using the approved procedure. Where needed, perform an approved temporary-account password change to validate shadow-file coverage. Locate events/alerts for the changed files, record detection delay and compare legitimate administrative activity.

**Variation test:** repeat with a different authorized temporary account. The rule must detect changes to the required files rather than one account name or content string.

**Expected evidence:** scoped FIM/rule settings, baseline context, sanitized metadata alerts for both paths, test timeline, benign/variation results and interpretation. Do not include file contents, credentials or password hashes.

**Cleanup and safety:** remove the temporary accounts and their test artifacts through the approved procedure; restore the VM's clean state. Do not alter existing users, grant unnecessary privileges or use real credentials.

### L3B — A Web Shell Appeared

**Operating system:** Linux web-application endpoint.

**Estimated duration:** 30-40 minutes after lab readiness.

**Security scenario:** a PHP file appears in the designated DVWA upload directory and is requested over HTTP. The lab artifact is harmless; a functional malicious shell is not required.

**Objective:** detect the file-appearance and web-request stages.

**Detect:** **(1)** a PHP file appearing in the upload directory through FIM, and **(2)** a `.php` or `.phtml` file under the upload path being requested through the web-server logs. Either working approach earns partial task credit; both are needed for full detection coverage, alongside the task's required tests/evidence.

**Log source or event:** Wazuh FIM and the approved web-server access logs from the designated DVWA instance.

**Telemetry and prerequisites:** confirm the supplied DVWA address, credentials through the private organizer channel, actual upload path and access-log location. `hackable/uploads` is a common application-relative location, not a verified absolute lab path. Both sources must reach Wazuh; do not assume a particular server or log filename.

**Implement:** scoped upload-directory monitoring and a rule for relevant PHP/PHTML requests under that path. Relate the two signals by endpoint, path and time; neither a generic file change nor an unrelated PHP request establishes the whole sequence.

**Expected alert information:** endpoint, timestamp, uploaded file path/change type for FIM, and request path/method plus source address/status where available for access events; retain each rule identity.

**Validation and testing:** upload the approved harmless PHP artifact through DVWA and request it once in the browser. Verify each signal separately, then explain the sequence. Compare benign permitted uploads/requests. An HTTP request or response does not by itself prove malicious code execution.

**Variation test:** repeat with a different approved filename and a supported PHP/PHTML request example. Do not match only the first test file.

**Expected evidence:** both relevant configurations/rules, sanitized FIM and access events/alerts, path/time mapping and positive/benign/variation results. Clearly label a single working approach as partial coverage.

**Cleanup and safety:** remove only your uploaded artifacts, close test sessions and restore the approved lab state. Do not upload a real shell, persist access, contact a public upload service or expose DVWA to the internet.

### L4B — The Web Server Called Home

**Operating system:** Linux web-application endpoint.

**Estimated duration:** 30-40 minutes after lab readiness.

**Security scenario:** an approved web-application test initiates outbound activity toward a team-controlled host on the isolated lab network. Unexpected activity attributable to a web-server account may indicate abuse.

**Objective:** detect the specified outbound behavior associated with **`www-data`**, while distinguishing process execution, a connection attempt and a confirmed connection.

**Detect:** the approved outbound activity attributable to the web-server process/effective identity, with destination context. Here, "external" means another authorized lab host, not an unrelated internet system.

**Log source or event:** the expected preconfigured **auditd** feed, plus approved network/listener evidence where required to establish connection details. Its actual configuration and a representative decoded sample require Technical Lead confirmation; neither is verified by this repository.

**Telemetry and prerequisites:** inspect the supplied event and record the exact decoded field names for the logical conditions below. Do not assume every audit event contains every field or that `www-data` has the same numeric UID on every VM.

| Required information | What to verify in the supplied telemetry |
|---|---|
| Execution and process identity | Relevant `SYSCALL`/`EXECVE` or equivalent records: executable, PID/parent context and actual command arguments. |
| Effective identity | Effective UID (`euid`) and its mapping to the assigned `www-data` account. Login audit identity (`auid`) alone is not equivalent. |
| Intended destination | Arguments can identify an intended URL/host, but do not establish the address actually contacted. |
| Network destination and outcome | Where supplied, related socket/connect records, decoded `SOCKADDR` data or approved corroborating network/listener logs. Link them to the process/test by available identifiers and timing. |

**Implement:** conditions matching the verified effective identity, relevant executable/arguments and authorized destination context. Preserve the mapping from these requirements to the lab's exact decoded fields in your README. Do not match a process name of `www-data`: it is normally an account identity, while the network client may be a child process.

**Expected alert information:** endpoint, timestamp, rule identity, effective user/UID, relevant executable/arguments and destination context. Include process linkage and connection outcome only where supported.

**Validation and testing:** use the existing approved callback procedure and benign lab listener. Compare the source record with the alert and any listener/network evidence. A successful `execve` means a program executed, **not** that it connected successfully. If the feed provides execution only, report that limited evidence and request the missing telemetry/Technical Lead decision; do not claim the original connection objective is fully demonstrated.

**Variation test:** change the authorized lab destination address or port and compare approved unrelated process activity. The detection must retain the web-server identity/behavior condition rather than matching one destination string.

**Expected evidence:** supplied audit configuration or approved reference, exact decoded-field mapping, custom rule, sanitized alerts/source records, positive/benign/variation results and corroboration for any claimed network connection. Clearly distinguish intended destination, attempted connection and observed success.

**Cleanup and safety:** stop your lab listener, remove temporary artifacts and restore the VM/application as instructed. No callbacks to unrelated external systems, data exfiltration or persistent access are permitted. Resolve insufficient telemetry before claiming full task completion.

## Recommended pairings

These are **optional learning suggestions**, not mandatory selections. Confirm the operating-system selection policy with the Technical Lead before relying on a pairing:

| Pairing | Focus |
|---|---|
| **W1B + L1B** | Authentication monitoring across Windows and Linux. |
| **W1B + W4B** | Authentication and security-control monitoring. |
| **L1B + L2B** | Authentication and Linux file integrity. |
| **W5B + L2B** | File integrity monitoring across Windows and Linux. |
| **L3B + L4B** | Web-application upload and outbound-activity detection. |

Identify selected card IDs in your submission. More cards do not automatically earn more points.

## Participant deliverables

For each selected card, provide:

- Custom Wazuh rule XML and relevant non-secret endpoint/collection/FIM configurations or configuration changes.
- Sanitized alert records with required fields, timestamps and task mapping. Screenshots may illustrate the evidence; retain the permitted exports/source context required by the [Track Rules](rules.md#submission-and-assessment-preparation).
- Expected/observed positive, benign and variation-test results, including count/window or scan-timing checks where applicable.
- Short documentation explaining the scenario, source, rule logic, interpretation, limitations, reproduction steps and cleanup.

Include the common submission items in the rules, including the backup demo video and team/SDG/contribution information. **Do not submit passwords, tokens, private keys, password hashes, sensitive file contents or unrelated system data.**

## Technical demonstration expectations

Be ready to show the approved original activity, its detection in Wazuh, the resulting alert and required fields, and a changed-input rerun. Explain why the rule works, what benign comparison you tested and what the evidence cannot establish. Perform only the approved lab activity; a new target or scenario is not authorized by a demonstration request.

This is **technical verification, not a formal presentation**. No slide deck or formal Track-Level pitch is required, and speaking style or presentation quality earns no marks.

## Technical assessment checkpoints

The selected task set is assessed **once out of 100 points**, not 100 per card. Full credit depends on demonstrated requirements and reproducible evidence; partial/inconsistent coverage earns partial credit, and missing or unsupported work earns none for the affected requirement. W4B's re-enable extension adds no separate bonus points, and L3B requires both detection approaches for full task coverage.

| Criterion | Points |
|---|---:|
| Detection accuracy and coverage | 30 |
| Detection rule quality, specificity and robustness | 20 |
| Validation, testing and evidence quality | 15 |
| Investigation quality and alert interpretation | 15 |
| Log-source collection and system configuration | 10 |
| Documentation and reproducibility | 10 |
| **Total for the selected task set** | **100** |

Approximately **two to three judges** may assess each team independently. Their scores are **averaged**, teams rank by the final average, and the **top three teams qualify for the Grand Finale**. See the [Track Rules](rules.md#judging-criteria) for the full rubric and [scoring and tie-breakers](rules.md#scoring-and-tie-breakers) for ranking.
