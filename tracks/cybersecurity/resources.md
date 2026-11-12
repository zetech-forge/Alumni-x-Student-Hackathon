---
title: Curated Resources
parent: Cybersecurity
grand_parent: Hackathon Tracks
nav_order: 2
---

# Cybersecurity: Curated Resources

Use references for your **selected cards**, not as a checklist of installations. **Essential** means relevant to that card or assigned setup role; **supplementary** means additional explanation or an alternative source. Documentation is free to read.

**Work only on supplied or explicitly authorized lab systems.** Public documentation does not authorize public-target testing. Obtain lab access privately; never publish credentials, private addresses or sensitive records.

**Version guidance:** use documentation matching the supplied lab. Wazuh `/current/` and GitHub `master` may differ from its installed release. Ubuntu 24.04, RHEL 9, Apache 2.4 and upstream OpenSSH references below are version-specific examples, not required lab versions. Confirm architecture, versions and permissions before installing or changing anything.

## Wazuh fundamentals

| Resource | Official source | Use | Cards | Priority |
|---|---|---|---|---|
| [Wazuh architecture](https://documentation.wazuh.com/current/getting-started/architecture.html) | Wazuh | Understand agents, server/manager, indexer and dashboard, and the event-to-alert path. | All | Essential |
| [Quickstart and deployment sizing](https://documentation.wazuh.com/current/quickstart.html) | Wazuh | Understand central deployment; install only if assigned, not on every participant laptop. | All | Supplementary; essential if deployment is assigned |
| [Agent installation](https://documentation.wazuh.com/current/installation-guide/wazuh-agent/index.html) | Wazuh | Supported endpoint setup/enrollment when required by the confirmed architecture. | All | Essential if agent setup is assigned |
| [Dashboard guide](https://documentation.wazuh.com/current/user-manual/wazuh-dashboard/index.html) | Wazuh | Locate assigned endpoints, filter time ranges and inspect alert details. Menus depend on version/role. | All | Essential |
| [Log-collection configuration](https://documentation.wazuh.com/current/user-manual/capabilities/log-data-collection/configuration.html) | Wazuh | Collect the selected Windows channels, Linux authentication, application or audit records. | W1B-W4B, L1B, L3B-L4B | Essential |

## Wazuh rules and detection engineering

| Resource | Official source | Use | Cards | Priority |
|---|---|---|---|---|
| [Custom rule creation](https://documentation.wazuh.com/current/user-manual/ruleset/rules/custom.html) | Wazuh | Rule files, custom IDs and safe extensions to installed rules. Use assigned IDs/deployment permissions. | All | Essential |
| [Rule syntax and matching](https://documentation.wazuh.com/current/user-manual/ruleset/ruleset-xml-syntax/rules.html) | Wazuh | Parent/field conditions, levels, frequency, timeframe and same-source correlation. | All; especially W1B/L1B | Essential |
| [Testing decoders and rules](https://documentation.wazuh.com/current/user-manual/ruleset/testing.html) | Wazuh | Use `wazuh-logtest` to inspect decoding and matches; validate observed trigger counts and changed inputs. | All; especially W1B/L1B | Essential |
| [Decoder concepts](https://documentation.wazuh.com/current/user-manual/ruleset/decoders/index.html) | Wazuh | Understand how source records become fields and investigate missing/incorrect decoding. | All | Supplementary |

**W1B and L1B:** prioritize syntax/correlation and rule testing. Both require **five or more failures from one source within two minutes**. Verify the installed parent and actual boundary behavior; copying a stock rule's frequency does not establish compliance. Sample testing does not prove live endpoint-to-dashboard delivery.

## Windows and Linux source references

### Windows security monitoring

| Resource | Official source | Use | Cards | Priority |
|---|---|---|---|---|
| [Security Event 4625](https://learn.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4625) | Microsoft | Interpret failed-logon account/source fields. Follow the article's Windows applicability notes. | W1B | Essential |
| [Security Event 4688](https://learn.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4688) | Microsoft | Understand process creation, command-line auditing and available creator/parent context. | W2B | Essential if this is the configured source |
| [Sysmon documentation](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon) | Microsoft Sysinternals | Process creation and parent/command-line telemetry where configured; not a universal extra installation. | W2B | Essential if Sysmon is the configured source |
| [Windows System rules](https://github.com/wazuh/wazuh/blob/master/ruleset/rules/0590-win-system_rules.xml) | Wazuh project | Inspect the upstream Event 7045 service-installation handling; compare with the installed version, not a copied parent ID. | W3B | Essential |
| [Defender events and troubleshooting](https://learn.microsoft.com/en-us/defender-endpoint/troubleshoot-microsoft-defender-antivirus) | Microsoft | Interpret 5001 (real-time protection disabled) and 5000 (enabled). Use the collection guide above for the Defender Operational channel. | W4B | Essential |
| [File Integrity Monitoring](https://documentation.wazuh.com/current/user-manual/capabilities/file-integrity/index.html) | Wazuh | Understand baselines and additions/modifications/deletions on Windows and Linux. | W5B, L2B-L3B | Essential |
| [syscheck and Windows Registry configuration](https://documentation.wazuh.com/current/user-manual/reference/ossec-conf/syscheck.html#windows-registry) | Wazuh | Distinguish `<directories>` from `<windows_registry>`, Registry views and scheduled scanning. Consult the page's timing options too. | W5B; timing/configuration also L2B-L3B | Essential |

Use only a disposable authorized VM for W4B and immediately restore protection. For W5B, use harmless file/value changes; a baseline or first scan is not proof of a new persistence event.

### Linux security monitoring

| Resource | Official source | Use | Cards | Priority |
|---|---|---|---|---|
| [OpenSSH server configuration](https://man.openbsd.org/sshd_config) | OpenSSH/OpenBSD | Logging concepts such as facility and level. The actual authentication file/journal depends on the assigned Linux system. | L1B | Supplementary |
| [auditd manual](https://manpages.ubuntu.com/manpages/noble/man8/auditd.8.html) | Ubuntu manpages | Understand the audit daemon and configuration context; use the supplied audit feed rather than inventing shared-host rules. | L4B | Essential |
| [Auditing the system](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html/security_hardening/auditing-the-system_security-hardening) | Red Hat, RHEL 9 | Interpret related audit records, syscall results and identities. Adapt concepts to the actual distribution. | L4B | Supplementary |

Use **log collection** above for L1B's assigned SSH source and **FIM/syscheck** for L2B and L3B. Disable sensitive account-file content diffs; do not export password hashes. For L4B, executable/arguments and effective user are not automatically proof of network success: inspect actual destination/outcome telemetry and explain its limits.

## Web application security monitoring

| Resource | Official source | Use | Cards | Priority |
|---|---|---|---|---|
| [DVWA project documentation](https://github.com/digininja/DVWA) | Official DVWA project | Understand the designated training application's setup and upload context. Use the approved instance, not a public target or a new unapproved installation. | L3B-L4B | Essential |
| [Apache access logs](https://httpd.apache.org/docs/2.4/logs.html#accesslog) | Apache HTTP Server 2.4 | Interpret request paths, methods, status and source information if Apache is the supplied server. | L3B | Essential if Apache is configured |
| [NGINX access-log module](https://nginx.org/en/docs/http/ngx_http_log_module.html) | NGINX | Equivalent access-log format reference if NGINX is used; not an additional installation requirement. | L3B | Supplementary alternative; essential if NGINX is configured |

For L3B, combine the approved upload directory's FIM records with the configured server logs. Use harmless PHP artifacts and relate file/request evidence by path and time. A request does not prove malicious execution. For L4B, a web access log alone does not establish outbound process identity. Never expose DVWA to the internet.

## Detection validation and investigation

Start with the official **rule-testing** and **dashboard** guides above, then apply this repeatable workflow to each selected card:

1. Record the approved activity, expected event/alert and required fields.
2. Inspect the raw event, decoded fields and matching rule.
3. Test the positive case and applicable count/window or scan boundaries.
4. Repeat with an approved changed indicator and compare benign activity.
5. Explain missed detections, unintended matches and legitimate reasons for an alert; do not tune away behavior the card requires.
6. Preserve sanitized records, timestamps, rule/configuration versions and expected/observed results so another authorized person can reproduce the test.

These are validation practices, not extra exercises or permission to test new targets. Redact secrets without removing the context needed to interpret the alert.

## Participant guidance

| Existing guide | Purpose | Cards | Priority |
|---|---|---|---|
| [Challenge cards](challenges.md) | Required behavior, telemetry, tests and cleanup. | All selected | Essential |
| [Track Rules](rules.md) | Authorization, selection, submission evidence and the current 100-point rubric. | All | Essential |
| [Content & Curriculum](content.md) | Choose relevant modules and bootcamp/preparation priorities. | All | Essential |
| [Participant guide](1_STUDENT_GUIDE.md) | Follow the practical access-to-evidence workflow. | All selected | Essential |
| [Wazuh Analyst Playbook](3_WAZUH_MANUAL.md) | Public operating guidance and permitted troubleshooting; not an answer key. | All selected | Supplementary |

Lab setup artifacts and unapproved extra simulations are not participant prerequisites. Ask the Technical Lead for the confirmed access/setup procedure; do not treat a repository artifact as a validated lab.
