# Scenario 03 – SSH Brute-Force Detection

## 📌 Overview

Simulated repeated SSH login attempts from Kali Linux against an Ubuntu server and investigated the activity using Suricata and Linux authentication logs.

## 🎯 Objective

* Detect SSH activity on TCP port 22
* Identify repeated failed login attempts
* Correlate Suricata and `auth.log`
* Check for successful authentication
* Map the activity to MITRE ATT&CK

## 🧪 Lab

```text
Kali Linux → SSH → Ubuntu Server
                  ↓
               Suricata
                  ↓
        EVE.json + auth.log
```

## 🔎 Investigation

Filter SSH traffic:

```bash
sudo jq 'select(.dest_port == 22)' /var/log/suricata/eve.json
```

Check failed logins:

```bash
sudo grep "Failed password" /var/log/auth.log
```

Check successful logins:

```bash
sudo grep "Accepted" /var/log/auth.log
```

## 🚨 Finding

Multiple failed SSH authentication attempts were observed from the Kali Linux 192.168.56.101 targeting the Ubuntu server on TCP port 22.

**Classification:** True Positive – SSH Brute-Force Attempt

## 🧠 MITRE ATT&CK

**T1110 – Brute Force**
**T1110.001 – Password Guessing**

## 🛡️ Recommendation

* Investigate the source IP
* Check for successful authentication
* Review post-login activity
* Block/restrict suspicious sources according to policy
* Use stronger authentication such as SSH keys/MFA

## 📸 Evidence

* Suricata EVE JSON
* `auth.log`
* Wireshark capture
* SSH failed-login evidence
