# Troubleshooting Notes

## Issue 1 — Event ID 4724 Not Generated

### Cause

The password was changed for the current user instead of resetting another user's password.

### Resolution

Reset the password of a different local account.

---

## Issue 2 — Audit Policy Not Configured

### Cause

Password reset auditing was disabled.

### Resolution

Enable the required Windows audit policy using `auditpol`.

---

## Issue 3 — Event Not Visible in Event Viewer

### Cause

Incorrect Event ID or audit configuration.

### Resolution

Verify Windows Security logs and confirm Event ID 4724 generation before investigating Wazuh.

---

## Issue 4 — Event Missing in Wazuh Discover

### Cause

Incorrect search query or indexing delay.

### Resolution

Confirm ingestion using archives.json before troubleshooting Discover.

---

## Issue 5 — Event Missing in alerts.json

### Cause

The event was collected but did not trigger a matching Wazuh rule.

### Resolution

Understand that alerts.json stores rule-matched events, while archives.json stores raw collected events.

---

## Issue 6 — Agent Connectivity

### Cause

Possible communication interruption.

### Resolution

Verify agent status using:

```bash
sudo /var/ossec/bin/agent_control -i 001
```

---

# Lessons Learned

- Verify Windows event generation before investigating SIEM issues.
- archives.json is the authoritative source for raw event ingestion.
- alerts.json represents processed security alerts.
- Event generation, collection, and detection are separate stages in the Wazuh pipeline.
- Structured troubleshooting significantly reduces investigation time.
