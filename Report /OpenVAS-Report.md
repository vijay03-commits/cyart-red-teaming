# OpenVAS Vulnerability Assessment Report

## Project Name

cyart-red-teaming - Week 2

---

# Objective

The objective of this assessment was to identify security weaknesses within the target system using OpenVAS Vulnerability Management. The scan was performed against a Windows 10 virtual machine deployed inside the SOC lab environment.

The purpose of vulnerability assessment is to proactively identify weaknesses before they can be exploited by attackers. Vulnerability management is one of the most important defensive security activities because it helps organizations reduce their attack surface and prioritize remediation efforts.

This assessment was conducted after the deployment of the SOC infrastructure and attack simulation environment.

---

# Scope of Assessment

The assessment focused on the following areas:

* Open ports and exposed services
* Software vulnerabilities
* Weak configurations
* Security misconfigurations
* Insecure protocols
* Missing security controls

The target of the assessment was the Windows 10 machine operating within the lab environment.

---

# Lab Environment

| System         | Purpose                 |
| -------------- | ----------------------- |
| Kali Linux     | Security Testing System |
| OpenVAS Server | Vulnerability Scanner   |
| Windows 10     | Assessment Target       |
| Wazuh SIEM     | Monitoring Platform     |

---

# What is OpenVAS

OpenVAS (Open Vulnerability Assessment System) is an open-source vulnerability scanner used by security professionals to identify known security weaknesses in systems, applications, and network services.

OpenVAS performs thousands of security checks against a target and compares discovered services against known vulnerabilities and misconfigurations.

---

# Why Vulnerability Assessment is Important

Organizations perform vulnerability assessments to:

* Identify security weaknesses
* Reduce attack surface
* Improve security posture
* Prioritize remediation efforts
* Meet compliance requirements
* Prevent exploitation by attackers

A vulnerability that remains unpatched can eventually become an entry point for an attacker.

---

# OpenVAS Installation Overview

The OpenVAS scanner was deployed on a dedicated Linux virtual machine.

The deployment process included:

* Installing OpenVAS packages
* Configuring vulnerability feeds
* Updating vulnerability databases
* Creating administrator accounts
* Accessing the Greenbone Security Assistant (GSA) dashboard

---

# Accessing OpenVAS

The web interface was accessed using:

```text
https://<OPENVAS-IP>:9392
```

Example:

```text
https://192.168.56.120:9392
```

---

# Vulnerability Assessment Methodology

The assessment followed a structured methodology:

```text
Target Identification
          ↓
Target Configuration
          ↓
Scan Configuration
          ↓
Vulnerability Discovery
          ↓
Risk Analysis
          ↓
Remediation Planning
```

This process reflects standard vulnerability management practices used in enterprise environments.

---

# Creating the Target

Before initiating the scan, a target profile was created.

Configuration:

| Setting   | Value                     |
| --------- | ------------------------- |
| Name      | Windows-Test              |
| Host      | Windows Target IP         |
| Port List | All TCP and Default Ports |

Purpose:

Allows OpenVAS to identify which host should be scanned.

---

# Scan Configuration

A new scan task was created using the following profile:

| Configuration | Value                   |
| ------------- | ----------------------- |
| Scan Type     | Full and Fast           |
| Scanner       | OpenVAS Default Scanner |
| Target        | Windows-Test            |
| Scheduling    | Manual                  |

---

# Why "Full and Fast" Was Used

The Full and Fast profile provides:

* Service discovery
* Port scanning
* Vulnerability detection
* Configuration assessment
* Security testing

while maintaining reasonable scan duration.

---

# Scan Execution

The scan was launched from the OpenVAS dashboard.

During execution OpenVAS performed:

* Host discovery
* Port enumeration
* Service identification
* Vulnerability checks
* Configuration analysis
* Security testing

The scan duration depended on:

* Target system specifications
* Number of exposed services
* Available resources
* Network latency

---

# Vulnerability Findings

