# Wazuh Analyst Playbook — Operating Instructions for the Event

This is the day-one working manual for the Wazuh stack. The challenge cards
tell you *what* to build; this tells you *how* to navigate the tool, where
everything lives, what good monitoring looks like, and where the official
documentation is when you need the exact syntax. Keep it open in a browser
tab next to the dashboard all day.

---

## Part 1 — Your first 15 minutes in Wazuh

### 1.1 Log in and orient yourself

The dashboard is at `https://<SIEM-IP>` (on your table card). Username and
password are on the same card. On first login:

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
   If it still won't connect after two restarts — call a track lead. Nothing
   you build counts until this is green.

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
| `data.win.eventdata.*` | Parsed Windows event fields (eventid, subjectUserName…) |
| `data.srcip`, `data.srcuser`, `data.dstuser` | Who, from where, against whom |
| `predecoder.hostname`, `program_name` | Which log produced the event |
| `full_log` | The raw log line — the ground truth |

### 1.3 Where rules live and how you edit them

You do **not** edit rules through the dashboard. Rules are XML files on the
manager. For this event, you will create one file per team on the manager
(or paste it via the organiser-provided web snippet at the SIEM console):

```
# On the Wazuh manager:
sudo nano /var/ossec/etc/rules/local_rules.xml
```

Custom rules go inside the existing `<group>` structure, or in a new group:

```xml
<group name="team07,attack,">
  <!-- a custom rule starting from the built-in sshd brute-force parent -->
  <rule id="100700" level="10" frequency="5" timeframe="120">
    <if_matched_sid>5710</if_matched_sid>
    <description>Multiple SSH auth failures from same source.</description>
    <same_srcip />
  </rule>
</group>
```

After every edit, restart the manager and **check the log for errors** — a
bad XML file silently drops ALL your custom rules, not just the broken one:

```
sudo systemctl restart wazuh-manager
sudo tail -20 /var/ossec/logs/ossec.log
# Look for: "wazuh-analysisd: INFO: Started" — good
#           "ERROR: Invalid element..." — fix the XML
```

**Rule-ID allocation:** each team gets a range on its table card
(e.g. team 07 → 100700–100799). Two teams using the same ID range will
overwrite each other's rules — the range is yours alone.

### 1.4 Test every rule with `wazuh-logtest` before you trust it

This is the single most useful tool today. It replays a log line through the
full ruleset live, in a shell:

```
sudo /var/ossec/bin/wazuh-logtest
Starting Wazuh log test...
Type one log per line

Nov 14 20:26:31 APP-SRV-02 sshd[3312]: Accepted password for svc_backup from 203.0.113.77 port 51023 ssh2

**Phase 1: Completed pre-decoding.
**Phase 2: Completed decoding.
       name: 'sshd'
       srcip: '203.0.113.77'
       srcuser: 'svc_backup'
**Phase 3: Completed filtering (rules).
       id: '5760'
       level: '5'
       description: 'sshd: Attempt to login using a non-existent user'
**Alert to be generated.
```

Paste the sample log line from your challenge card, watch which phase decodes
what, and see exactly which rule matches. If Phase 2 shows no decoder or the
wrong one, no amount of rule-writing will help — tell a track lead.

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

**What the attack looks like:** a burst of 4625 / "Failed password" events
from one external source, then — the critical bit — a 4624 / "Accepted
password" from the same source. Detection = the *combination*, which needs
the frequency + `same_srcip` pattern from 1.3.

**Alert threshold guidance for beginners:** frequency 5 within 120 seconds.
If your lab traffic is slower, 4 in 180 s. Tune until the practice attack
fires and normal activity doesn't.

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

### 2.3 FIM monitoring (C1, C2, L2B, L3B)

**Where:** Integrity Monitoring module, or Discover filtered to
`rule.groups: syscheck`.

**What generates events:** file added / modified / deleted / permissions
changed on monitored paths, and Windows registry changes on monitored keys.

**Configuration lives on the agent**, in `/var/ossec/etc/ossec.conf` (Linux)
or `C:\Program Files (x86)\ossec-agent\ossec.conf` (Windows), inside
`<syscheck>`. Minimum useful block for L2B:

```xml
<syscheck>
  <directories check_all="yes" realtime="yes" report_changes="yes">/var/www/html/hackable/uploads</directories>
  <directories check_all="yes" report_changes="yes">/etc/passwd,/etc/shadow,/etc/sudoers</directories>
</syscheck>
```

After editing agent config: restart the agent, then trigger a test change
(`touch /var/www/html/hackable/uploads/test.txt`) and confirm the alert
within ~1 minute. `realtime` is instant; without it, syscheck scans on a
schedule (default 12h — far too slow for today).

**Baseline rule:** stock syscheck events fire at level 0–3 (no alert). Your
custom rule promotes them. The gradient matters: file *added* to an upload
dir = interesting; `/etc/passwd` *modified* = higher severity; the *content
diff* contains `eval(` = highest.

