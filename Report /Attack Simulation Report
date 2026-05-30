# Attack Simulation Report

## Project Name

cyart-red-teaming - Week 2

---

# Objective

After successfully deploying the SOC lab environment, the next objective was to simulate common attacker activities and validate whether the deployed security monitoring infrastructure could successfully detect, log, and alert on suspicious behavior.

The goal of this exercise was not exploitation, but rather understanding how attacker actions appear from a defender's perspective and how those activities are detected inside a Security Operations Center (SOC).

---

# Scope of Testing

The following attack simulations were performed:

1. Network Reconnaissance
2. PowerShell Execution
3. Authentication Failure Simulation
4. File Integrity Monitoring Validation
5. Persistence Technique Simulation
6. Security Event Investigation
7. MITRE ATT&CK Mapping

---

# Lab Environment

| Machine        | Role            |
| -------------- | --------------- |
| Kali Linux     | Attacker System |
| Windows 10     | Victim System   |
| Ubuntu + Wazuh | SIEM Server     |

---

# Attack Simulation Methodology

The attack simulation phase was divided into multiple stages to mimic a simplified cyber attack lifecycle.

The process followed:

```text
Reconnaissance
      ↓
Enumeration
      ↓
Execution
      ↓
Persistence
      ↓
Detection
      ↓
Investigation
```

This workflow closely resembles activities observed during real-world attacks.

---

# Phase 1 - Network Reconnaissance

## Purpose

Before attackers attempt exploitation, they usually gather information about the target environment.

Reconnaissance helps attackers identify:

* Open ports
* Running services
* Operating systems
* Potential attack vectors

---

## Tool Used

Nmap

---

## Command Executed

```bash
nmap -sS -A <TARGET-IP>
```

Example:

```bash
nmap -sS -A 192.168.56.105
```

---

## Command Explanation

### -sS

Performs a TCP SYN Scan.

Often referred to as a stealth scan.

---

### -A

Enables:

* OS Detection
* Version Detection
* Script Scanning
* Traceroute

---

# Expected Attacker Outcome

The attacker receives:

* Open ports
* Service versions
* Operating system details

This information can be used for future attacks.

---

# Defender Perspective

From a SOC perspective, reconnaissance activity is highly suspicious because attackers typically perform scanning before exploitation.

---

# Detection in Wazuh

The following indicators were monitored:

* Network scanning activity
* Suspicious connection attempts
* Unusual network behavior

---

# MITRE ATT&CK Mapping

| Technique ID | Technique Name           |
| ------------ | ------------------------ |
| T1046        | Network Service Scanning |

---

# Phase 2 - Authentication Failure Simulation

## Purpose

Brute-force attacks remain one of the most common attack techniques used by threat actors.

This simulation was performed to verify whether authentication failures were being logged and monitored correctly.

---

# Activity Performed

Multiple invalid login attempts were generated against the Windows system.

---

# Expected Security Events

Windows should generate:

* Failed Login Events
* Authentication Failure Logs
* Security Event IDs

---

# Detection in Wazuh

Wazuh monitored:

* Failed authentication attempts
* Login anomalies
* Repeated authentication failures

---

# MITRE ATT&CK Mapping

| Technique ID | Technique Name |
| ------------ | -------------- |
| T1110        | Brute Force    |

---

# Phase 3 - PowerShell Execution Monitoring

## Purpose

PowerShell is one of the most abused tools in modern cyber attacks.

Threat actors frequently use PowerShell for:

* Enumeration
* Script execution
* Payload delivery
* Lateral movement
* Persistence

---

# Commands Executed

```powershell
powershell -ep bypass
```

Followed by:

```powershell
whoami
ipconfig
net user
```

---

# Command Explanation

## whoami

Displays the current user account.

---

## ipconfig

Displays network configuration information.

---

## net user

Displays local user accounts.

---

# Why Attackers Use These Commands

These commands help attackers understand:

* Current privileges
* Network configuration
* Available user accounts

