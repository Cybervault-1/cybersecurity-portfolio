# Splunk Log Analysis – Account Compromise Detection

## Overview

This project demonstrates the detection of a potential account compromise using Splunk by analyzing SSH authentication logs.

---

## Objective

Identify suspicious login behavior, including failed login attempts followed by successful logins from the same IP address.

---

## Tools Used

* Splunk (SIEM)
* SSH authentication logs

---

## Investigation Steps

### 1. View all logs

```
index=main sourcetype=compromise_log
```

---

### 2. Identify failed login attempts

```
index=main sourcetype=compromise_log failed
```

---

### 3. Extract attacker IPs

```
index=main sourcetype=compromise_log failed 
| rex "from (?<ip>\d+\.\d+\.\d+\.\d+)" 
| stats count by ip 
| sort - count
```

---

### 4. Identify successful logins

```
index=main sourcetype=compromise_log "Accepted password"
```

---

### 5. Extract usernames from successful logins

```
index=main sourcetype=compromise_log "Accepted password" 
| rex "user (?<user>\w+)" 
| stats count by user
```

---

## Findings

* Suspicious IP: 203.0.113.5
* This IP performed multiple failed login attempts
* The same IP attempted access to multiple accounts

---

## Security Concern

The pattern of repeated failed attempts suggests a **brute-force attack**, which could eventually lead to account compromise if successful.

---

## Conclusion

This activity indicates a **potential account compromise attempt** through brute-force login attacks.

---

## Recommendations

* Enable multi-factor authentication (MFA)
* Block or monitor suspicious IP addresses
* Implement account lockout policies
* Monitor login activity continuously

---

## Skills Demonstrated

* Log analysis
* Threat detection
* Regex (field extraction)
* SIEM investigation