### 2.4 SCA — hardening posture (C5, C6)

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

### 2.5 Active response (C7, W4B-advanced)

Active responses tie a rule to a script. Configuration on the manager,
`/var/ossec/etc/ossec.conf`:

```xml
<active-response>
  <command>firewall-drop</command>
  <location>srcip</location>
  <rules_id>100700</rules_id>   <!-- your brute-force rule -->
  <timeout>600</timeout>        <!-- block for 10 minutes -->
</active-response>
```

**Test procedure:** fire the trigger rule (run your practice attack), watch
the alert, then verify the block is real:

```
# On the Linux target, during an active block:
sudo iptables -L INPUT -n | grep <attacker-ip>

# NOTE: any Windows image works (10/11/Server 2016+). What you need is
# host-only networking, this agent connected, and Sysmon installed.
# On Windows target:
netsh advfirewall firewall show rule name=all | findstr <attacker-ip>
```

Then confirm the timeout released it (10 min later, same command shows it
gone). A block you cannot demonstrate releasing is an availability failure in
the report.

**Safety valves:** never set an active response on a rule that fires on
legitimate admin activity, and always whitelist the SIEM + management IPs —
`<white_list>` entries in the active-response config, and verify by loging
in from the management IP during a live block.

### 2.6 MITRE ATT&CK mapping (evidence marks)

The **Mitre** module visualises which techniques your alerts cover. For the
submission: map each of your rules to its technique by adding the ATT&CK id
in the rule description, e.g.:

```xml
<description>T1110: Brute force detected (5+ failures then success).</description>
<mitre><id>T1110</id></mitre>
```

This is what earns the "correct MITRE mapping" evidence marks — a rule that
fires but doesn't declare its technique scores less.

---

## Part 3 — The monitoring rhythm (when to look at what)

| Phase | What you check | Why |
| --- | --- | --- |
| Hour 0 (setup) | Agent Active, Discover shows heartbeats, test `wazuh-logtest` | Without telemetry nothing counts |
| Each Loop 1 (attack) | Discover filtered to your agent, "Last 15 min" | Watch the attack arrive as events |
| Each Loop 2 (rule) | `wazuh-logtest` first, then live fire, then Discover | Catch XML errors before they cascade |
| Loop 3 (control) | Active-response execution alerts + FIM + SCA | The control must leave telemetry too |
| Hour 6 (cross-check) | Run every rule against the hardened box | Count and fix false positives |
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
| Custom rule never fires | XML error (silently drops file) or bad `if_matched_sid` | Check ossec.log after restart; confirm the parent rule id exists |
| Rule fires on everything | Over-broad match (e.g. missing field condition) | Add field filters; test benign lines with `wazuh-logtest` |
| Active response blocks nothing | Script not enabled or `<location>` wrong | Confirm `firewall-drop` present in ossec.conf; check `/var/ossec/logs/active-responses.log` |
| FIM events don't arrive | `realtime` missing or path typo | Restart agent; check `ossec.log` for syscheck init lines |
| Rule fired but disappeared | Time-range picker | Widen to 24h in Discover |
| Two teams share rule ids | ID collision | Use your allocated range; renumber and restart |

---

## Part 5 — References (official documentation)

These are the pages that answer the "how exactly do I…" questions. All are
reachable from the venue if the SIEM VM has internet (the defender stack is
allowed out); otherwise organisers will print the marked-up set and put it on
USB.

**Core**

- Wazuh documentation home —
  https://documentation.wazuh.com/current/
- Ruleset syntax (the definitive page for every tag used today) —
  https://documentation.wazuh.com/current/user-manual/ruleset/ruleset-xml-syntax.html
- Custom rules how-to —
  https://documentation.wazuh.com/current/user-manual/ruleset/custom.html
- Decoders —
  https://documentation.wazuh.com/current/user-manual/ruleset/decoders.html
- `wazuh-logtest` reference —
  https://documentation.wazuh.com/current/user-manual/ruleset/testing.html
- Default rule numbering map —
  https://documentation.wazuh.com/current/user-manual/ruleset/ruleset-xml-syntax.html#logical-fields (and the ruleset source tree under `/var/ossec/ruleset/rules/` on the manager)

**Modules used today**

- File Integrity Monitoring —
  https://documentation.wazuh.com/current/user-manual/capabilities/file-integrity/index.html
- SCA —
  https://documentation.wazuh.com/current/user-manual/capabilities/sec-config-assessment/index.html
- SCA use cases / custom checks —
  https://documentation.wazuh.com/current/user-manual/capabilities/sec-config-assessment/use-case.html
- Active response overview —
  https://documentation.wazuh.com/current/user-manual/manager/manual-active-response.html
- Default active-response scripts (firewall-drop etc.) —
  https://documentation.wazuh.com/current/user-manual/manager/manual-active-response.html#default-active-response-scripts
