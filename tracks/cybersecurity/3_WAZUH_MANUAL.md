---
title: Wazuh Analyst Playbook
parent: Cybersecurity
grand_parent: Hackathon Tracks
nav_order: 6
---

# Wazuh Analyst Playbook — Operating Instructions for the Event

This is the day-one working manual for the Wazuh stack. The challenge cards
tell you *what* to build; this tells you *how* to navigate the tool, where
everything lives, what good monitoring looks like, and where the official
documentation is when you need the exact syntax. Keep it open in a browser
tab next to the dashboard all day.

**Scope:** use only supplied or explicitly authorized lab systems and the
selected [nine task cards](challenges.md). Do not test unrelated public systems,
university infrastructure outside the lab or other teams' systems without
permission. Protect credentials/logs and change only assigned configurations.
The [Track Rules](rules.md) control selection, mandatory evidence and scoring.
Legacy C/W/L examples, SCA and active response below are supplementary, not
extra tasks. An installed server, table card or privileged account is not
guaranteed; confirm the actual environment at the briefing.

---

## Part 1 — Your first 15 minutes in Wazuh

### 1.1 Log in and orient yourself

Obtain the dashboard address (for example `https://<SIEM-IP>`) and permitted
account through the announced organizer channel. Do not share or commit
credentials. Menu names vary by installed version and permissions. On first login:

1. Click the **hamburger menu (☰)** top-left. The modules you will live in,
   in order of importance today:

   | Module | Path | What it's for |
   | --- | --- | --- |
   | **Security events** | ☰ → Explore → Discover (default view) | Every alert that has fired. Your main workspace. |
   | **Agent status** | ☰ → Agents | Is your agent connected? Green = collecting. |
   | **Integrity monitoring** (FIM) | ☰ → Modules → Security Information Management → File Integrity Monitoring | File/registry change events for C1, C2, L2B |
   | **Security Configuration Assessment** (SCA) | ☰ → Modules → Security Information Management → SCA | Hardening posture for C5, C6 |
   | **Mitre** | ☰ → Modules → Threat Hunting → MITRE ATT&CK | Maps your alerts to ATT&CK tactics — used for evidence marks |
   | **Ruleset** | ☰ → Settings → Rules | Not where you edit — see 1.3 |

2. **First check: Agents.** Click ☰ → Agents. Your machine must show
   **Status: Active** with a recent "Last keep-alive". If it's grey:

   ```
   # On the agent machine:
   sudo systemctl restart wazuh-agent        # Linux
   Restart-Service Wazuh                     # Windows (as Administrator)
   ```
   Then check the agent log for errors:

   ```
   Linux:   tail -50 /var/ossec/var/run/wazuh-agent.state 2>/dev/null || tail -50 /var/ossec/logs/ossec.log
   Windows: Get-Content "C:\Program Files (x86)\ossec-agent\ossec.log" -Tail 50
   ```
   Run service/configuration commands only on your assigned endpoint with
   permission. If connection remains unavailable, contact the track lead.
   Active status alone does not prove that the selected event channels arrive.

### 1.2 Where alerts appear and how to search

**Discover** (☰ → Explore → Discover) is a search interface over all alerts.
The three skills you need:

**a) Time-range picker** — top-right of the Discover bar. Set "Last 15
minutes" while testing; widen as needed. Alerts disappear from view simply
because the window moved — before assuming your rule didn't fire, widen the
range.

**b) The KQL search bar** — the main filter input. Examples you will use
today:

```
# All alerts from your agent
agent.name: "victim-win-01"

# All alerts above level 10
rule.level: >= 10

# One rule id
rule.id: 5710

# Combine
agent.name: "victim-lin-01" and rule.groups: "sshd"

# Failed logon alerts
rule.id: 5710 and data.srcip: 192.168.56.50
```

**c) The alert fields panel** — left sidebar. Click any field value to
filter, or click the ▶ expand arrow on an alert row to see every field. The
fields you will read most:

| Field | Meaning |
| --- | --- |
| `rule.id`, `rule.level`, `rule.description` | What matched and how severe |
| `data.win.system.eventID`, `data.win.eventdata.*` | Windows event ID and decoded event-specific fields; inspect the actual record for names |
| `data.srcip`, `data.srcuser`, `data.dstuser` | Who, from where, against whom |
| `predecoder.hostname`, `program_name` | Which log produced the event |
| `full_log` | The raw log line — the ground truth |

