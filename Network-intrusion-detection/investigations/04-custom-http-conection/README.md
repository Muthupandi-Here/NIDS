# Scenario 04 – HTTP Suspicious Request Detection

## 📌 Overview

Simulated suspicious HTTP requests from Kali Linux to an Ubuntu web server and investigated the traffic using Suricata, Wireshark, and Apache logs.

## 🎯 Objective

* Detect HTTP traffic on port 80
* Identify suspicious URL requests
* Correlate Suricata and Apache logs
* Analyze HTTP packets using Wireshark

## 🧪 Lab

```text
Kali Linux
    │
    │ HTTP Requests
    ▼
Ubuntu Web Server
    │
    ├── Apache access.log
    └── Suricata
          ↓
       eve.json
```

## 🔎 Investigation

Generate HTTP requests:

```bash
curl "http://<UBUNTU_IP>/admin"
curl "http://<UBUNTU_IP>/login"
curl "http://<UBUNTU_IP>/test"
```

Check Apache logs:

```bash
sudo tail -f /var/log/apache2/access.log
```

Filter HTTP traffic in Suricata:

```bash
sudo jq 'select(.dest_port == 80)' /var/log/suricata/eve.json
```

Wireshark filter:

```text
http
```

## 🚨 Finding

Suspicious HTTP requests from the Kali source IP were observed targeting the Ubuntu web server on **TCP port 80**.

**Classification:** Suspicious HTTP Activity

## 📸 Evidence

* Apache access log
* Suricata EVE JSON
* Wireshark HTTP packets
* Source and destination IPs

## 🛡️ Recommendation

* Investigate the source IP
* Review requested URLs
* Check HTTP response codes
* Monitor for repeated or malicious requests
* Block suspicious sources according to security policy
