# Security Options Hardening

## Overview
Security Options provide granular control over authentication, network communication, and account behavior. These settings reduce attack surface, prevent legacy protocol abuse, and enforce secure communication across the domain.

## Settings Applied

### Network Security
- LAN Manager authentication level: Send NTLMv2 response only  
- SMBv1 disabled  
- Digitally sign client communications: Enabled  
- Digitally sign server communications: Enabled  

### Account Restrictions
- Guest account: Disabled  
- Administrator account: Disabled (if applicable)  
- Do not allow anonymous enumeration of SAM accounts: Enabled  
- Do not allow anonymous enumeration of SAM accounts and shares: Enabled  

## Why This Matters
These settings prevent credential downgrade attacks, block anonymous reconnaissance, enforce secure communication, and reduce exposure to legacy protocols. They align with Security+ Domain 3 (Implementation) and common enterprise hardening baselines.

## Configuration Steps
1. Open Group Policy Management (`gpmc.msc`)
2. Edit the Default Domain Policy
3. Navigate to:
   `Computer Configuration → Policies → Windows Settings → Security Settings → Local Policies → Security Options`
4. Apply the settings listed above

## Screenshots

### Network Security

**LAN Manager authentication level: Send NTLMv2 response only**
![LAN Manager authentication level: Send NTLMv2 response only](Screenshots/security-options-enforce-NTLMv2-authentication.PNG)

**SMBv1 disabled**
![SMBv1 disabled](Screenshots/security-options-disable-SMBv1.PNG)

**Digitally sign client communications: Enabled**
![Digitally sign client communications: Enabled](Screenshots/security-options-require-digital-signing-mnclient.PNG)

**Digitally sign server communications: Enabled**
![Digitally sign server communications: Enabled](Screenshots/security-options-require-digital-signing-mnserver.PNG)

### Account Restrictions

**Guest account: Disabled**
![Guest account: Disabled](Screenshots/security-options-disable-guest-account.PNG)

**Administrator account: Disabled (if applicable)**
![Administrator account: Disabled (if applicable)](Screenshots/security-options-disable-admin-account-optional.PNG
)

**Do not allow anonymous enumeration of SAM accounts: Enabled**
![Do not allow anonymous enumeration of SAM accounts: Enabled](Screenshots/security-options-restrict-anonymous-access.PNG)

**Do not allow anonymous enumeration of SAM accounts and shares: Enabled**
![Do not allow anonymous enumeration of SAM accounts and shares: Enabled](Screenshots/security-options-restrict-anonymous-access.PNG)

## Summary
Security Options hardening strengthens authentication, reduces attack surface, and enforces secure communication across the domain.
