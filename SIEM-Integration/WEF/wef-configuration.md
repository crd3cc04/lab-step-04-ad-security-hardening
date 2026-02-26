# 🛡️ Windows Event Forwarding (WEF) Configuration

## Overview

This document details the configuration of Windows Event Forwarding (WEF) on the domain controller to enable centralized log collection for SIEM analysis. This setup supports real-time monitoring, threat detection, and incident response, core competencies in Security+ and SOC operations.

---

## ⭐ 1. Enable Windows Remote Management (WinRM)

WinRM is required for source-initiated event forwarding. Run the following command in Powershell (as Administrator):

```Code

winrm quickconfig

```
If prompted to enable WinRM or create a listener, select Y.

### Screenshot

screenshots/winrm-quickconfig.png

### Security+ Alignment

- **Domain 3.0 - Implementation:** Secure remote management configuration.
- **Domain 2.0 - Architecture:** Enables centralized log collection.

---

## ⭐ 2. Initialize Windows Event Collector Service

Run:

```Code

wecutil qc

```

This configures the Windows Event Collector service and sets it to **Automatic (Delayed Start)**, expected behavior for WEF.

### Screenshot

screenshots/wecutil-qc.png

### Security+ Alignment

- **Domain 4.0 - Operations & IR:** Centralized logging supports correlation and detection.

---

## ⭐ 3. Configure Subscription Manager via Group Policy

Create a new GPO:

**Name:**

```Code

WEF - Subscription Manager

```

**Path:**

```Code

Computer Configuration  
   → Policies  
      → Administrative Templates  
         → Windows Components  
            → Event Forwarding  
               → Configure target Subscription Manager

```

Set to **Enabled**, then click **Show**... and add:

```Code

Server=http://<SIEM-IP>:5985/wsman/SubscriptionManager/WEC,Refresh=60

```
Replace ```<SIEM-IP>``` with the IP address of your SIRM or collector server.

### Screenshot

screenshots/gpo-subscription-manager.png

### Security+ Alignment

- **Domain 3.0 - Implementation:** Log forwarding is a core secure configuration.
- **Domain 4.0 - IR:** Supports centralized event correlation.

---

## ⭐ 4. Create Event Subscription on the Collector

Open **Event Viewer** on the SIEM/collector server:

```Code

Event Viewer → Subscriptions → Create Subscription

```

### Subscription Settings

- **Name:** Domain Controller Security logs
- **Destination Log:** Forwarded Events
- **Type:** Source computer initiated

### Screenshot

screenshots/subscription-main.png

---

### 4.1 Add Source Computers

Click **Select Computer Groups**...
Add your domain controller:

```Code

DC01.lab.local

```

### Screenshot

screenshots/subscription-computer-group.png

---

### 4.2 Select Event to Collect

Click **Select Event**...
Choose **By log**, then select:

- Security
- System
- Windows Powershell
- Microsoft-Windows-Powershell/Operational
- Microsoft-Windows-Sysmon/Operational (if Sysmon is installed later)

### Screenshot

screenshots/subscription-events.png

---

### 4.3 Configure Advanced Settings

Click **Advanced**..

Set:

- **Event Delivery Optimization:** Minimize Latency
- **Protocol:** HTTP
- **Heartbeat Interval:** Default

### Screenshot

screenshots/subscription-advanced.png

---

## ⭐ 5. Apply GPO and Verify Log Flow

On the domain controller:

```Code

gpupdate /force

```
On the SIEM/collector:
Restart the Windows Event Collector service:

```Code

Restart-Service Wecsvc

```
Within a few minutes, verify:

- DC01 appears under **Runtime Status**
- Events populate in **Forwarded Events**

### Screenshot

screenshots/runtime-status.png

### Collector Not Yet Installed

The domain controller has been fully configured as a Windows Event Forwarding (WEF) source.  
Log flow verification will be completed once the SIEM/collector server is deployed in a later phase.


---

## 🔐 Security+ Alignment Summary

**Domain 4.0 - Operations & Incident Response**

- Centralized logging enables correlation, alerting, and forensic analysis.

**Domain 3.0 - Implementation**

- Secure configuration of remote management and event forwarding.

**Domain 2.0 - Architecture & Design**

- Supports defense-in-depth and centralized monitoring.

**Domain 1.0 - Threats**

- Enables detection of brute force, privilege escalation, Powershell abuse, lateral movement, and Kerberos attacks.