### 1.3 Where rules live and how you edit them

Rules are XML files on the manager. The permitted editor/deployment route
depends on the installed version, dashboard role and organizer setup; do not
assume SSH or a web editor is supplied. Use only your allocated file/rule-ID
range. The command below is an example for an explicitly authorized standalone
manager, not permission to edit a shared rules file:

```
# On the Wazuh manager:
sudo nano /var/ossec/etc/rules/local_rules.xml
```

Use the [custom-rules reference](https://documentation.wazuh.com/current/user-manual/ruleset/rules/custom.html)
for XML/group syntax. Select conditions and correlation parents from the actual
decoded source event and the task card. An SSH rule ID is not a Windows
authentication parent; copied IDs are not portable across event families.

Validate the edited rules and follow the assigned deployment procedure.
Only restart a manager when explicitly authorized; a shared restart can
affect other teams. **Check errors explicitly** rather than assuming a failed
configuration loaded. For an authorized standalone manager:

```
sudo systemctl restart wazuh-manager
sudo tail -20 /var/ossec/logs/ossec.log
# Look for: "wazuh-analysisd: INFO: Started" — good
#           "ERROR: Invalid element..." — fix the XML
```

**Rule-ID allocation:** request the assigned range/file or approval procedure
(a team-specific range such as 100700-100799 is illustrative). Do not assume
an example range is free or overwrite another team's rules.

### 1.4 Test every rule with `wazuh-logtest` before you trust it

Where access is permitted, this tests a log sample against the manager's
decoders/rules. Keep sample correlation events in the appropriate test session.
It does **not** prove that an endpoint collected an event or that an alert
arrived in the dashboard:

```
sudo /var/ossec/bin/wazuh-logtest
Starting Wazuh log test...
Type one log per line

Paste the permitted sample from your actual selected task.
Inspect Phase 1 (pre-decoding), Phase 2 (decoded fields)
and Phase 3 (matched rule).
```

If the fields are missing or incorrectly decoded, resolve collection/decoding
with the track lead before changing correlation logic. Then verify the card's
approved live event and record its actual alert when live collection is required.

---

## Part 2 — What to monitor, module by module

This is the monitoring plan for the day, expressed as "where to look and what
normal looks like". When something is abnormal you will know it because of
this section.

### 2.1 Authentication monitoring (challenges W1, L1, W1B, L1B)

**Where:** Security events, filtered to `rule.groups: authentication_failed`
or `syslog,sshd` on Linux; `windows` channel on the Windows target.

**Baseline (what normal looks like):** a handful of 4624 successful logons an
hour on the Windows target from the management IP; SSH logins on Linux from
the admin workstation only. Record what "normal" looks like in your notes
during hour one — your false-positive judgement later depends on this.

**Current card outcome:** W1B and L1B require **five or more failures from the
same lab source within two minutes**, with source IP and username. They do
not require a successful login afterwards. Keep the published threshold;
verify its boundary behavior instead of lowering it to make a test pass.
The bank guide's success-after-failures scenario is supplementary.

### 2.2 Process monitoring — Sysmon / 4688 (W2, W2B)

**Where:** Security events filtered to
`rule.groups: sysmon` or `data.win.system.eventID: 1`.

**Watch fields:** `Image` (the binary run), `CommandLine`, `ParentImage`,
`Hashes`. Anomalies that matter today: PowerShell with encoded commands,
anything from a temp path, unusual parents (a browser spawning cmd.exe).

**The allowlist idea (W2B):** don't write "alert on powershell.exe" — admins
run PowerShell. Write "alert on powershell.exe whose command line contains a
download verb". Start narrow, widen only when you confirm no false positives
on the hardened box.

### 2.3 FIM monitoring (W5B, L2B, L3B)

**Where:** Integrity Monitoring module, or Discover filtered to
`rule.groups: syscheck`.

**What generates events:** file added / modified / deleted / permissions
changed on monitored paths, and Windows registry changes on monitored keys.

**Configuration lives on the agent**, in `/var/ossec/etc/ossec.conf` (Linux)
or `C:\Program Files (x86)\ossec-agent\ossec.conf` (Windows), inside
`<syscheck>`. For L2B, merge the relevant settings into the assigned agent's
existing configuration rather than duplicating a complete config. Do not
capture sensitive account-file content diffs:

```xml
<syscheck>
  <directories check_all="yes" realtime="yes" report_changes="no">/etc/passwd,/etc/shadow</directories>
</syscheck>
```

Apply changes only with permission, then use the selected card's approved
test. L3B also needs its actual upload-directory/access-log configuration;
W5B needs the approved Windows file/registry scope. Scan timing and realtime
support depend on platform/configuration. Record observed detection delay;
do not assume any arbitrary file change will alert immediately.

**Baseline and interpretation:** severity/alerting depend on the actual
ruleset. Distinguish initial inventory from new changes and compare benign
activity. File metadata can establish a change without exposing its contents;
an account-file change or uploaded file is not by itself proof of compromise.

### 2.4 SCA — supplementary hardening, not a current task

The legacy C5/C6 labels are not among the nine current cards. Do not perform
additional hardening or submit SCA evidence unless separately approved.

**Where:** SCA module. Each agent shows a compliance score with pass/fail
counts against the loaded policy (CIS benchmark).

**What to do:** open the failing checks, read the *rationale* (each check
explains why), fix three of them on the OS, wait for the next scan (or set
`<sca><scan_on_start>yes</scan_on_start>` and restart), confirm the check
turns green. Screenshots before/after for the submission.

**Custom check:** SCA policies are YAML files in
`/var/ossec/ruleset/sca/` on the agent. Copy the stock policy, change the
policy id and name, and add a check:

```yaml
- id: 99999
  title: "DVWA default admin password must not be in use"
  condition: all
  rules:
    - 'f:/var/www/html/config/config.inc.php -> !r:^\$db_password\s*=\s*.password.;'
```

### 2.5 Active response — supplementary, not a current task

The legacy C7 label is not a current card, and W4B does not require an
automated blocking system. Do not deploy response scripts or firewall changes
on shared systems without separate approval. Any optional response must use
the installed version's valid configuration and a tested recovery procedure,
without disrupting management access or another team's telemetry.

### 2.6 MITRE ATT&CK mapping (supplementary investigation context)

The **Mitre** module visualises which techniques your alerts cover. For the
submission: map each of your rules to its technique by adding the ATT&CK id
in the rule description, e.g.:

```xml
<description>T1110: Brute force detected (5+ failures then success).</description>
<mitre><id>T1110</id></mitre>
```

A correct mapping can help explain the event, but there are no separate
mandatory ATT&CK points. Do not replace investigation or required fields with
a technique label; use the [public rubric](rules.md#judging-criteria).

---

## Part 3 — The monitoring rhythm (when to look at what)

| Phase | What you check | Why |
| --- | --- | --- |
| Setup | Agent status, recent source events and permitted `wazuh-logtest` access | Confirm live collection before claiming end-to-end detection |
| Each Loop 1 (attack) | Discover filtered to your agent, "Last 15 min" | Watch the attack arrive as events |
| Each Loop 2 (rule) | `wazuh-logtest` first, then live fire, then Discover | Catch XML errors before they cascade |
| Loop 3 (investigate) | Source event, matched condition, affected endpoint and benign alternatives | Explain what the alert establishes and what remains uncertain |
| Cross-check | Compare rules against approved benign lab activity | Count false positives without assuming a second hardened machine is supplied |
| Hour 7 (submission) | Export each fired alert as JSON (Discover → Save → Export) | That JSON is your evidence |

**Alert export for the submission:** in Discover, select the relevant alerts
→ click "Save" (bottom of search bar) → "Export" — produces a CSV/NDJSON you
include in the team folder alongside the rule XML.

---

## Part 4 — Common failures and fixes

| Symptom | Cause | Fix |
| --- | --- | --- |
| Agent grey/never connects | Wrong manager IP, firewall, or wrong key | Verify `WAZUH_MANAGER` in agent config; ping the SIEM IP |
| Alerts appear but fields empty (srcip missing) | Decoder didn't parse the log | Paste the line into `wazuh-logtest`; if Phase 2 fails, tell a track lead |
| Custom rule never fires | Invalid XML, failed deployment or wrong parent/field conditions | Check deployment/log errors through the permitted route; confirm the actual decoded event and parent |
| Rule fires on everything | Over-broad match (e.g. missing field condition) | Add field filters; test benign lines with `wazuh-logtest` |
| Active response blocks nothing | Script not enabled or `<location>` wrong | Confirm `firewall-drop` present in ossec.conf; check `/var/ossec/logs/active-responses.log` |
| FIM events don't arrive | `realtime` missing or path typo | Restart agent; check `ossec.log` for syscheck init lines |
| Rule fired but disappeared | Time-range picker | Widen to 24h in Discover |
| Two teams share rule ids | ID collision | Use your allocated range; renumber and restart |

---

## Part 5 — References (official documentation)

Use [Curated Resources](resources.md) for the current official installation,
collection, decoding, rule-testing, FIM and source references, mapped to the
nine cards. Confirm access in advance; neither venue internet nor offline
copies are guaranteed. Do not give a deliberately vulnerable endpoint
internet access just to read documentation.

---

## Part 6 — Writeup guidance: what a complete submission looks like

Use one team submission folder with per-task evidence/README sections.
The layout below is illustrative; only include configuration files relevant
to your selected cards:

```
team07_submission/
├── README.md                 ← one-page summary per challenge (see skeleton below)
├── rules/
│   └── local_rules.xml       ← your full custom ruleset
├── alerts/
│   ├── w1_attack_fired.json  ← exported alerts proving each rule fired
│   └── w1_hardened_quiet.json← the false-positive test result
├── configs/
│   ├── ossec_agent.conf.diff ← agent config changes (FIM etc.)
│   └── other_collection_changes.diff
└── screenshots/              ← supplementary; relevant alerts/logs are primary
```

**README skeleton per challenge (copy this):**

```
## Task W1B — Failed-logon detection
### What we built
<rule id="100700"> ... (paste XML) ...

### Proof the attack was detected
- Approved failure-only test at HH:MM from <lab-source>
- Alert fired at HH:MM:SS: <paste the alert JSON>
- Fields captured: srcip, srcuser, rule.level

### MITRE mapping
- T1110 Brute Force (sub-technique T1110.001 password guessing)

### Collection and investigation
- Security-channel configuration and relevant decoded fields
- Affected endpoint/account and failure count/window
- What this establishes, legitimate alternatives and what remains unknown

### False-positive test
- Ran <approved benign activity> on the designated lab endpoint
- Record the actual duration, expected result and observed alerts

### Changed-input test
- Repeat using an approved changed account/source
- Compare expected and actual output; identify evidence files

### What we would improve
- <honest note — e.g. "our frequency window would miss a slow spray">
```

**How your evidence supports the public technical rubric:**

| Submission section | Rubric component it earns |
| --- | --- |
| Required behaviors/fields detected | Detection accuracy and coverage (30 points) |
| Rule conditions, correlation and false-positive handling | Detection rule quality, specificity and robustness (20 points) |
| Positive/benign/changed-input results and traceable exports | Validation, testing and evidence quality (15 points) |
| Event context, significance, legitimate alternatives and uncertainty | Investigation quality and alert interpretation (15 points) |
| Required channel/FIM/audit settings and functioning collection | Log-source collection and system configuration (10 points) |
| README, rule/configuration files and repeatable steps | Documentation and reproducibility (10 points) |
| **Total for the selected task set** | **100 points** |

These allocations total **100 points for your selected task set**, not per
rule or task. Use the [Track Rules](rules.md) for the full rubric, authorized
scope, score averaging and qualification. Technical demonstrations verify
evidence; no formal pitch or slides are required.

Keep the README current as you work. Dedicated bank-lab roles are suggestions,
not extra requirements for the nine cards.

---

## Part 7 — Choosing a starting rule

Use the decoded source and current card, not legacy W1/W2 labels or a copied
rule number. W1B/L1B require failures-only correlation; W2B concerns download
process behavior, not LSASS access. W3B concerns Event 7045 paths outside
Windows, not an unrelated directory policy. Consult the current custom-rule
reference, use your assigned IDs and preserve actual test results. No validated
nine-card starter ruleset is supplied by the removed legacy examples.
