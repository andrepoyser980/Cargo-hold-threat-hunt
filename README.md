# Cargo Hold – Threat Hunt & Incident Response Case Study

**Azuki Import / Export**

A real-world, multi-stage intrusion involving credential reuse, lateral movement, data staging, credential dumping, exfiltration, persistence, and anti-forensics — detected via Microsoft Defender for Endpoint.

**Overview**

This repository documents a threat hunting investigation following a confirmed compromise of an enterprise workstation. Approximately **72 hours after the initial breach,** the attacker re-entered the environment, pivoted laterally to a file server, staged sensitive data, dumped credentials, and exfiltrated information to an external service.

The case demonstrates **hands-on-keyboard attacker behavior**, extensive Living-off-the-Land (LOLBin) abuse, and strong alignment with the **MITRE ATT&CK framework**.

**Executive Summary**

* Initial compromise occurred on November 19, 2025

* Attacker returned 72 hours later using valid credentials

* Lateral movement from azuki-sl → azuki-fileserver01

* PowerShell-based payloads staged and hidden

* Credential dumping via renamed tooling

* Sensitive data compressed and exfiltrated externally

* Persistence established via registry autorun key

* Anti-forensics observed (log deletion)

**Impact Level:High**
**Threat Type**: Interactive intrusion / Data exfiltration
**Detection Source**: Microsoft Defender for Endpoint
<img width="280" height="280" alt="image" src="https://github.com/user-attachments/assets/c0ab37ae-e2e2-411a-b6d5-9a20c4fa4c64" /> <img width="280" height="280" alt="image" src="https://github.com/user-attachments/assets/05f2846d-0f16-4cc0-9b8c-5f34b61ba0a2" /> <img width="380" height="220" alt="image" src="https://github.com/andrepoyser980/Cargo-hold-threat-hunt/blob/main/images/attack-flow3.jpg" />

Attack Sequence:

Valid credential reuse (RDP)

Lateral movement to file server

Network, share, and privilege discovery

Hidden staging directory creation

Credential dumping (LSASS)

Data aggregation and compression

External exfiltration

Persistence via registry

Log deletion (anti-forensics)

**Attacker & Compromised Assets**
**Compromised Accounts**

**kenji.sato** – Initial foothold

**fileadmin** – Lateral movement & data theft

**Compromised Systems**

**azuki-sl** (Workstation)

**azuki-fileserver01** (File Server)

**External Infrastructure**

* **Initial Access IP**: 159.26.106.98

* **Exfiltration Service**: file.io

**MITRE ATT&CK Mapping**
| **Tactic**   |	**Technique** |	**Description** |
|--------------|----------------|-----------------|
|Initial Access|	T1078       	| Valid Accounts
| Execution    |	T1059.001	    | PowerShell      |
| Lateral Movement|	T1021.001	  |RDP              |
Discovery|	T1087 / T1135	|Account & Share Discovery
Defense Evasion|	T1564.001	|Hidden Directories
Credential Access|	T1003.001	|LSASS Dump
Collection|	T1560	|Archive Data
Exfiltration|	T1567.002	|Web Services
Persistence|	T1547.001	|Registry Run Keys
Impact|	T1070.004	|Log Deletion

**Investigation Timeline (UTC)**

<img width="240" height="180" alt="image" src="https://github.com/andrepoyser980/Cargo-hold-threat-hunt/blob/main/images/7-Phases-of-Incident-Response.jpg" />   <img width="240" height="240" alt="image" src="https://github.com/andrepoyser980/Cargo-hold-threat-hunt/blob/main/images/Evolution-of-the-Security-figure1.png" />  <img width="220" height="220" alt="image" src="https://github.com/andrepoyser980/Cargo-hold-threat-hunt/blob/main/images/Rick-and-Morty-Timeline-1.png" />
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- 
|**Time** |	**Event** |
|---------|-----------|
| 00:40	  | User & privilege enumeration|
| 00:42	  | Network share discovery     |
| 00:55	  | Staging directory hidden    |
| 01:03 	| PowerShell payload execution
|01:07	  | Credential file creation
| 01:30	  | Data compression
|01:59	  | Data exfiltration
| 02:10	  | Registry persistence
| 02:26   |	PowerShell logs deleted
----------------------------------
**Key Findings (IOCs**)
**Files**

* ex.ps1

* svchost.ps1

* credentials.tar.gz

* IT-Admin-Passwords.csv

* pd.exe (renamed credential dumper)

  **Directories**

* C:\Windows\Logs\CBS (hidden staging path)

**Network**

* External upload to file.io

* Remote access from 159.26.106.98

**Impact Assessment**
**Actual Impact**

* Administrative credential compromise

* Unauthorized access to file server

* Sensitive data theft

* Persistence mechanisms deployed

* Log tampering reduced forensic visibility

**Risk Rating**

**High**

**Reasoning**:
Confirmed credential dumping + exfiltration + persistence + lateral movement.

**Recommendations**
**Immediate**

* Disable/reset affected accounts

* Isolate compromised hosts

* Remove registry persistence

* Block external file-sharing services

* Preserve forensic images

**Long-Term**

* Enforce MFA for all privileged access

* Restrict PowerShell with ASR rules

* Monitor for hidden directories & autoruns

* Alert on encoded PowerShell

* Detect outbound uploads via curl, certutil

**About This Case Study**

**This project is intended for**:

* Blue Team / SOC portfolios

* Threat hunting demonstrations

* DFIR interview discussions

* MITRE ATT&CK mapping practice

All sensitive identifiers are sanitized.

**Author**: Andre Poyser

**Role**: Security Analyst / Threat Hunter

**Tools**: Microsoft Defender for Endpoint, Log Analytics Workspace, KQL

