# Cybersecurity Portfolio - Adetayo Adedeji

## About Me

Aspiring SOC Analyst with hands-on experience in log analysis, threat detection, and security investigations. Passionate about identifying threats and continuously building real-world cybersecurity skills.

## Skills

* SIEM: Splunk
* Networking: TCP/IP, DNS, HTTP
* Tools: Wireshark, Linux
* Security: Threat Detection, Incident Response
* Log Analysis: Investigating authentication and security events

## Projects

### 🔍 Splunk Log Analysis – Brute Force Detection

* Investigated failed login attempts using log data
* Identified suspicious IP activity
* Detected potential brute-force attack

👉 [View Project](./splunk-brute-force-detection)
### 🔍 Splunk Log Analysis – Brute Force Detection

## Incident Summary

Analysis of SSH authentication logs revealed multiple failed login attempts from several IP addresses.

The most active IP address (203.0.113.5) generated 6 failed login attempts using different usernames, indicating a brute-force attack pattern.

## Findings

* 203.0.113.5 → 6 failed attempts
* 192.168.1.10 → 5 failed attempts
* 198.51.100.23 → 5 failed attempts

Multiple usernames were targeted, including admin, root, guest, oracle, and postgres.

## Security Concern

Successful login events were also identified in the logs, suggesting that at least some login attempts succeeded.

## Conclusion

The activity is consistent with a brute-force attack, and the presence of successful logins raises concern for potential unauthorized access.

## Recommendation

* Investigate successful login accounts
* Block suspicious IP addresses
* Enable multi-factor authentication (MFA)
* Monitor for further suspicious activity

## Contact

* Email: adedejiadetayo33@gmail.com
* LinkedIn: (add later)
