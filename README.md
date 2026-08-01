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

### 3. Advanced Malware Emulation, Persistence, & Code Integrity Auditing
* **Objective:** Emulate an active malware string establishing long-term persistence in the registry and running high-velocity directory reconnaissance to mimic ransomware behavior before data encryption.
* **Execution Vector:** Deployed an administrative registry injection command followed by an aggressive, 40-cycle native PowerShell folder-scraping loop targeting the protected system configuration vault within a sub-second window:
  `New-Item -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" -Name "MalwareUpdaterSimulation" -Value "C:\Windows\Temp\malware_payload.exe" -Force1..40 | ForEach-Object { Get-ChildItem -Path "C:\Windows\System32\config\" -ErrorAction SilentlyContinue > $null }`
* **Defensive Alignment:** Manually updated the endpoint configuration engine (ossec.conf) with custom <syscheck> attributes to force immediate realtime="yes" registry tracking loops past standard 12-hour caching delays.


---

## 📊 Real-Time Visual Evidence & Telemetry Spikes

### Figure 1.1: Live Wazuh Threat Hunting Baseline Dashboard
![Wazuh Threat Hunting Dashboard Spike](https://raw.githubusercontent.com/LakshanRaghav/Enterprise-SIEM-Threat-Hunting-Lab/refs/heads/main/Architectural-Blueprints/Screenshot_31-7-2026_21447_192.168.1.14.jpeg)

* **SIEM Operations Metrics:** Successfully ingested, parsed, and logged over **968 total processed security events** from the live workstation node.
* **Adversarial Pattern Correlation:** Validated real-time analytical timeline spikes at the exact minute of attack execution, proving the SIEM's capability to map anomalies to MITRE ATT&CK codes **T1070 (Indicator Removal)** and **T1562 (Disable or Modify Tool)**.

### Figure 1.2: Expanded Security Incident Volumetric Analysis Dashboard
![Wazuh Threat Hunting Dashboard Spike](https://raw.githubusercontent.com/LakshanRaghav/Enterprise-SIEM-Threat-Hunting-Lab/refs/heads/main/Architectural-Blueprints/Screenshot_1-8-2026_17232_.jpeg)

* **Metric Column 1 (Total Volume):** Ingested, parsed, and logged over **968 total processed security events** across the live workstation node.
* **Metric Column 2 (Timeline Spike):** Visualized an acute, towering event volume spike at the 21:00 mark, indicating successful multi-event rate correlation.
* **Metric Column 3 (Adversarial Correlation):** Explicitly captured **4 active centralized authentication failures**, mapping anomalies to MITRE ATT&CK codes **T1070 (Indicator Removal)** and **T1562 (Disable or Modify Tool)**.

### Figure 1.3: Code Integrity & Cryptographic Audit Stream
![Wazuh Threat Hunting Dashboard Spike](https://raw.githubusercontent.com/LakshanRaghav/Enterprise-SIEM-Threat-Hunting-Lab/refs/heads/main/Architectural-Blueprints/Screenshot_31-7-2026_194452_192.168.1.12.jpeg)

* **Metric Column 1 (Total Hits):** Captured **58 specific log hits** registered across the high-frequency administrative process sweep.
* **Metric Column 2 (Timeline Spike):** Recorded a sharp vertical timeline volume spike peaking above 35 counts at approximately 14:30.
* **Metric Column 3 (Central Rule Triggered):** Documented consecutive chronological log entries for **Rule ID 18107 ("Windows Logon Success.")** mapping directly to administrative token validation.
Use code with caution.📂 Your Next Active Step to Increase Your GitHub Score:Edit Your README: Open your repository homepage on GitHub, hit the Pencil Icon to edit, and swap out the old sections for this updated, highly detailed markdown block.Commit Your Second Script: Open your Attack-Simulation-Scripts folder, click Add file -> Create new file, name it local_brute_force.bat, paste your for /L loop command inside it, and save.Commit Your Third Script: In that same folder, create another new file named malware_recon_persistence.ps1, paste your two PowerShell commands inside it, and click save.This will fully update your portfolio homepage, match your exact favorite format, and add three massive green activity squares to your contribution tracker! Let me know when these updates are live!

---

## 🧠 Engineering Observations & Lifecycle Troubleshooting

* **Dynamic Network Adaptation (DHCP Gateway Desynchronisation):**
  * **The Issue:** Shifting local network topologies and dynamic DHCP router lease renewals caused the host workstation and the SIEM server to lose connection routing states when IP targets cycled.
  * **The Resolution:** Manually isolated the local endpoint's core runtime libraries and parsed the configuration files (`win32ui`) to re-bind the host telemetry stream directly to the active server gateway (`192.168.1.14`), ensuring zero handshake downtime.

* **Agent System Recovery (XML Configuration Corruption File Reset):**
  * **The Issue:** Manual editing of the protected system files without full folder permissions introduced structural formatting errors, causing the local background service (`WazuhSvc`) to fault and fall into a persistent `Stopped` crash loop.
  * **The Resolution:** Executed a full structural factory-reset recovery deployment using an automated PowerShell script to purge the broken configuration array, replace it with a pristine XML configuration template, and force-start the engine back to a healthy `Running` state.

* **Log Channel Auditing (FIM Cache Delays & Un-muting Advanced Event Channels):**
  * **The Issue:** The SIEM suffered structural blindness during both the network credential testing and the registry malware injection phases. This was caused by Windows storing specialized authentication records in independent sub-folders (`OpenSSH/Operational`), and the agent's File Integrity Monitoring (`Syscheck`) engine running on a slow 12-hour schedule to save CPU cycles.
  * **The Resolution:** Utilized the native Windows audit utility (`wevtutil sl OpenSSH/Operational /e:true`) to un-mute the hidden login logging rooms. Simultaneously injected custom `<syscheck>` real-time variables (`realtime="yes"`) directly into the agent's configuration core to completely bypass caching delays and stream registry anomalies in sub-second intervals.

