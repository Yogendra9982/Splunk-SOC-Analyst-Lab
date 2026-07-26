# Detection Rules

## Overview

This section contains the detection rules used in this project.

Detection rules help identify suspicious activities from the logs collected in Splunk. These rules are based on common attacker techniques and Windows events.

---

# Purpose

The main purpose of these detection rules is to:

* Detect suspicious processes
* Monitor Windows activities
* Identify possible attacks
* Generate security alerts
* Support incident investigation

---

# Detection Categories

The detection rules in this project include:

* PowerShell Detection
* Encoded PowerShell Detection
* Command Prompt (CMD) Detection
* Certutil Detection
* MSHTA Detection
* Rundll32 Detection
* Regsvr32 Detection
* LOLBins Detection
* Suspicious Parent Process Detection

---

# How It Works

Each detection rule searches for specific Windows events or process activity using SPL queries.

When a suspicious activity matches the rule, it can be investigated further to determine whether it is normal or malicious.

---

# Result

These detection rules helped me:

* Detect suspicious activities
* Monitor Windows security events
* Investigate potential threats
* Improve my understanding of Splunk detections
* Practice SOC Analyst skills
