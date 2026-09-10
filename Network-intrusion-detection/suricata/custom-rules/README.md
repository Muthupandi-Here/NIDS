# Custom Suricata Detection Rules

## Overview

This directory contains custom Suricata IDS rules developed and tested
for the Network Intrusion Detection project.

The purpose of these rules is to detect specific network activities
generated within an isolated security laboratory.

The rules allow the project to demonstrate the complete detection
workflow:

Network Traffic → Suricata Rule → Alert → Investigation → Response

---

## Environment

| Component | Details |
|---|---|
| IDS | Suricata 8.0.3 |
| Operating System | Ubuntu |
| Monitoring Interface | enp0s3 |
| Traffic Generator | Kali Linux |
| Network | Isolated Host-Only Lab |
| Packet Analysis | Wireshark |

---

## Rule File

The primary custom rule file is:

```text
local.rules