# Investigation Timeline

| Time | Activity | Evidence |
|------|----------|----------|
| 07:15 | Verified Windows Audit Policy | auditpol |
| 07:20 | Generated password reset activity | net user |
| 07:31 | Windows generated Event ID 4724 | Event Viewer |
| 07:33 | Verified event using PowerShell | Get-WinEvent |
| 07:40 | Verified Wazuh agent health | agent_control |
| 07:45 | Checked event forwarding | Wazuh Agent |
| 07:50 | Confirmed ingestion in archives.json | archives.json |
| 07:55 | Compared alerts.json | Rule validation |
| 08:00 | Correlated findings | Documentation |

---

# Investigation Flow

Investigation Started

↓

Verified Audit Policy

↓

Generated Password Reset

↓

Windows Logged Event 4724

↓

Validated Event with PowerShell

↓

Verified Wazuh Agent

↓

Confirmed Raw Event in archives.json

↓

Compared alerts.json

↓

Correlated Evidence

↓

Investigation Completed

---

# Summary

This investigation successfully reconstructed the lifecycle of a Windows password reset event using native Windows Security auditing and Wazuh. The investigation emphasized the importance of validating each stage of the logging pipeline—from event generation to raw event ingestion—while demonstrating how archives.json and alerts.json serve different forensic purposes.
