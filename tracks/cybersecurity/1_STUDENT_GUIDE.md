# CYBER DEFENCE HACKATHON 2026
# Zetech University  |  12–13 November 2026

## Welcome. Your team is the bank's security team.

Your job is to look after the bank's critical systems. You have one day to
set up a SIEM — a security monitoring tool called **Wazuh** — that watches
for security events and tells you when something bad happens.

You will not be the one breaking in. You are the ones **defending**.

---

## What you will be doing

1. **Run some attacks** on your lab machine — the same attacks real
   attackers use, in a safe, closed lab.
2. **Build detections in Wazuh** — rules that fire when those attacks happen.
3. **Stop the attacks** — block them, or configure your machine so they fail.
4. **Prove it worked** — show the alert, and show the attack failing afterwards.

You score marks for detections, for good evidence, and for stopping attacks
*without breaking the rest of the system*. Getting a rule that works well is
worth more than running many attacks.

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

### Your tools — that is all you have

- **Wazuh.** Where your alerts appear and where you write rules.
- **Suricata.** Watches network traffic. When something suspicious crosses the
  network, it alerts Wazuh. You don't need to learn a second tool.
- **Sysmon.** On the Windows machine. It records every program that starts,
  every connection it makes, and every file it creates. Your rules read
  these records.

**First thing you do:** open the Wazuh dashboard and check your machine says
**Active**. If it doesn't, nothing you build will count. Fix that first.

---

## Getting a Windows machine

Any Windows works. You don't need a special one:

- A Windows ISO in VirtualBox, VMware, or Hyper-V
- A Vagrant box from vagrantcloud.com
- A ready-made OVA image

Whatever you use, it needs three things — the Windows version doesn't matter:

1. The **Wazuh agent** installed and connected
2. **Sysmon** installed
3. **Host-only / internal network** — no route to the internet

That third one matters most. It keeps your deliberately vulnerable machine
from touching anything real.

---

## Where to run Wazuh

**Cloud is better.** Running Wazuh on your own laptop uses 4 GB of RAM and
slows everything down, and the dashboard dies when the laptop sleeps.

- **AWS EC2**, **DigitalOcean**, or **Azure** — any of those, a 4 GB Ubuntu
  machine, costs a few dollars for the event. Open only the ports Wazuh needs
  (443 for the dashboard, 1514/1515 for agents, 22 for you).

Local works if you're short on time. Cloud is what we recommend.

---

## The five rules

1. **Submit the rule AND a screenshot of it working.** We score the rule.
   The screenshot proves it fired. A rule with no proof scores about half.
2. **At the end, we run the attack again in a way you haven't seen.**
   If your rule only matches the exact command you tried, it will fail.
3. **Blocking everything scores zero.** Block the attacker, not the internet.
4. **Prove the attack worked before you block it.** No attack, no marks.
5. **False alarms cost you marks.** Test your rules against a clean machine.

Partial credit is real. Getting part of a chain right scores those parts.
Submitting nothing is the only way to lose completely.

---

## Using AI

Use AI tools during the event. That's encouraged.

- Ask what a Windows event means
- Paste a rule and ask why it isn't firing
- Ask what MITRE technique your detection covers

**But:** AI gives you code, not understanding. The final round uses an attack
you haven't seen. A rule you don't understand will fail exactly like a
hardcoded one. Use AI to move faster. Use your own head to survive the
final round.

---

## Attacks to try

Pick **two or three**. Each takes about 30–40 minutes. These are **examples
to learn from**, not a checklist — research, adapt, and try your own
variations.

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

Your organisers will give you a lab VM with this already set up, or a script
you run inside it. Named `simulate-ransomware.ps1`, it is a **PowerShell
script** — not an `.exe`, not malware.

- The VM boots, and a folder called `C:\LabFiles` is filled with 80 dummy
  documents (40 in the root, 20 in `Finance`, 20 in `HR`).
- The script takes those 80 files one by one.
- It **reads** each file — real ransomware does this too, and it's part of
  what you detect.
- It **renames the last part of each name** — `document_1.docx` becomes
  `document_1.encrypted`. The content never changes. Nothing is deleted.
- It **pauses 400 milliseconds** between files. Real ransomware would do
  thousands per minute. That pause is your window to catch it.
- **Every file, it checks the file is still inside `C:\LabFiles`** before
  touching it. If anything ever points outside that folder, it stops.

**To run it:** arm your detection first, then inside the VM run
`powershell -ExecutionPolicy Bypass -File C:\LabFiles\simulate-ransomware.ps1`.
It takes about 30 seconds to finish all 80 files. Watch Wazuh while it runs.

**To reset:** rename the `.encrypted` files back, or delete `C:\LabFiles`.
Nothing else to clean up.

**Why it's safe:** the VM has **no network route out** — no internet, no
access to your real machine, nothing. Even if something went wrong, the
script can only touch the 80 dummy documents it created itself.

This is the hardest challenge on purpose. Sysmon does not log *renames*,
so you can't just match the extension. The signal is **how many files one
program touches per second** — the same signal that catches real ransomware.

**9. Only legitimate programs, used badly.** Attack using only Windows'
own trusted tools — `msbuild.exe`, `rundll32`, `certutil`. Nothing
malicious is ever installed — the *behaviour* is the problem. This is why
signature rules aren't enough.

---

## Your team

3–4 people:

- **Attacker** — runs the attacks, writes down exactly what was run
- **Detection** — writes and tunes the Wazuh rules
- **Defender** — applies the controls: blocking, allowlists
- **Scribe (mandatory)** — writes everything down as it happens and owns
  the final report. Not a spare role.

Team of three? Combine attacker + detection. Keep the scribe.

---

## Your day

| When | What |
| --- | --- |
| **Thu 12 Nov** | Briefing, agent checks, pick your scenarios, start detecting |
| **Fri 13 Nov** | Cross-check on the clean machine → apply controls → **Final round: the attack is re-run against your rules, in a new way** → Submit, judging, feedback |

Stuck for more than 20 minutes? Ask. A question costs a minute; staying
stuck costs an hour.

---

## Submit this

```
team07_submission/
├── README.md      one page per scenario: what you ran, your rule, the evidence, what you blocked, your false-positive test
├── rules/         your Wazuh ruleset XML
└── alerts/        alert screenshots / exports
```

Scoring: detection 25%, evidence 25%, vulnerability ID 20%, prevention 20%,
reporting 10%.

Everything you need to run Wazuh is in `3_WAZUH_MANUAL.md` — keep it open
all day.
