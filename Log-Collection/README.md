# Log Collection

## Overview

This section explains how Windows logs were collected and sent to Splunk Enterprise.

I used **Splunk Universal Forwarder** to collect logs from the Windows 10 machine and forward them to Splunk for monitoring and analysis.

---

# Log Sources

The following logs were collected:

* Windows Security Logs
* Windows System Logs
* Windows Application Logs
* Sysmon Operational Logs

These logs were used to monitor system activity and investigate security events.

---

# Universal Forwarder Setup

The Splunk Universal Forwarder was installed on the Windows 10 machine.

It was configured to collect and forward the following logs:

* Security
* System
* Application
* Microsoft-Windows-Sysmon/Operational

After the configuration, the logs were successfully sent to Splunk Enterprise.

---

# Important Windows Event IDs

| Event ID | Description      |
| -------- | ---------------- |
| 4624     | Successful Login |
| 4625     | Failed Login     |
| 4688     | Process Creation |

---

# Log Collection Flow

```text
Windows 10
      │
      ▼
Windows Event Logs + Sysmon Logs
      │
      ▼
Splunk Universal Forwarder
      │
      ▼
Splunk Enterprise
      │
      ▼
Search & Analysis
```

---

# Result

Windows Event Logs and Sysmon logs were successfully collected in Splunk and used for:

* Log Analysis
* Threat Detection
* Threat Hunting
* Incident Investigation
* Security Dashboards
