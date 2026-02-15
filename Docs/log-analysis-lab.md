# Log Monitoring & Analysis – Practical Lab

## Lab Objective
Perform authentication log monitoring to detect suspicious login attempts and anomalies using Linux logs.



## Step 1: Locate Authentication Logs
In Linux systems, authentication logs are stored at:

- /var/log/auth.log   (Debian / Kali)
- /var/log/secure     (CentOS / RHEL)

Open log file:

- sudo cat /var/log/auth.log



## Step 2: Identify Failed Login Attempts
Use grep to find failed authentication attempts:

- sudo grep "Failed password" /var/log/auth.log

This helps identify brute-force login attempts.



## Step 3: Identify Successful Logins
- sudo grep "Accepted password" /var/log/auth.log

Compare successful and failed attempts from same IP to detect compromise.



## Step 4: Monitor Logs in Real-Time
- sudo tail -f /var/log/auth.log

This shows live login activity and helps detect ongoing attacks.



## Step 5: Detect Suspicious IP Activity
- Count repeated failures from a single IP:

sudo grep "Failed password" /var/log/auth.log | awk '{print $11}' | sort | uniq -c | sort -nr

IPs with high failure counts may indicate brute-force attempts.



## Step 6: Basic Event Correlation
Check if the same IP later logged in successfully:

- sudo grep "192.168.1.15" /var/log/auth.log

This helps detect attacker success after multiple attempts.



## Step 7: Create Simple Alert Script (Basic SIEM Concept)
Example simple alert:

- sudo grep "Failed password" /var/log/auth.log | wc -l

If failures exceed threshold → possible alert condition.



## Lab Outcome
After completing this lab you should be able to:
- Identify authentication logs
- Detect failed login attempts
- Identify suspicious IP addresses
- Monitor logs in real-time
- Understand basic SIEM monitoring concepts
