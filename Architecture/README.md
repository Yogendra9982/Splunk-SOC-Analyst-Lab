# 1. SOC Lab Setup

## What is SOC Lab Setup?

SOC Lab Setup means creating your own practice environment where you can learn security monitoring and incident investigation.

In this project, I created a small SOC lab for learning and practicing SOC Analyst skills.

## What was included in the lab?

* Kali Linux (Attacker/Admin Machine)
* Windows 10 (Victim Machine)
* Splunk Enterprise (SIEM)

## What is the role of each machine?

### Windows 10

Windows 10 is the target machine.

On this machine:

* Users log in.
* Commands are executed.
* Applications are opened.
* Attack simulations are performed.
* Security logs are generated.

### Splunk Enterprise

Splunk is the SIEM tool used in this lab.

It is responsible for:

* Collecting Windows logs.
* Storing logs.
* Searching and analyzing logs.
* Creating dashboards.
* Helping with threat detection and incident investigation.

### Kali Linux

Kali Linux is used for:

* Installing and managing Splunk.
* Testing and attack simulation.
* Managing the lab environment.

---

# 2. Splunk Installation

## What is Splunk?

Splunk is a **SIEM (Security Information and Event Management)** tool.

SOC Analysts use Splunk to collect, monitor, search, and analyze security logs.

## Installation Steps

### Step 1

Download Splunk Enterprise.

### Step 2

Install Splunk on Linux.

Example:

```bash
sudo dpkg -i splunk.deb
```

### Step 3

Start the Splunk service.

```bash
sudo /opt/splunk/bin/splunk start
```

### Step 4

Accept the Splunk license agreement.

### Step 5

Create an administrator account.

Example:

```text
Username: admin
Password: ********
```

### Step 6

Open the Splunk web interface in your browser.

```text
http://localhost:8000
```

## Result

Splunk is now installed and ready to collect and analyze logs.

---

# 3. Universal Forwarder Setup

## What is Universal Forwarder?

Splunk Universal Forwarder is a lightweight agent that is installed on the Windows machine.

Its job is to collect logs from Windows and send them to the Splunk server.

Without the Universal Forwarder, Splunk cannot automatically receive logs from the Windows machine.

## Why was Universal Forwarder installed?

The Universal Forwarder was installed to send Windows Event Logs and Sysmon logs from Windows 10 to Splunk Enterprise.

This allows Splunk to receive logs in real time for monitoring and investigation.

## Installation Steps

### Step 1

Download the Splunk Universal Forwarder for Windows.

### Step 2

Install the Universal Forwarder on the Windows machine.

### Step 3

Configure the connection with the Splunk server.

Example:

```text
Splunk Server IP : <Splunk_Server_IP>
Management Port  : 8089
Receiving Port   : 9997
```

### Step 4

Configure the inputs to collect the following logs:

* Security
* System
* Application
* Microsoft-Windows-Sysmon/Operational

### Step 5

Restart the Splunk Universal Forwarder service.

### Step 6

Verify that the Windows logs are successfully received in Splunk.

## Result

The Universal Forwarder successfully sent Windows Event Logs and Sysmon logs to Splunk Enterprise.

---

# 4. Windows Log Collection

## What is Windows Log Collection?

Windows records every important system activity in Windows Event Logs.

These logs help SOC Analysts understand what is happening on the system.

Examples of Windows activities:

* User Login
* User Logout
* Program Execution
* Process Creation
* System Errors
* Security Events

These logs are collected by the Universal Forwarder and sent to Splunk for monitoring and investigation.

## What was done?

The Windows machine was configured to generate security logs.

The Universal Forwarder was configured to collect and forward these logs to Splunk.

The following important events were collected:

* Event ID 4624 – Successful Login
* Event ID 4625 – Failed Login
* Event ID 4688 – Process Creation

## Result

Windows Event Logs were successfully forwarded and became searchable in Splunk.

---

# 5. Sysmon Integration

## What is Sysmon?

Sysmon (System Monitor) is a Microsoft tool that collects detailed system activity.

It provides much more information than the default Windows Event Logs.

For this reason, Sysmon is widely used by SOC Analysts and DFIR professionals.

## Why was Sysmon installed?

Normal Windows logs provide limited information.

For example:

### Normal Windows Log

```text
PowerShell started.
```

### Sysmon Log

```text
Process:
powershell.exe

Parent Process:
explorer.exe

Command:
powershell -enc ...

User:
John

SHA256:
xxxxxxxx

Process ID:
3456
```

Sysmon provides detailed information that makes investigations much easier.

## Installation

The following steps were performed:

* Download Sysmon.
* Download a Sysmon configuration file.
* Install Sysmon using the configuration.

Command:

```cmd
Sysmon64.exe -accepteula -i sysmonconfig.xml
```

## After Installation

A new log source is created in Windows Event Viewer.

```text
Applications and Services Logs
        ↓
Microsoft
        ↓
Windows
        ↓
Sysmon
        ↓
Operational
```

The Universal Forwarder collects these Sysmon logs and sends them to Splunk for detection and investigation.

---

# Final Architecture Flow

```text
Windows User Activity
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
Indexing & Log Storage
        │
        ▼
SPL Queries
        │
        ▼
Detection Rules
        │
        ▼
Threat Hunting
        │
        ▼
Incident Investigation
        │
        ▼
Security Dashboard
```
