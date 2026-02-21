# Password Policy Hardening

## Overview
This policy enforces strong password requirements across the domain to reduce the risk of credential compromise.

## Settings Applied
- Minimum password length: 14 characters
- Password complexity: Enabled
- Maximum password age: 60 days
- Minimum password age: 1 day

## Why This Matters
Weak passwords are one of the most common attack vectors. Enforcing strong password policies aligns with Security+ Domain 3 (Implementation) and reduces brute-force and credential stuffing risks.

## Configuration Steps
1. Open Group Policy Management
2. Edit the Default Domain Policy
3. Navigate to:
   `Computer Configuration → Policies → Windows Settings → Security Settings → Account Policies → Password Policy`
4. Apply the settings listed above

## Screenshots
![Password Policy Screenshot](Screenshots/security-hardening-password-policy)

## Summary
This hardening step strengthens domain authentication and reduces the likelihood of unauthorized access.





