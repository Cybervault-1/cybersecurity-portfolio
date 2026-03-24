# Splunk Log Analysis – Brute Force Detection

## Objective

Detect suspicious login attempts using Splunk by analyzing authentication logs.

## Tools Used

* Splunk (SIEM)
* Sample auth.log file

## Log Source

The log file contains SSH authentication activity, including successful and failed login attempts.

## Steps Taken

1. Uploaded the log file into Splunk
2. Searched all logs:
   index=main
3. Filtered failed login attempts:
   failed
4. Analyzed IP activity:
   stats count by from

## Findings

* Multiple failed login attempts were detected from IP 192.168.1.10
* Repeated authentication failures indicate suspicious behavior

## Conclusion

The repeated failed login attempts suggest a possible brute-force attack targeting the system.

## Skills Demonstrated

* Log analysis
* Threat detection
* SIEM usage (Splunk)
* Basic incident investigation

## Screenshots

(To be added after analysis in Splunk)