- Windows event channel log collection —
  https://documentation.wazuh.com/current/user-manual/reference/ossec-conf/localfile.html#windows-eventchannel
- Sysmon integration with Wazuh —
  https://documentation.wazuh.com/current/proof-of-concept-guide/integrate-sysmon-with-wazuh.html
- Agent management (enrol, restart, troubleshoot) —
  https://documentation.wazuh.com/current/user-manual/agents/index.html

**Browsing alerts**

- Wazuh dashboard (OpenSearch Dashboards basics) —
  https://documentation.wazuh.com/current/user-manual/wazuh-dashboard/index.html

**Telemetry references for the attacks**

- Windows security event IDs glossary (4624/4625/4697/4720 etc.) —
  https://learn.microsoft.com/en-us/windows/security/threat-protection/auditing/audit-events
- Sysmon event reference —
  https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon
- MITRE ATT&CK technique index —
  https://attack.mitre.org/

---

## Part 6 — Writeup guidance: what a complete submission looks like

Each challenge submission is a folder with:

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
│   └── active_response.conf
└── screenshots/              ← only supporting; the JSON/XML is primary
```

**README skeleton per challenge (copy this):**

```
## Challenge W1 — Brute force then success
### What we built
<rule id="100700"> ... (paste XML) ...

### Proof the attack was detected
- Attack run at HH:MM from <attacker-ip> (nmap/hydra command attached)
- Alert fired at HH:MM:SS: <paste the alert JSON>
- Fields captured: srcip, srcuser, rule.level

### MITRE mapping
- T1110 Brute Force (sub-technique T1110.001 password guessing)

### Prevention applied
<active-response config pasted>
- Verified: attacker IP blocked at HH:MM (iptables output pasted)
- Verified: released after 600s
- Verified: SIEM and management IPs unaffected (login log pasted)

### False-positive test
- Ran <benign activity> against the hardened box for 30 minutes
- Rule produced 0 alerts (export attached)

### What we would improve
- <honest note — e.g. "our frequency window would miss a slow spray">
```

**Marking map (same rubric as the master plan):**

| Submission section | Rubric component it earns |
| --- | --- |
| Rule XML + why this logic | Detection engineering (25%) |
| Alert JSON with named fields + MITRE id | SIEM evidence quality (25%) |
| Attack reproduction notes | Vulnerability identification (20%) |
| Control config + block verification + release test | Prevention and containment (20%) |
| README clarity + hardened-box test | Reporting (10%) |

The teams that score best write the README *as they go*, not at 17:30. The
scribe role exists for exactly this.

---

## Part 7 — Appendix: rule templates for the three starter detections

These are the starting points referenced in the challenge cards. They are
*starting points* — each needs tuning to your lab and each has a deliberate
gap the atomic test will find.

**Brute force then success (W1/L1 shape):**

```xml
<group name="team,brute_force,">
  <rule id="100700" level="10" frequency="5" timeframe="180">
    <if_matched_sid>5710</if_matched_sid>      <!-- Windows 4625 failures -->
    <description>T1110: $(dstuser) auth failures followed by success.</description>
    <same_srcip />
  </rule>
  <rule id="100701" level="12">
    <if_matched_sid>100700</if_matched_sid>
    <if_sid>5716</if_sid>                       <!-- Windows 4624 success -->
    <description>T1110: Successful logon after brute force from $(srcip).</description>
  </rule>
</group>
```

(Linux shape: `if_matched_sid` 5712 for sshd failures, parent to 5715/5710
"Accepted password" — check the actual ids on your manager with
`grep -rn "sshd" /var/ossec/ruleset/rules/01_syslog_rules.xml | head`.)

**LSASS access (W2 shape):**

```xml
<group name="team,credential_access,">
  <rule id="100710" level="13">
    <if_group>sysmon_event1_10</if_group>       <!-- depends on local sysmon rules; verify id -->
    <field name="win.eventdata.targetImage">lsass.exe$</field>
    <description>T1003: process access to LSASS ($(win.eventdata.image)).</description>
  </rule>
</group>
```

Check the shipped sysmon rule group name on your manager:
`grep -rn "eventid.*10\b" /var/ossec/ruleset/rules/*sysmon* | head`.

**Service installed outside system paths (W3 shape):**

```xml
<group name="team,persistence,">
  <rule id="100720" level="12">
    <if_sid>92321</if_sid>                      <!-- shipped: new service installed -->
    <field name="win.system.message">^C:\\(?!(Windows|Program Files))</field>
    <description>T1543.003: new service outside standard paths: $(win.eventdata.serviceName).</description>
  </rule>
</group>
```

Confirm the shipped service-install rule id on your manager:
`grep -rn "7045" /var/ossec/ruleset/rules/ | head`.

The id numbers in these templates are illustrative — **verify against your
manager's actual ruleset** (the commands above) before trusting them, and
remember your allocated ID range for your own rules.
