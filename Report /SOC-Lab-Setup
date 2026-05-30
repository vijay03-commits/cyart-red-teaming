# SOC Lab Setup Report

## Project Name

cyart-red-teaming - Week 2

---

# Purpose of the Lab

The purpose of this lab was to build a functional Security Operations Center (SOC) environment using open-source security tools. The lab was designed to simulate a real-world enterprise environment where security events can be collected, monitored, analyzed, and investigated.

This setup serves as the foundation for all later activities such as threat detection, attack simulation, incident response, vulnerability assessment, and threat hunting.

---

# Lab Objectives

The primary objectives of this setup were:

* Create an isolated cybersecurity lab environment
* Deploy a SIEM platform for centralized monitoring
* Configure endpoint monitoring
* Enable log collection from multiple systems
* Prepare systems for attack simulation
* Build an environment suitable for incident investigation
* Understand the architecture of a SOC environment

---

# Hardware Requirements

The lab was created using a personal computer with virtualization support enabled.

Recommended specifications:

| Component      | Recommended          |
| -------------- | -------------------- |
| RAM            | 16 GB or higher      |
| CPU            | 4 Cores or higher    |
| Storage        | 100 GB Free Space    |
| Virtualization | VT-x / AMD-V Enabled |

---

# Virtualization Platform

## VirtualBox

VirtualBox was selected as the virtualization platform because it is free, lightweight, and widely used for cybersecurity labs.

### Why VirtualBox

* Easy VM management
* Snapshot support
* Network customization
* Cross-platform support
* Suitable for isolated environments

---

# Virtual Machines Used

## Kali Linux

### Purpose

Used as the attacker machine.

### Responsibilities

* Network reconnaissance
* Vulnerability testing
* Attack simulation
* Security assessment

### Common Tools Available

* Nmap
* Metasploit
* Burp Suite
* Wireshark
* Hydra

---

## Windows 10

### Purpose

Used as the victim machine.

### Responsibilities

* Generate logs
* Receive attack simulations
* Provide endpoint telemetry

### Monitoring Installed

* Wazuh Agent
* Sysmon

---

## Ubuntu Server

### Purpose

Used as the SIEM server.

### Responsibilities

* Collect logs
* Generate alerts
* Monitor endpoints
* Correlate events

### Installed Components

* Wazuh Manager
* Wazuh Dashboard
* Wazuh Indexer

---

# Network Configuration

## Network Type

Host-Only Adapter

### Why Host-Only Adapter

Host-Only networking allows all virtual machines to communicate with each other while remaining isolated from external networks.

Benefits:

* Safe attack simulation
* Internal communication
* Reduced risk
* Controlled environment

---

# Network Verification

After configuring the network, connectivity was verified using ping.

Example:

```bash
ping <TARGET-IP>
```

Expected Result:

Successful ICMP replies from the target system.

---

# Wazuh Deployment

## What is Wazuh

Wazuh is an open-source Security Information and Event Management (SIEM) platform.

### Features

* Log collection
* Threat detection
* File Integrity Monitoring
* Vulnerability Detection
* Security Monitoring
* Incident Investigation

---

# Ubuntu Preparation

Before installing Wazuh, Ubuntu packages were updated.

Command:

```bash
sudo apt update && sudo apt upgrade -y
```

### Why

Ensures latest security updates are installed before deployment.

---

# Wazuh Installation

## Download Installation Script

```bash
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
```

### Purpose

Downloads the official installation script from Wazuh.

---

## Execute Installation

```bash
sudo bash wazuh-install.sh -a
```

### Purpose

Installs:

* Wazuh Manager
* Wazuh Dashboard
* Wazuh Indexer

The installation creates a complete SIEM environment.

---

# Dashboard Access

After installation, the dashboard was accessed through a web browser.

Format:

```text
https://<WAZUH-IP>
```

Example:

```text
https://192.168.56.110
```

---

# Wazuh Agent Installation (Kali Linux)

## Download Agent

```bash
wget https://packages.wazuh.com/4.x/apt/pool/main/w/wazuh-agent/wazuh-agent_4.7.5-1_amd64.deb
```

---

## Install Agent

```bash
sudo WAZUH_MANAGER='<WAZUH-IP>' dpkg -i wazuh-agent_4.7.5-1_amd64.deb
```

### Purpose

Connects Kali Linux to the Wazuh Manager.

---

## Enable Service

```bash
sudo systemctl daemon-reload
sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent
```

---

## Verify Service

```bash
sudo systemctl status wazuh-agent
```

Expected Result:

```text
active (running)
```

---

# Sysmon Deployment

## What is Sysmon

Sysmon is a Windows monitoring utility developed by Microsoft Sysinternals.

### Why Sysmon Was Installed

Default Windows logging is limited.

Sysmon provides:

* Process creation logs
* Network connection logs
* PowerShell activity
* Persistence detection
* Registry modifications

---

# Sysmon Installation

## Install Command

```powershell
Sysmon64.exe -accepteula -i sysmonconfig-export.xml
```

### Purpose

Installs Sysmon using a predefined monitoring configuration.

---

# Wazuh and Sysmon Integration

Modified file:

```text
C:\Program Files (x86)\ossec-agent\ossec.conf
```

Added:

```xml
<localfile>
  <location>Microsoft-Windows-Sysmon/Operational</location>
  <log_format>eventchannel</log_format>
</localfile>
```

### Purpose

Forward Sysmon events to Wazuh for centralized monitoring.

---

# File Integrity Monitoring (FIM)

## Purpose

Monitor file creation, modification, and deletion.

---

## Configuration

Modified:

```text
/var/ossec/etc/ossec.conf
```

Added:

```xml
<directories realtime="yes">/etc,/home</directories>
```

---

## Restart Agent

```bash
sudo systemctl restart wazuh-agent
```

---

# Validation Testing

Several tests were performed to verify functionality.

## Agent Status Check

```bash
sudo systemctl status wazuh-agent
```

---

## File Monitoring Test

```bash
touch ~/testfile
```

and

```bash
echo "test" >> ~/testfile
```

Expected Result:

Wazuh generates File Integrity Monitoring alerts.

---

# Challenges Encountered

During deployment several issues were encountered:

## Agent Connectivity

Issue:

* Agent not appearing in dashboard

Resolution:

* Verified IP address
* Restarted agent service

---

## Dashboard Access

Issue:

* SSL warning displayed

Resolution:

* Accepted self-signed certificate warning

---

## Network Communication

Issue:

* VM communication failure

Resolution:

* Reconfigured Host-Only Adapter

---

# Outcome

The SOC lab was successfully deployed and operational.

Achievements:

* Wazuh SIEM deployed successfully
* Kali agent connected successfully
* Windows monitoring enabled
* Sysmon integrated successfully
* File Integrity Monitoring configured
* Event collection operational
* Environment ready for attack simulation

---

# Conclusion

This phase established the foundation of the SOC lab environment. A centralized monitoring platform was deployed, endpoint visibility was enabled, and security telemetry collection was verified. The completed setup provides the infrastructure required for attack simulation, incident investigation, vulnerability assessment, and threat hunting activities in subsequent phases of the project.

---
