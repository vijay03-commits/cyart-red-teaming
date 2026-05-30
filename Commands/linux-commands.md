# Linux Commands Reference

## System Update

### Command

```bash
sudo apt update && sudo apt upgrade -y
```

### Purpose

Updates package repositories and upgrades installed packages.

### Why Used

Before installing Wazuh and other security tools, the operating system should be updated to ensure stability and security.

---

# Network Connectivity Test

### Command

```bash
ping <TARGET-IP>
```

### Purpose

Verifies communication between virtual machines.

### Example

```bash
ping 192.168.56.105
```

### Expected Result

ICMP replies from target host.

---

# Nmap Reconnaissance Scan

### Command

```bash
nmap -sS -A <TARGET-IP>
```

### Purpose

Performs reconnaissance against a target system.

### Parameters

#### -sS

TCP SYN Scan.

#### -A

Enables:

* OS Detection
* Version Detection
* Script Scanning
* Traceroute

### Security Value

Used to simulate attacker reconnaissance activity.

---

# Download Wazuh Agent

### Command

```bash
wget https://packages.wazuh.com/4.x/apt/pool/main/w/wazuh-agent/wazuh-agent_4.7.5-1_amd64.deb
```

### Purpose

Downloads Wazuh agent package.

---

# Install Wazuh Agent

### Command

```bash
sudo WAZUH_MANAGER='<WAZUH-IP>' dpkg -i wazuh-agent_4.7.5-1_amd64.deb
```

### Purpose

Installs and registers Kali Linux with the Wazuh server.

---

# Start Wazuh Agent

### Command

```bash
sudo systemctl start wazuh-agent
```

### Purpose

Starts Wazuh service.

---

# Enable Wazuh Agent

### Command

```bash
sudo systemctl enable wazuh-agent
```

### Purpose

Starts agent automatically after reboot.

---

# Verify Agent Status

### Command

```bash
sudo systemctl status wazuh-agent
```

### Purpose

Confirms agent is running correctly.

Expected:

```text
active (running)
```

---

# File Creation Test

### Command

```bash
touch ~/testfile
```

### Purpose

Creates a new file.

### Security Value

Generates File Integrity Monitoring events.

---

# File Modification Test

### Command

```bash
echo "malwaretest" >> ~/testfile
```

### Purpose

Modifies an existing file.

### Security Value

Triggers Wazuh File Integrity Monitoring alerts.

---

# Restart Wazuh Agent

### Command

```bash
sudo systemctl restart wazuh-agent
```

### Purpose

Applies configuration changes.
