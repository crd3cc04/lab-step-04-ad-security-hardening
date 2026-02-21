# Attack Simulation

## Purpose
This section contains controlled attack scenarios used to test the effectiveness of security hardening and SIEM monitoring.

## Scenarios
### 1. Brute-Force Attack
Located in `Brute-Force/`:
- Multiple failed logons
- Event ID 4625 analysis
- Successful logon (4624)

### 2. Privilege Escalation
Located in `Privilege-Escalation/`:
- Group membership changes
- Event IDs 4728–4732

### 3. Suspicious PowerShell
Located in `Suspicious-PowerShell/`:
- Execution of encoded commands
- Event ID 4104

### 4. Unauthorized Access
Located in `Unauthorized-Access/`:
- Access to restricted shares
- Event ID 5140

## Documentation Format
Each scenario includes:
- Description of the attack
- Steps taken to simulate it
- Logs captured
- Screenshots
- Summary of findings
