# Enterprise SIEM Infrastructure Deployment & Cyber Threat Hunting Laboratory

## 🏢 Project Overview
This project demonstrates the engineering, configuration, and structural validation of an enterprise-grade Security Information and Event Management (SIEM) pipeline. The core objective is to deploy a centralized log aggregation node capable of parsing real-time host endpoint telemetry, mapping live security events directly to the MITRE ATT&CK framework, and alerting on adversarial tactics. 

---

## 🛠️ Infrastructure & System Architecture
* **Central SIEM Management Server:** Deployed a pre-configured Wazuh Security Appliance running on an **Amazon Linux 2023** kernel environment.
* **Server Resource Allocation:** Engineered the core server container with a dedicated operational profile of 2 vCPU cores, 6GB of system RAM, and 30GB of isolated database storage.
* **Network Gateway Engineering:** Provisioned a virtual **Bridged Adapter** layout, allowing the isolated server instance to claim its own physical IP address from the local router pool (`192.168.1.14`).
* **Endpoint Telemetry Channel:** Configured a secure, encrypted daemon monitoring agent (**WazuhSvc**) onto a live Windows 11 host node to stream standard event directories back to the server brain.

---

## ⚔️ Adversarial Emulation Playbooks

### 1. Anti-Forensics Log Elimination (Indicator Removal)
* **Objective:** Emulate an active threat actor attempting to destroy tracking history and blind the defensive operations team.
* **Execution Vector:** Fired an administrative string to forcefully flush the target host's security event tracking block:  
  `wevtutil cl Security`
* **Defensive Interception:** The endpoint agent instantly captured the deletion signature, packeted the raw metadata, and streamed a critical **Level 10 Severity Alert** directly to the central dashboard.

### 2. High-Velocity Automated Credential-Guessing (Brute-Force)
* **Objective:** Emulate an automated password-cracking script to audit correlation alerts and rate-limiting rules.
* **Execution Vector:** Deployed a native loopback subsystem command script to blast the local authentication database with 30 rapid-fire logon attempts within a 1-second window:  
  `for /L %i in (1,1,30) do @net use \\127.0.0.1 /user:FakeHackerUser WrongPassword999 >nul 2>&1`
* **Defensive Alignment:** Manually provisioned and un-muted the Windows Advanced Event Logging topology (`wevtutil sl OpenSSH/Operational /e:true`) to guarantee absolute log ingestion visibility over active local network sockets.

---

## 📊 Real-Time Visual Evidence & Telemetry Spikes

![Wazuh Threat Hunting Dashboard Spike](https://githubusercontent.com)

* **SIEM Operations Metrics:** Successfully ingested, parsed, and logged over **968 total processed security events** from the live workstation node.
* **Adversarial Pattern Correlation:** Validated real-time analytical timeline spikes at the exact minute of attack execution, proving the SIEM's capability to map anomalies to MITRE ATT&CK codes **T1070 (Indicator Removal)** and **T1562 (Disable or Modify Tool)**.

---

## 🧠 Engineering Observations & Lifecycle Troubleshooting
* **Dynamic Network Adaptation:** Successfully resolved changing network environments and dynamic DHCP router shifts by manually re-mapping the endpoint's core file utility paths (`win32ui`) to ensure zero handshake downtime.
* **Agent System Recovery:** Resolved structural file collisions by executing a clean factory-reset configuration profile via administrative PowerShell, restoring a pristine data sync loop.
* **Log Channel Auditing:** Diagnosed an internal telemetry gap by identifying that specialized remote and local authentication protocols write to independent sub-directories, resolving system blindness by force-activating hidden logging rooms.
