# Splunk Universal Forwarder Installation on DC01  
Active Directory + SIEM Integration | Security+ Aligned

This document details the installation and configuration of the Splunk Universal Forwarder (UF) on the domain controller **DC01**, enabling centralized log collection for SIEM operations. All steps were performed manually to ensure transparency, reproducibility, and alignment with Security+ monitoring objectives.

---

## 1. Overview

The Splunk Universal Forwarder is a lightweight agent installed on Windows endpoints to securely forward logs to a Splunk Indexer.

**Lab Components:**
- **DC01** – Windows Server Domain Controller  
- **Splunk Enterprise** – Ubuntu Server (`192.168.56.101`)  
- **Universal Forwarder** – Installed on DC01 to forward logs  

This setup enables real‑time monitoring, detection engineering, and incident response workflows.

---

## 2. Prerequisites

### Splunk Enterprise (Ubuntu)
- Host‑only IP: `192.168.56.101`
- Receiving port enabled: `9997`
- Verified via:
  ```bash
  sudo netstat -tulpn | grep 9997
 
### DC01 (Windows Server)
- Host‑only IP: 192.168.56.102 (or your assigned value)
- IE ESC disabled (optional)
- UF installer downloaded via direct link:

```Code
https://download.splunk.com/products/universalforwarder/releases/9.2.1/windows/splunkforwarder-9.2.1-78803f08aabb-x64-release.msi

```
---

## 3. Installation Steps

**3.1 Launch Installer**
Right‑click the MSI → **Run as Administrator**

**3.2 License Agreement**
Accept the license terms.

**3.3 Setup Type**
Select:
 ```Code
 Customized Options
 ```

**3.4 SSL Certificate Screen**
- Leave all fields **unchanged**
- Click **Next**
- No custom SSL certificate used

**3.5 Service Account**
Select:
 ```Code
 Local System
 ```
**Reason:**
Local System has required permissions for Security logs, AD logs, Sysmon (later), and Poweshell logs.

**3.6 Event Log, Performance, and AD Monitoring**
Check **every box** under:
- Windows Event Logs
- Performance Monitor
- Active Directory Monitoring

This ensures full visibility into authentication, Kerberos, GPO, AD replication, and system health.

**3.7 Splunk Forwarder Admin Account**
Create a local UF admin account:
 ```Code
 Username: splunkuf
 Password: <secure password>
 ```

This account is **local to the forwarder** and not used for Splunk Web login.

**3.8 Deployment Server**

Leave **blank**
(No deployment server used.)

**3.9 Receiving Indexer**
Enter:
 ```Code
 192.168.56.101:9997
 ```

This is the Splunk Indexer's receiving port.

**3.10 Complete Installation**
Click **Install** and allow the service to start.

---

## 4. Post-Installation Verification

**4.1 Verify Forwarder Service**
On DC01 Powershell:
 ```Powershell
 Get-Service splunkforwarder
 ```

Expected:
 ```Code
 Status: Running
 ```

**4.2 Verify Forwarder in Splunk**
In Splunk Web:
**Settings → Forwarder Management**
Expected:
- 1 active forwarder
- Client name: **DC01**
- Status: **Connected**

**4.3 Verify Logs Are Flowing**
In Splunk Web → Search & Reporting:
 ```Code
 index=* host=DC01 | head 20
 ```
Expected results:
- Security logs
- System logs
- Application logs
- AD DS logs
- Performance metrics

This confirms the SIEM pipeline is operational.

---

## 5. Outcome
DC01 is now fully integrated with Splunk Enterprise and forwarding:
- Windows Event Logs
- Active Directory logs
- Performance metrics

This forms the foundation for:
- Sysmon integration
- PowerShell logging
- AD deep-dive auditing
- Detection engineering
- Attack simulation
- SOC workflows

Your SIEM enviornment is officially online.

---

## 6. Next Steps (Planned)
- Install Sysmon with hardened config
- Add Sysmon Event ID ingestion
- Enable PoweShell Script Block Logging
- Add AD DS advanced auditing
- Build detection searches
- Simulate attacks (Kerberoasting, brute force, lateral movement)



