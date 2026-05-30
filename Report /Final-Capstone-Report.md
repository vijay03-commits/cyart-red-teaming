# Final Capstone Project Report

## Project Name

cyart-red-teaming - Week 2

---

# Executive Summary

This capstone project was conducted to build and operate a complete Security Operations Center (SOC) lab environment using open-source security tools. The project combined multiple defensive security concepts including SIEM deployment, endpoint monitoring, attack simulation, vulnerability assessment, incident investigation, threat detection, and basic containment activities.

The objective was to simulate real-world attacker behavior, observe the resulting security events, analyze generated alerts, and understand how a SOC analyst investigates suspicious activities using centralized monitoring platforms.

The lab was developed entirely within a virtualized environment and consisted of an attacker machine, a victim machine, and centralized monitoring infrastructure.

The project demonstrates practical knowledge of security monitoring, endpoint visibility, threat detection, vulnerability management, and incident response workflows.

---

# Project Objectives

The primary objectives of the capstone project were:

* Build a functional SOC environment
* Deploy centralized log monitoring
* Configure endpoint monitoring
* Simulate attacker activities
* Detect suspicious behavior
* Investigate generated alerts
* Perform vulnerability assessments
* Map attacker behavior using MITRE ATT&CK
* Practice containment procedures
* Develop security documentation

---

# Project Scope

The project covered the following areas:

### Security Monitoring

* Wazuh SIEM deployment
* Log aggregation
* Alert monitoring

### Endpoint Visibility

* Sysmon deployment
* Process monitoring
* PowerShell monitoring

### Threat Detection

* Reconnaissance detection
* Authentication monitoring
* File Integrity Monitoring

### Vulnerability Assessment

* OpenVAS deployment
* Vulnerability scanning
* Risk analysis

### Incident Response

* Alert investigation
* Event correlation
* Containment simulation

---

# Lab Architecture

## Infrastructure Components

| System        | Role                            |
| ------------- | ------------------------------- |
| Kali Linux    | Attacker Machine                |
| Windows 10    | Victim Machine                  |
| Ubuntu Server | Wazuh SIEM Server               |
| OpenVAS       | Vulnerability Assessment Server |

---

# Environment Setup

The entire environment was deployed using VirtualBox.

A Host-Only network was configured to ensure all virtual machines could communicate while remaining isolated from external networks.

The architecture was intentionally designed to replicate a simplified enterprise security environment.

---

# Phase 1 - SOC Infrastructure Deployment

## Wazuh SIEM

Wazuh was selected as the central monitoring platform because it provides:

* Log management
* Threat detection
* File integrity monitoring
* Security event analysis
* Agent management

---

## Installation Process

### Update Ubuntu

```bash
sudo apt update && sudo apt upgrade -y
```

### Download Installer

```bash
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
```

### Install Wazuh

```bash
sudo bash wazuh-install.sh -a
```

The installation deployed:

* Wazuh Manager
* Wazuh Dashboard
* Wazuh Indexer

---

# Phase 2 - Endpoint Monitoring

## Sysmon Deployment

To improve endpoint visibility, Sysmon was installed on the Windows machine.

Sysmon provides enhanced logging capabilities including:

* Process creation
* Command execution
* PowerShell activity
* Persistence monitoring
* Network connections

---

## Sysmon Installation

```powershell
Sysmon64.exe -accepteula -i sysmonconfig-export.xml
```

---

## Wazuh Integration

The following configuration was added:

```xml
<localfile>
  <location>Microsoft-Windows-Sysmon/Operational</location>
  <log_format>eventchannel</log_format>
</localfile>
```

This allowed Sysmon events to be forwarded directly into Wazuh.

---

# Phase 3 - Attack Simulation

After monitoring infrastructure was validated, attack simulations were performed.

The purpose was to generate realistic security events and evaluate detection capabilities.

---

# Attack Scenario 1 - Network Reconnaissance

## Objective

Identify open services and gather information about the target.

---

## Tool Used

Nmap

---

## Command

```bash
nmap -sS -A <TARGET-IP>
```

---

## Expected Outcome

Discovery of:

* Open ports
* Running services
* Operating system details

---

## Detection

Wazuh generated alerts associated with reconnaissance behavior.

---

## MITRE ATT&CK Mapping

| Technique ID | Technique                |
| ------------ | ------------------------ |
| T1046        | Network Service Scanning |

---

# Attack Scenario 2 - Authentication Failure Simulation

## Objective

Generate failed login events to verify monitoring effectiveness.

---

## Activity

Multiple invalid authentication attempts were performed against the Windows system.

---

## Detection

Wazuh successfully detected:

* Authentication failures
* Repeated login attempts
* Potential brute-force indicators

---

## MITRE ATT&CK Mapping

| Technique ID | Technique   |
| ------------ | ----------- |
| T1110        | Brute Force |

---

# Attack Scenario 3 - PowerShell Execution

## Objective

Simulate command execution frequently observed during attacks.

---

## Commands Executed

```powershell
powershell -ep bypass

whoami

ipconfig

net user
```

---

## Purpose

These commands allow attackers to:

* Identify users
* Enumerate systems
* Understand network configuration

---

## Detection

