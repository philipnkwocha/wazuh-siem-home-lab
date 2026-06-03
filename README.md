# Wazuh SIEM Home Lab — Privilege Escalation Detection

**Analyst:** Philip Nkwocha  
**Security+** | Cybersecurity Analyst  
**Lab completed:** March 2026

---

## Project Overview

This project documents the deployment of a Wazuh SIEM environment across a 
multi-OS home lab, including custom detection rule development, log analysis, 
alert triage, and incident response documentation.

The lab simulates a real SOC analyst workflow — from initial SIEM deployment 
through detection engineering, true/false positive analysis, and formal 
incident reporting.

---

## Lab Environment

| Component | Details |
|---|---|
| SIEM Platform | Wazuh v4.14.2 |
| Manager OS | Ubuntu 24.04 LTS |
| Agent 1 | Ubuntu (empire) — IP 10.0.2.15 |
| Agent 2 | Windows 10 VM |
| Hypervisor | VirtualBox |

---

## What Was Built

- Deployed Wazuh manager on Ubuntu with two enrolled agents (Linux + Windows)
- Configured UFW firewall rules for agent communication ports (1514 UDP / 1515 TCP)
- Ingested logs from multiple sources: auth.log, syslog, auditd, Windows Event Log
- Wrote custom detection rule targeting privilege escalation via sudo abuse
- Performed alert triage — identified true positive (/etc/shadow access) and false positive (PAM session noise)
- Tuned alerts to reduce false positive volume while preserving detection fidelity
- Documented findings in a formal incident report (IR-2026-001)

---

## Detection Use Case — Privilege Escalation

**MITRE ATT&CK:** T1548.003 — Sudo and Sudo Caching  
**Trigger:** User 'empire' executed `sudo cat /etc/shadow`  
**Why it matters:** /etc/shadow contains hashed passwords. Reading this file 
via sudo is a known credential harvesting technique and is not part of normal 
operations.

**Result:** Custom Wazuh rule fired correctly. Alert tuned to suppress benign 
PAM session-close noise. Incident documented as TRUE POSITIVE.

---

## Project Documents

| Document | Description |
|---|---|
| `IR-2026-001_Privilege_Escalation.docx` | Full incident report with timeline, IOCs, MITRE mapping, and recommendations |

---

## Skills Demonstrated

`Wazuh SIEM` `Log Analysis` `Detection Engineering` `Alert Triage`  
`Incident Response` `Linux Hardening` `Windows Hardening`  
`MITRE ATT&CK` `True/False Positive Analysis` `UFW Firewall`  
`auditd` `SSH Hardening` `Fail2Ban` `AppArmor`

---

## Related Projects

- Ubuntu System Hardening (CIS-aligned, 12-step process)
- Windows System Hardening (SOC-focused, Advanced Audit Policy)
- Router Hardening (Xfinity gateway — WPA3, UPnP disable, remote management)
- Wazuh Agent Deployment — Windows + Ubuntu cross-platform setup

---

*This lab was built to develop hands-on SOC analyst skills and demonstrate 
real-world security operations capability.*
