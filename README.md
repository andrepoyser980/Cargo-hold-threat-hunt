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