Sysmon and Wazuh logged:

* Process creation
* PowerShell execution
* Command-line arguments

---

## MITRE ATT&CK Mapping

| Technique ID | Technique  |
| ------------ | ---------- |
| T1059.001    | PowerShell |

---

# Attack Scenario 4 - File Modification Activity

## Objective

Validate File Integrity Monitoring.

---

## Commands

```bash
touch ~/testfile
```

```bash
echo "malwaretest" >> ~/testfile
```

---

## Detection

Wazuh generated alerts for:

* File creation
* File modification
* Real-time file monitoring events

---

# Attack Scenario 5 - Persistence Simulation

## Objective

Simulate attacker persistence.

---

## Command

```powershell
schtasks /create /sc onlogon /tn "Updater" /tr "cmd.exe"
```

---

## Purpose

Scheduled tasks are commonly used by attackers to maintain access after system reboot.

---

## Detection

Sysmon and Wazuh successfully logged:

* Task creation
* Process execution
* Persistence activity

---

## MITRE ATT&CK Mapping

| Technique ID | Technique      |
| ------------ | -------------- |
| T1053.005    | Scheduled Task |

---

# Phase 4 - Vulnerability Assessment

## OpenVAS Deployment

OpenVAS was used to assess the security posture of the Windows target.

---

## Assessment Goals

* Identify vulnerabilities
* Discover weak configurations
* Detect outdated software
* Evaluate attack surface

---

## Scan Profile

Full and Fast

---

## Findings

### SMB Signing Disabled

Severity: Medium

CVSS: 5.3

Recommendation:
Enable SMB Signing.

---

### Weak TLS Configuration

Severity: Medium

CVSS: 6.5

Recommendation:
Disable outdated TLS protocols.

---

### Outdated Services

Severity: High

CVSS: 8.1

Recommendation:
Update software to latest versions.

---

### Unnecessary Open Ports

Severity: Low

CVSS: 3.7

Recommendation:
Disable unused services.

---

# Phase 5 - Incident Investigation

Each alert generated during testing was investigated using the Wazuh Dashboard.

The following fields were analyzed:

* Timestamp
* Agent Name
* Source IP
* Process Name
* Command Line
* Alert Severity
* Event Description
* MITRE ATT&CK Mapping

---

# Investigation Methodology

```text
Alert Generated
       ↓
Alert Review
       ↓
Event Analysis
       ↓
Event Correlation
       ↓
Threat Classification
       ↓
Response Action
```

---

# Phase 6 - Containment Simulation

A containment exercise was performed by blocking the attacker IP address using Windows Firewall.

Command:

```powershell
netsh advfirewall firewall add rule name="Block Kali" dir=in action=block remoteip=<KALI-IP>
```

Purpose:

Prevent communication from the attacking system and simulate incident response containment procedures.

---

# Security Benefits Observed

The project demonstrated the value of:

* Centralized logging
* Endpoint visibility
* Event correlation
* Threat detection
* Vulnerability management
* Incident response workflows

---

# Challenges Encountered

Several issues were encountered during deployment and testing.

### Network Configuration Issues

Virtual machines initially failed to communicate.

Resolution:
Host-Only networking was reconfigured.

---

### Agent Connectivity Problems

The Kali agent did not initially appear in the dashboard.

Resolution:
Verified manager IP and restarted services.

---

### Sysmon Event Collection

Logs were not immediately visible.

Resolution:
Updated ossec.conf and restarted services.

---

### OpenVAS Performance

Vulnerability scans required significant processing time.

Resolution:
Allowed scans to complete without interruption.

---

# Skills Developed

This project provided practical experience in:

* SOC Operations
* SIEM Deployment
* Wazuh Administration
* Sysmon Monitoring
* Threat Detection
* Event Correlation
* Vulnerability Assessment
* MITRE ATT&CK Mapping
* Incident Investigation
* Security Documentation

---

# Lessons Learned

The project reinforced several important cybersecurity concepts:

* Most attacker activity generates observable artifacts.
* Endpoint monitoring dramatically improves visibility.
* SIEM solutions simplify investigations through centralized logging.
* Vulnerability management is critical for reducing attack surface.
* MITRE ATT&CK provides a structured way to classify attacker behavior.
* Security monitoring and vulnerability management complement each other.

---

# Project Outcome

The capstone project successfully achieved all planned objectives.

The environment demonstrated the ability to:

* Collect logs
* Detect suspicious activity
* Monitor endpoints
* Perform vulnerability assessments
* Investigate security events
* Simulate incident response actions

The completed lab provides a practical demonstration of modern SOC operations and defensive security practices.

---

# Conclusion

This capstone project successfully combined security monitoring, endpoint visibility, attack simulation, vulnerability assessment, and incident investigation into a single integrated environment.

The deployment of Wazuh, Sysmon, and OpenVAS provided valuable hands-on experience with technologies commonly used in enterprise security operations. Through attack simulation and alert analysis, the project demonstrated how defensive teams detect and respond to suspicious activities while maintaining visibility across monitored systems.

The project serves as a practical example of a complete SOC workflow and highlights the importance of continuous monitoring, vulnerability management, and proactive security operations.

---