The scan identified several security weaknesses within the target environment.

---

# Finding 1: SMB Signing Disabled

## Severity

Medium

## CVSS Score

5.3

## Description

Server Message Block (SMB) signing was not enforced.

SMB signing helps protect network communications from tampering and man-in-the-middle attacks.

Without SMB signing, attackers may be able to intercept or modify SMB traffic.

---

## Risk

Potential man-in-the-middle attacks.

---

## Recommendation

Enable SMB signing through Group Policy or Local Security Policy.

---

# Finding 2: Weak TLS Configuration

## Severity

Medium

## CVSS Score

6.5

## Description

The system was configured to support outdated TLS versions or weak cryptographic settings.

Weak encryption protocols increase the risk of secure communications being compromised.

---

## Risk

Reduced confidentiality of network communications.

---

## Recommendation

Disable legacy TLS protocols and enable modern TLS configurations.

---

# Finding 3: Outdated Service Version

## Severity

High

## CVSS Score

8.1

## Description

A service running on the target system was identified as outdated.

Older software versions often contain publicly disclosed vulnerabilities that can be exploited by attackers.

---

## Risk

Potential remote code execution or privilege escalation.

---

## Recommendation

Update affected software to the latest supported version.

---

# Finding 4: Unnecessary Open Ports

## Severity

Low

## CVSS Score

3.7

## Description

Several ports were exposed that were not required for normal operation.

Every exposed service increases the attack surface of a system.

---

## Risk

Additional attack vectors become available to threat actors.

---

## Recommendation

Disable unused services and close unnecessary ports.

---

# Risk Prioritization

The findings were prioritized according to severity.

| Severity | Action Priority |
| -------- | --------------- |
| High     | Immediate       |
| Medium   | High            |
| Low      | Normal          |

Organizations should always address high-severity vulnerabilities first.

---

# Vulnerability Management Workflow

The assessment reinforced the standard vulnerability management lifecycle:

```text
Discover
    ↓
Assess
    ↓
Prioritize
    ↓
Remediate
    ↓
Verify
```

This cycle should be repeated continuously to maintain security.

---

# Correlation with Attack Simulation

Several findings identified during vulnerability assessment could potentially assist an attacker during the attack simulation phase.

Examples include:

* Weak configurations
* Exposed services
* Outdated software versions

An attacker performing reconnaissance could use these weaknesses as potential entry points.

This demonstrates the relationship between vulnerability management and threat detection.

---

# Challenges Encountered

Several challenges were observed during the assessment.

## Network Connectivity Issues

Initially the scanner could not communicate with the target.

Resolution:

* Verified IP configuration.
* Confirmed Host-Only network connectivity.

---

## Scan Duration

The Full and Fast profile required significant processing time.

Resolution:

* Allowed scan to complete without interruption.

---

## Resource Utilization

The scanner consumed considerable CPU and RAM resources.

Resolution:

* Allocated additional resources to the OpenVAS virtual machine.

---

# Lessons Learned

This assessment provided practical understanding of:

* Vulnerability scanning
* Risk assessment
* Security posture evaluation
* Attack surface analysis
* Remediation planning
* Vulnerability management workflows

The exercise demonstrated how vulnerability assessment complements SIEM monitoring and threat detection.

---

# Outcome

The assessment successfully identified multiple security weaknesses and provided actionable remediation recommendations.

The OpenVAS deployment proved effective in:

* Discovering exposed services
* Identifying misconfigurations
* Detecting outdated software
* Prioritizing security risks

This information can be used to improve the overall security posture of the environment.

---

# Conclusion

The OpenVAS vulnerability assessment successfully demonstrated the process of identifying, analyzing, and prioritizing security weaknesses within a target environment.

The findings highlighted the importance of regular vulnerability assessments, patch management, secure configuration practices, and continuous security monitoring.

By combining OpenVAS with Wazuh SIEM and endpoint monitoring, a more comprehensive defensive security strategy can be achieved.

---
