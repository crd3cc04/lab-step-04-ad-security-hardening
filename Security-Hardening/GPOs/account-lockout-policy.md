# Account Lockout Policy Hardening

## Overview
This policy protects domain accounts from brute-force and password spraying attacks by locking accounts after repeated failed authentication attempts.

## Settings Applied
- Account lockout threshold: 5 invalid attempts  
- Account lockout duration: 30 minutes  
- Reset account lockout counter after: 30 minutes  

## Why This Matters
Lockout policies slow down attackers attempting to guess passwords and provide clear indicators of malicious activity. These settings align with Security+ Domain 3 (Implementation).

## Configuration Steps
1. Open Group Policy Management (`gpmc.msc`)
2. Edit the Default Domain Policy
3. Navigate to:
   `Computer Configuration → Policies → Windows Settings → Security Settings → Account Policies → Account Lockout Policy`
4. Apply the settings listed above

## Screenshot
![Account Lockout Policy Screenshot](Screenshots\account-lockout-policy.PNG)

## Summary
This configuration strengthens authentication security and provides early warning signs of brute-force attempts.


