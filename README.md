# Windows Sysmon & Splunk Home Lab

A home lab environment with Windows Sysmon configured, forwarding logs to Splunk Universal Forwarder. Includes custom Splunk dashboards and queries to detect failed logins, PowerShell usage, and privileged logons — designed for SOC analyst skill-building.

## Table of Contents
- [Overview](#overview)
- [Setup](#setup)
- [Sysmon Configuration](#sysmon-configuration)
- [Splunk Forwarding](#splunk-forwarding)
- [Detection Queries & Dashboards](#detection-queries--dashboards)
- [How to Simulate Events](#how-to-simulate-events)
- [Future Improvements](#future-improvements)
- [License](#license)

## Overview



## Setup
[https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon)


## Sysmon Configuration
I used the existing Community configuration from SwiftOnSecurity. I highly recommend as it is a very viable starting off point and allows you to learn more in depth about configuring Sysmon, which is an entirely separte thing on its own: Link is here for reference and modification:
[SwiftOnSecurity/sysmon-config](https://github.com/SwiftOnSecurity/sysmon-config) 

## Detection Queries & Dashboards

### Failed Login Attempts
```splunk
index=sysmon-logs EventCode=4625
| stats count by Account_Name, Source_Network_Address
| where count > 5
```

### Failed Login Attempts
```splunk
index=sysmon_logs EventCode=1 Image="*powershell.exe" NOT(User="Administrator")
| stats count by User, CommandLine
```

### Failed Login Attempts
```splunk
```
