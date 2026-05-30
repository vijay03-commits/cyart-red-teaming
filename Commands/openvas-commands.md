# OpenVAS Commands and Workflow

## Access OpenVAS

URL:

```text
https://<OPENVAS-IP>:9392
```

Example:

```text
https://192.168.56.120:9392
```

Purpose:
Access vulnerability management dashboard.

---

# Create Target

Navigation:

```text
Configuration
    ↓
Targets
    ↓
New Target
```

Purpose:
Define host to scan.

---

# Configure Scan

Navigation:

```text
Scans
   ↓
Tasks
   ↓
New Task
```

Configuration:

| Setting   | Value         |
| --------- | ------------- |
| Scan Type | Full and Fast |
| Target    | Windows-Test  |
| Scanner   | Default       |

---

# Launch Scan

Navigation:

```text
Scans
   ↓
Tasks
   ↓
Start
```

Purpose:
Begin vulnerability assessment.

---

# Review Findings

Focus on:

* Critical
* High
* Medium

Information to collect:

* Vulnerability Name
* Severity
* CVSS Score
* Description
* Recommendation

---

# Example Findings

| Vulnerability          | CVSS |
| ---------------------- | ---- |
| SMB Signing Disabled   | 5.3  |
| Weak TLS Configuration | 6.5  |
| Outdated Services      | 8.1  |

---

# Vulnerability Prioritization

| Severity | Priority  |
| -------- | --------- |
| Critical | Immediate |
| High     | High      |
| Medium   | Moderate  |
| Low      | Normal    |

---

# Vulnerability Management Lifecycle

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

Purpose:
Standard vulnerability management workflow.

---

# Security Value

OpenVAS helps identify:

* Weak configurations
* Missing patches
* Outdated software
* Attack surface exposure

This information supports remediation planning and improves overall security posture.
