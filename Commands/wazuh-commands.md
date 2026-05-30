# Wazuh Commands Reference

## Download Wazuh Installer

```bash
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
```

Purpose:
Downloads official installation script.

---

# Install Wazuh

```bash
sudo bash wazuh-install.sh -a
```

Purpose:
Installs:

* Wazuh Manager
* Wazuh Dashboard
* Wazuh Indexer

---

# Dashboard Access

```text
https://<WAZUH-IP>
```

Example:

```text
https://192.168.56.110
```

Purpose:
Access SIEM dashboard.

---

# Check Agent Status

```bash
sudo systemctl status wazuh-agent
```

Purpose:
Verify agent health.

---

# Enable Agent

```bash
sudo systemctl enable wazuh-agent
```

Purpose:
Enable auto-start.

---

# Start Agent

```bash
sudo systemctl start wazuh-agent
```

Purpose:
Start agent service.

---

# Restart Agent

```bash
sudo systemctl restart wazuh-agent
```

Purpose:
Apply configuration changes.

---

# Wazuh File Integrity Monitoring Configuration

File:

```text
/var/ossec/etc/ossec.conf
```

Configuration:

```xml
<directories realtime="yes">/etc,/home</directories>
```

Purpose:
Enable real-time file monitoring.

---

# Sysmon Integration Configuration

File:

```text
C:\Program Files (x86)\ossec-agent\ossec.conf
```

Configuration:

```xml
<localfile>
  <location>Microsoft-Windows-Sysmon/Operational</location>
  <log_format>eventchannel</log_format>
</localfile>
```

Purpose:
Forward Sysmon logs to Wazuh.

---

# Useful Dashboard Searches

Search for PowerShell:

```text
powershell.exe
```

Search for Nmap activity:

```text
nmap
```

Search High Severity Alerts:

```text
rule.level >= 5
```

Purpose:
Speed up investigations.
