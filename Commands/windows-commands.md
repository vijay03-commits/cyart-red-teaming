# Windows Commands Reference

## Launch PowerShell

### Command

```powershell
powershell
```

### Purpose

Opens PowerShell console.

---

# Bypass Execution Policy

### Command

```powershell
powershell -ep bypass
```

### Purpose

Starts PowerShell with execution policy bypass.

### Security Value

Frequently observed in attacker activity.

### Detection

Sysmon and Wazuh can detect this behavior.

---

# Display Current User

### Command

```powershell
whoami
```

### Purpose

Displays currently logged-in user.

### Security Value

Common attacker enumeration command.

---

# Display Network Configuration

### Command

```powershell
ipconfig
```

### Purpose

Shows network adapter information.

### Security Value

Used by attackers during internal reconnaissance.

---

# List Local Users

### Command

```powershell
net user
```

### Purpose

Displays local user accounts.

### Security Value

Used for account discovery.

---

# Create Scheduled Task

### Command

```powershell
schtasks /create /sc onlogon /tn "Updater" /tr "cmd.exe"
```

### Purpose

Creates a scheduled task.

### Security Value

Simulates attacker persistence.

### MITRE Mapping

T1053.005 - Scheduled Task

---

# Block Attacker IP

### Command

```powershell
netsh advfirewall firewall add rule name="Block Kali" dir=in action=block remoteip=<KALI-IP>
```

### Purpose

Blocks attacker machine.

### Security Value

Simulates containment activity during incident response.

---

# Stop Wazuh Service

### Command

```powershell
NET STOP WazuhSvc
```

### Purpose

Stops Wazuh agent.

---

# Start Wazuh Service

### Command

```powershell
NET START WazuhSvc
```

### Purpose

Starts Wazuh agent.

---

# Verify Sysmon Service

### Command

```powershell
Get-Service Sysmon64
```

### Expected Result

```text
Running
```

### Purpose

Verifies Sysmon installation.
