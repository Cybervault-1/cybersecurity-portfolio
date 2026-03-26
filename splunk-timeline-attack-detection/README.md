# Splunk Log Analysis – Timeline Attack Detection

## Overview

This project demonstrates the investigation of a suspected account compromise by analyzing authentication logs in Splunk. The focus is on identifying suspicious login patterns and reconstructing the timeline of attacker activity.

---

## Objective

To detect abnormal login behavior by analyzing failed and successful authentication attempts and identifying potential account compromise.

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

### 2. Build event timeline

```
index=main sourcetype=compromise_log
| sort _time
```

---

### 3. Track activity from suspicious IP

```
index=main sourcetype=compromise_log 45.33.32.156
```

---

### 4. Identify failed login attempts

```
index=main sourcetype=compromise_log failed
```

---

### 5. Identify successful logins

```
index=main sourcetype=compromise_log "Accepted password"
```

---

## Findings

* The IP address **45.33.32.156** performed multiple login attempts within a short time frame
* Initial attempts targeted **admin** and **root** accounts and failed
* The attacker made:

  * 2 failed attempts on the admin account
  * 1 failed attempt on the root account
* The same IP later successfully logged into the user account **"michael"**
* Two successful logins were recorded:

  * 11:01:05 AM
  * 11:04:00 AM

---

## Timeline of Events

* 11:00:10 AM → Failed login (admin)
* 11:00:15 AM → Failed login (admin)
* 11:00:20 AM → Failed login (root)
* 11:01:05 AM → Successful login (michael)
* 11:04:00 AM → Second successful login (michael)

---

## Security Analysis

* The attacker initially targeted high-privilege accounts (admin and root)
* After failing, the attacker shifted to a lower-privilege account (michael)
* The successful login shortly after failed attempts indicates password compromise
* Repeated successful access confirms unauthorized use of the account

---

## Conclusion

This activity represents a **confirmed account compromise**, where an attacker gained access to the "michael" account after multiple failed login attempts on other accounts.

---

## Recommendations

* Reset password for the compromised account (michael)
* Enable multi-factor authentication (MFA)
* Block or monitor IP address 45.33.32.156
* Implement account lockout policies after multiple failed attempts

---

## Skills Demonstrated

* Log analysis
* Timeline reconstruction
* Threat detection
* Event correlation
* SIEM investigation
