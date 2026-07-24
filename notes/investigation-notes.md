# Investigation Notes

## Lab Summary

This investigation focused on monitoring Windows password reset activity using native Windows Security logs and Wazuh.

Rather than relying on Sysmon, the investigation validated the complete Windows Security logging pipeline—from event generation to Wazuh ingestion.

---

## Analyst Methodology

The investigation followed a structured DFIR workflow:

1. Verify Windows audit configuration.
2. Generate password reset activity.
3. Validate Event ID 4724 in Event Viewer.
4. Confirm the event using PowerShell.
5. Verify Wazuh agent health.
6. Confirm raw event ingestion.
7. Compare archives.json with alerts.json.
8. Correlate investigative findings.
9. Document forensic evidence.

---

## Investigation Scenario

A Windows administrator reset a local account password.

The investigation aimed to determine:

- Whether Windows generated Event ID 4724.
- Whether Wazuh successfully collected the event.
- Whether the event generated an alert.
- Whether any logging issues existed.

---

## Evidence Collected

### Evidence 1 – Windows Audit Policy

Collected:

- Audit Policy Change configuration

Finding:

Verified prerequisite logging was enabled.

---

### Evidence 2 – Event Viewer

Collected:

- Event ID 4724

Finding:

Confirmed successful password reset auditing.

---

### Evidence 3 – PowerShell Validation

Command Used

```powershell
Get-WinEvent -FilterHashtable @{
LogName='Security'
Id=4724
} -MaxEvents 5
```

Finding:

Confirmed Windows recorded the password reset event.

---

### Evidence 4 – Wazuh Agent

Collected:

- Agent status
- Last Keep Alive

Finding:

Confirmed active communication with the manager.

---

### Evidence 5 – archives.json

Collected:

- Raw Event ID 4724

Finding:

Confirmed successful event ingestion into Wazuh.

---

### Evidence 6 – alerts.json

Collected:

- Rule matching status

Finding:

Illustrated the distinction between raw event ingestion and rule-generated alerts.

---

## DFIR Analysis

The investigation confirmed that Windows Security logs, PowerShell, and Wazuh all reported consistent evidence.

Validation through archives.json demonstrated successful collection even when alert generation required further analysis.

---

## MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---------|-----------|----|
| Credential Access | Account Manipulation | T1098 |
| Discovery | Account Discovery | T1087 |

---

## Analyst Observations

- Event ID 4724 is generated only for password resets performed on another account.
- Windows Audit Policy must be correctly configured.
- PowerShell provides reliable independent event validation.
- archives.json confirms raw event collection.
- alerts.json depends on Wazuh rule matching.
- Event generation and alert generation are separate stages of the logging pipeline.

---

## Conclusion

The investigation successfully reconstructed the Windows password reset event lifecycle from generation through SIEM ingestion. By validating each stage independently, the investigation demonstrated an effective DFIR methodology for credential-related security events.
