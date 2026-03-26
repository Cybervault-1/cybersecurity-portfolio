# Splunk Log Analysis – Insider Threat / Suspicious Login Detection

## Overview

This project investigates unusual login behavior by analyzing authentication logs in Splunk. The goal is to identify anomalies in user activity that may indicate account compromise or unauthorized access.

---

## Objective

To detect suspicious login patterns by identifying users accessing systems from multiple IP addresses within short time intervals.

---

## Tools Used

* Splunk (SIEM)
* SSH authentication logs

---

## Investigation Steps

### 1. View all logs

```
index=main sourcetype=insider_log
```

---

### 2. Sort logs by time (timeline analysis)

```
index=main sourcetype=insider_log
| sort _time
```

---

### 3. Focus on specific user activity

```
index=main sourcetype=insider_log "david"
```

---

### 4. Extract IP addresses and analyze login pattern

```
index=main sourcetype=insider_log "Accepted password"
| rex "from (?<ip>\d+\.\d+\.\d+\.\d+)"
| rex "user (?<user>\w+)"
| table _time user ip
| sort _time
```

---

## Findings

* The user **david** exhibited inconsistent login behavior across multiple IP addresses
* A total of **7 login events** were observed
* Logins originated from:

  * **192.168.1.10** (internal)
  * **203.0.113.200** (external)
  * **10.0.0.5** (internal)

---

## Timeline of Activity

* **13:00:00** → Login from 192.168.1.10
* **13:02:00** → Login from 203.0.113.200 ⚠️
* **13:10:00** → Login from 192.168.1.10
* **13:11:00** → Login from 203.0.113.200 ⚠️
* **13:25:00** → Login from 10.0.0.5
* **13:45:00** → Login from 203.0.113.200 ⚠️
* **14:00:00** → Login from 192.168.1.10

---

## Security Analysis

* The user logged in from multiple IP addresses within short time intervals
* Rapid switching between internal and external IP addresses is highly unusual
* Example:

  * 13:00 → Internal IP
  * 13:02 → External IP (2 minutes later)

This behavior suggests:

* Potential account compromise
* Possible credential sharing
* Unauthorized remote access

---

## Conclusion

This activity indicates **suspicious login behavior consistent with a potential insider threat or compromised account**, due to rapid IP switching and the involvement of external network sources.

---

## Recommendations

* Investigate IP address **203.0.113.200**
* Reset david’s account credentials
* Enable multi-factor authentication (MFA)
* Monitor user activity for further anomalies
* Review logs for lateral movement or additional compromise

---

## Skills Demonstrated

* Log analysis
* Behavioral analysis
* Timeline reconstruction
* Threat detection
* SIEM investigation