---

# Detection

Sysmon captured:

* Process creation
* Command line activity
* User context

Wazuh generated corresponding alerts.

---

# MITRE ATT&CK Mapping

| Technique ID | Technique Name |
| ------------ | -------------- |
| T1059.001    | PowerShell     |

---

# Phase 4 - File Integrity Monitoring Validation

## Purpose

Attackers frequently modify files during:

* Malware deployment
* Configuration changes
* Persistence setup
* Data staging

The objective was to verify that File Integrity Monitoring was functioning correctly.

---

# Test Activity

Created a new file:

```bash
touch ~/testfile
```

Modified the file:

```bash
echo "malwaretest" >> ~/testfile
```

---

# Detection

Wazuh File Integrity Monitoring detected:

* File creation
* File modification
* Real-time changes

---

# Security Value

File Integrity Monitoring helps identify:

* Unauthorized modifications
* Malware activity
* Persistence attempts
* Insider threats

---

# Phase 5 - Persistence Simulation

## Purpose

Attackers often attempt to maintain long-term access after initial compromise.

One common technique involves creating scheduled tasks.

---

# Command Executed

```powershell
schtasks /create /sc onlogon /tn "Updater" /tr "cmd.exe"
```

---

# Command Breakdown

## /create

Creates a new scheduled task.

---

## /sc onlogon

Triggers task during user logon.

---

## /tn

Task name.

---

## /tr

Command executed by the task.

---

# Security Significance

Persistence mechanisms allow attackers to regain access after reboot or user logout.

---

# Detection

Sysmon detected:

* Task creation
* Process execution
* Persistence-related activity

Wazuh correlated and displayed alerts.

---

# MITRE ATT&CK Mapping

| Technique ID | Technique Name |
| ------------ | -------------- |
| T1053.005    | Scheduled Task |

---

# Security Event Investigation

After alerts were generated, investigation was performed through the Wazuh dashboard.

Each alert was reviewed using:

* Timestamp
* Agent Name
* Source IP
* Process Name
* Command Line
* Alert Severity
* Rule Description
* MITRE ATT&CK Mapping

---

# Findings

The monitoring infrastructure successfully detected all simulated activities.

Observed detections included:

* Network reconnaissance
* PowerShell execution
* Authentication failures
* File modifications
* Persistence attempts

---

# Lessons Learned

During the attack simulation phase, several important defensive concepts were reinforced:

* Attacker actions generate detectable artifacts
* Endpoint monitoring improves visibility
* SIEM platforms help centralize investigations
* File Integrity Monitoring is valuable for detecting unauthorized changes
* MITRE ATT&CK provides a useful framework for classifying attacker behavior

---

# Challenges Faced

The following issues were encountered:

## Network Communication Issues

Initial communication failures occurred due to incorrect VirtualBox network configuration.

Resolution:

* Reconfigured Host-Only Adapter settings.

---

## Agent Connectivity Problems

The Wazuh agent initially failed to appear in the dashboard.

Resolution:

* Restarted the agent service.
* Verified manager IP configuration.

---

## Sysmon Log Collection

Sysmon logs were not visible initially.

Resolution:

* Updated ossec.conf configuration.
* Restarted Wazuh service.

---

# Outcome

The attack simulation exercise successfully demonstrated how attacker activities can be monitored and investigated using Wazuh and Sysmon.

The environment successfully detected:

* Reconnaissance
* Execution
* Authentication failures
* File modifications
* Persistence activities

The SOC infrastructure proved capable of collecting, correlating, and analyzing security events generated during simulated attack scenarios.

---

# Conclusion

This phase provided hands-on experience with both offensive and defensive aspects of cybersecurity. Simulated attacker activities generated meaningful security telemetry that was collected and analyzed using Wazuh and Sysmon.

The exercise improved understanding of attacker behavior, detection engineering, incident investigation, and SOC workflows while reinforcing the importance of centralized monitoring and endpoint visibility.

---
