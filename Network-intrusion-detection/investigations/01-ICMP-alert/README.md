# Investigation 01 — ICMP Traffic Detection

## 1. Investigation Overview

This investigation demonstrates the detection and analysis of ICMP
traffic within an isolated laboratory network.

Traffic was generated from a Kali Linux system to an Ubuntu system
running Suricata IDS.

The activity was monitored using Suricata and analyzed using Wireshark.

---

## 2. Lab Environment

| Component | Details |
|---|---|
| Traffic Source | Kali Linux |
| IDS | Suricata 8.0.3 |
| Monitoring System | Ubuntu |
| Packet Analyzer | Wireshark |
| Network | Isolated Host-Only Network |
| Ubuntu Interface | enp0s3 |

---

## 3. Network Information

| System | IP Address | Role |
|---|---|---|
| Kali Linux | 192.168.56.101 | Traffic Generator |
| Ubuntu | 192.168.56.103 | IDS / Monitoring |


---

## 4. Detection Scenario

A controlled ICMP ping was generated from the Kali Linux machine
towards the Ubuntu monitoring system.

The purpose was to verify that:

1. Network traffic reaches the monitoring interface.
2. Suricata detects the traffic using a custom rule.
3. Suricata generates an alert.
4. The alert is recorded in the logs.
5. Wireshark can be used to validate the corresponding packets.

---

## 5. Traffic Generation

The following command was executed from Kali Linux:

```bash
ping 192.168.56.103