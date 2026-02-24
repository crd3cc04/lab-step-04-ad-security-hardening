## 🛡️ Windows Firewall Hardening

## Overview

This section documents the hardening of inbound and outbound firwall rules on the domain controller. The goal is to reduce attack surface by disabling unnecessary services while ensuring all Active Directory, critical ports remain available. This aligns with enterprise baselines (CIS, Microsoft Security Baseline, DISA STIG) and CompTIA Security+ best practices.

---

## ✔ Inbound Rules Allowed (Required for AD Functionality)

These rules must remain enabled for the domain controller to operate correctly. My VM already displayed these under Active Directory Domain Controller, DNS, DFS, and Core Networking groups.

## Active Directory Domain Controller

- LDAP (TCP-In/UDP-In)
- LDAP for Global Catalog (TCP-In)
- Secure LDAP (TCP-In)
- Secure LDAP for Global Catalog (TCP-In)
- NetBIOS name resolution (UDP-In)
- SAM/LSA (NP-TCP-In / NP-UDP-In)
- Kerberos Key Distribution Center (TCP/UDP-In)
- Active Directory Domain Controller (RPC)
- Active Directory Domain Controller (RPC-EPMAP)
- W32Time (NTP-UDP-In)
- Active Directory Web Services (TCP-In)

## DNS

- DNS (TCP-In)
- DNS (UDP-In)

## DFS/File Replication

- DFS Namespace
- DFS Replication
- File Replication (RPC)

## Core Networking 

- All Core Networking rules (IPv4/IPv6 stack, DHCP, Router Advertisement, Neighbor Discovery, etc.)

## Remote Desktop (Optional)

- Remote Desktop - User Mode (TCP-In)
- Remote Desktop - Shadow (TCP-In)
***(Keep enabled only if you use RDP)***

---

## ❌ Inbound Rules Disabled (Not Needed on a Domain Controller)

These services are consumer-oriented or unrelated to AD. Disabling them reduces attack surface.

## Disabled Groups

- Cast to Device (qWAve, SSDP, UPnP, streaming)
- AllJoyn Router
- Cortana
- Windows Media Player / Media Sharing
- BranchCache (unless intentionally configured)
- mDNS
- Network Discovery (SSDP, UPnP, WSD)
- DIAL Protocol Server
- Windows Media Player Network Sharing Service

These were safely disabled in the VM.

## ⚠ Optional Rules (Enable Only If Needed)

These are not harmful but not required for AD.

- Windows Remote Management (WinRM)
- File Server Remote Management
- iSCSI Service
- Performance Logs and Alerts

You may leave them enabled or disable them depending on the lab design.

---

## Outbound Rules

Outbound traffic is allowed by default. Optional hardening includes:

- Block outbound SMB to external networks
- Block outbound RDP
- Block outbound FTP/Telnet

These reduce data exflitration and lateral movement.

---

## Custom Rule Example

## Block Powershell Remoting

- Ports: 5985, 5986
- Action: Block
- Profiles: Domain, Private, Public

This prevents remote Powershell sessions, a common attacker technique.

---

## 🔐 Security+ Alignment

## Domain 3.0 - Implementation

- Host-based firewall configuration is a core secure system design control.
- Enforcing least privilege at the network layer reduces unnecessary exposure.

## Domain 2.0 - Architecture & Design

- Firewall support defense-in-depth.
- Limiting services aligns with secure baseline configurations.

## Domain 1.0 - Threats, Attacks, and Vulnerabilities

- Disabling unused ports mitigates:
    - Lateral movement
    - Remote code execution
    - SMB-based attacks (e.g., EternalBlue)
    - Reconnaissance and enumeration

## Domain 4.0 - Operations & Incident Response

- Firewall logs support detection of unauthorized access attempts.
- Clean rule sets improve monitoring and incident response.

---

## Screenshots


---

## Summary

The firewall is now hardening to allow only essential Active Directory services while blocking unnecessary or risky traffic. This configuration reduces attack surface, supports secure domain controller operations, and aligns with Security+ best practices.