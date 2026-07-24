# wazuh-windows-password-reset-investigation-dfir-lab
## Overview

This Digital Forensics and Incident Response (DFIR) lab investigates Windows password reset activity using native Windows Security auditing and Wazuh.

Unlike Sysmon-based investigations, this lab relies entirely on Windows Security logs and Wazuh event collection to validate how password reset events are generated, ingested, and analyzed.

A significant part of the investigation focused on troubleshooting why Event ID 4724 was not appearing, validating Windows audit policies, confirming Wazuh agent connectivity, and verifying raw event ingestion through `archives.json`.

---

# Executive Summary

This investigation demonstrates how Windows password reset events can be monitored using Wazuh without Sysmon.

The investigation covered the complete event lifecycle:

- Understanding the difference between password change and password reset events.
- Configuring Windows Audit Policy.
- Generating Event ID 4724.
- Validating event generation using Event Viewer and PowerShell.
- Confirming Wazuh agent communication.
- Verifying raw log ingestion through `archives.json`.
- Understanding why events may appear in archives before matching alert rules.

The investigation highlights the importance of validating every stage of the Windows → Wazuh logging pipeline during DFIR investigations.

---

# Learning Objectives

- Understand Windows Event ID 4724.
- Differentiate between Event IDs 4723 and 4724.
- Configure Windows Audit Policy.
- Validate Security log generation.
- Verify Wazuh agent connectivity.
- Confirm event ingestion into Wazuh.
- Understand the difference between archives.json and alerts.json.
- Perform structured DFIR troubleshooting.

---

# Skills Demonstrated

- Windows Security Log Analysis
- Password Reset Investigation
- Windows Audit Policy Configuration
- Event Viewer Analysis
- PowerShell Event Validation
- Wazuh Agent Verification
- Raw Event Validation
- Wazuh Troubleshooting
- Evidence Correlation
- Digital Forensics Documentation
- MITRE ATT&CK Mapping

---

# Tools Used

- Wazuh Dashboard (Discover)
- Windows Event Viewer
- Windows Security Log
- Windows PowerShell
- auditpol
- net user
- Wazuh Agent
- Wazuh Manager
- archives.json
- alerts.json

---

# Lab Environment

| Component | Details |
|-----------|---------|
| SIEM | Wazuh 4.12 |
| Endpoint | Windows 11 Pro |
| Server | Oracle Linux 9 |
| Investigation Type | Windows DFIR |
| Event Source | Windows Security Log |
| Event ID | 4724 |
| Sysmon | Not Used |

---

# Investigation Scenario

An administrator receives a report that a local user's password has been reset.

As the DFIR analyst, the objectives were to determine:

- Was a password reset performed?
- Was the correct Windows audit policy enabled?
- Did Windows generate Event ID 4724?
- Did Wazuh receive the event?
- Was the event successfully ingested into the SIEM?
- If alerts were missing, where in the ingestion pipeline did the issue occur?

---

# Investigation Workflow

1. Verify Windows Audit Policy.
2. Generate password reset activity.
3. Validate Event ID 4724 in Event Viewer.
4. Verify event using PowerShell.
5. Confirm Wazuh agent health.
6. Validate event forwarding.
7. Inspect `archives.json`.
8. Compare `archives.json` with `alerts.json`.
9. Correlate investigative findings.
10. Document forensic evidence.

---

# MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---------|-----------|----|
| Credential Access | Account Manipulation | T1098 |
| Discovery | Account Discovery | T1087 |

### Why This Matters

Password reset events can indicate legitimate administrative activity or malicious attempts to gain persistent access. Verifying both Windows audit configuration and Wazuh ingestion ensures that critical credential-related events are available during incident response.

---

# Evidence Collected

- Windows Audit Policy
- Event ID 4724
- Event Viewer logs
- PowerShell output
- Wazuh Agent status
- archives.json entries
- alerts.json validation
- Wazuh Discover results

---

# Evidence Correlation

| Evidence Source | Information Obtained | Investigation Value |
|-----------------|---------------------|--------------------|
| auditpol | Audit configuration | Verified logging prerequisites |
| Event Viewer | Event ID 4724 | Confirmed Windows generated event |
| PowerShell | Event validation | Independent verification |
| Agent Control | Agent status | Confirmed endpoint connectivity |
| archives.json | Raw event | Confirmed Wazuh ingestion |
| alerts.json | Rule matching | Determined alert generation status |

---

# Investigation Findings

- Windows successfully generated Event ID 4724.
- Audit Policy Change logging was properly configured.
- Wazuh agent remained connected throughout the investigation.
- Event forwarding from Windows to Wazuh was successful.
- Raw events were confirmed inside `archives.json`.
- The investigation demonstrated that ingestion can be validated independently of rule-based alert generation.

---

# Key Takeaways

- Event generation must always be verified before investigating SIEM ingestion.
- archives.json confirms raw event collection.
- alerts.json only contains events that match Wazuh rules.
- Windows audit configuration is a critical prerequisite for credential-related investigations.
- Understanding the complete event pipeline improves DFIR accuracy.

---

