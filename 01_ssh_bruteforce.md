# SSH Brute Force Detection

## Scenario Overview

This detection focuses on identifying SSH brute-force attacks by analyzing repeated authentication attempts from single or multiple source IP addresses.  
Brute-force attacks attempt to gain unauthorized access by systematically guessing credentials.

---

## 🎯 Objective

- Detect excessive SSH login attempts  
- Identify attacker source IPs  
- Analyze success/failure patterns  
- Validate brute-force behavior  
- Map activity to MITRE ATT&CK  

---

## Dataset Information

- **Log Source:** [Custom SSH authentication logs (`ssh_logs.json`)](https://drive.google.com/drive/folders/1BL-kVlc3yCRcAH8NnDmAyRm_3j_2mNLM?usp=sharing)  
- **Log Type:** SSH authentication events  
- **Fields Used:**
  - `auth_attempts`
  - `auth_success`
  - `id.orig_h` (Source IP address)
  - `ts` (Timestamp)

---

## Log Ingestion and Index verification

after we ingest the `ssh_logs.json` log file, we will verify the created Index in Splunk-Web

![SSH Logs Index verification](https://github.com/ashish6t7/Threat-Detection-Log-Analysis-Splunk/blob/85517efd39a33c626bd4b001cf17f36dfefc4ac1/Detection_Images/ssh_bruteforce/SSH%20Logs%20Index%20verify.png)

Index successfully created and verified !

---

## Detection Logic

Brute-force behavior is identified by:

- High number of authentication attempts  
- Repeated failures  
- Pattern consistency across IPs  

### SPL Query Used

```spl
index=ssh_logs
| where auth_attempts > 5
| table ts id.orig_h auth_success auth_attempts
| sort - auth_attempts
```
![SPL query outcome](https://github.com/ashish6t7/Threat-Detection-Log-Analysis-Splunk/blob/5a9ac56777745f44aff213e936f543a47a97a45b/Detection_Images/ssh_bruteforce/SSH%20SPL%20query%20result.png)

### Findings

- Multiple IPs attempted `repeated SSH logins`
- All authentication attempts `failed`
- **out of 173 results, 56 IPs performed 8 attempts, 59 IPs performed 7 attempts and 58 IPs performed 6 attempts**
- Pattern indicates `automated attack behavior`
- Observed distributed `brute-force activity`
- SPL query used to identify attempt pattern:
```
index=ssh_logs
| where auth_attempts>5
| stats count by auth_attempts
| sort - auth_attempts
```
![Authorization attempts pattern](https://github.com/ashish6t7/Threat-Detection-Log-Analysis-Splunk/blob/902a8984d61f1c348f2fdd9be8093ca95bbb676c/Detection_Images/ssh_bruteforce/auth%20attempts%20pattern.png)

## Analysis

- Uniform attempt count suggests scripted attacks
- Multiple attacking IPs indicate horizontal brute-force
- No successful login observed
- Internal IP range used (lab environment)

## MITRE ATT&CK Mapping

| Technique                      | ID        |
| ------------------------------ | --------- |
| **Brute Force** | **T1110.001** |
| Sub-Technique - **Password Guessing** | **001** |

### Impact

- Potential unauthorized access
- Risk of account lockout
- Credential exposure

## Mitigation Recommendations

- Implement account lockout policies
- enable `MFA` (Multi Factor Authentication)for SSH
- **Restrict** SSH access via firewall rules
- Continuously **monitor** authentication logs
- Use `fail2ban` or similar tools - [fail2ban](https://github.com/fail2ban/fail2ban) - **Fail2ban can automatically block IPs after repeated failed SSH authentication attempts, preventing brute-force attacks in real time.**

## Conclusion

- This detection successfully identified brute-force behavior targeting SSH services.
- The activity shows clear automated attack patterns consistent with known credential attack techniques.
