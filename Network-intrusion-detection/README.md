🛡️ Network Intrusion Detection System (NIDS)

A practical Network Intrusion Detection System (NIDS) built using Suricata to monitor network traffic, detect suspicious activities, and generate security alerts.

The project uses Ubuntu as the IDS machine and Kali Linux as the testing/traffic-generation machine. Wireshark is used for packet-level traffic analysis and verification.

---

📌 Project Overview

The purpose of this project is to build a small-scale network monitoring and intrusion detection environment.

The system continuously monitors network traffic and uses predefined/custom Suricata rules to identify potentially malicious activities.

When suspicious traffic matches a detection rule, Suricata generates an alert that can be investigated by a security analyst.

Architecture

                 ┌─────────────────────┐
                 │      Host Machine   │
                 │    VirtualBox       │
                 └──────────┬──────────┘
                            │
                Host-Only / Virtual Network
                            │
             ┌──────────────┴──────────────┐
             │                             │
   ┌─────────▼─────────┐         ┌─────────▼─────────┐
   │    Kali Linux     │         │      Ubuntu       │
   │                   │         │                   │
   │ Traffic Generator │ ──────► │ Suricata IDS      │
   │ Nmap / Test Tools  │ Traffic│ Custom Rules      │
   └───────────────────┘         │ Alert Generation  │
                                 └─────────┬─────────┘
                                           │
                                  ┌────────▼────────┐
                                  │    Wireshark    │
                                  │ Packet Analysis │
                                  └─────────────────┘

---

🎯 Objectives

- Monitor network traffic in real time.
- Detect suspicious and potentially malicious network activity.
- Create and test custom Suricata detection rules.
- Analyze network packets using Wireshark.
- Generate and investigate IDS alerts.
- Understand the workflow of a SOC Analyst L1.
- Practice basic network security monitoring and incident investigation.

---

🧰 Tools & Technologies

Tool| Purpose
Ubuntu| IDS / monitoring machine
Kali Linux| Security testing and traffic generation
Suricata| Network Intrusion Detection System
Wireshark| Packet capture and analysis
Nmap| Network scanning/testing
VirtualBox| Virtual lab environment
Linux CLI| System administration and investigation

---

🖥️ Lab Environment

Ubuntu

Ubuntu is configured as the IDS machine.

Responsibilities:

- Run Suricata
- Monitor network traffic
- Apply detection rules
- Generate alerts
- Store logs

Kali Linux

Kali Linux is used as the testing machine.

Responsibilities:

- Generate controlled network traffic
- Perform network scanning
- Test IDS detection rules
- Verify Suricata alerts

«All security testing in this project is performed inside an isolated virtual lab.»

---

⚙️ Suricata Configuration

After installing Suricata, identify the network interface:

ip addr

Example:

enp0s3

Check Suricata configuration:

sudo suricata -T -c /etc/suricata/suricata.yaml

A successful configuration test should indicate that the configuration is valid.

---

📝 Custom Detection Rules

Custom rules are stored in:

/etc/suricata/rules/

Example custom rule:

alert icmp any any -> any any (msg:"ICMP Ping Detected"; sid:1000001; rev:1;)

This rule generates an alert when ICMP traffic is detected.

Rule Components

alert

Action taken by Suricata.

icmp

Protocol being monitored.

any any -> any any

Source and destination network/port.

msg:"ICMP Ping Detected"

Alert message.

sid:1000001

Unique rule identifier.

rev:1

Rule revision number.

---

🚀 Running Suricata

Start Suricata manually:

sudo suricata -c /etc/suricata/suricata.yaml -i <interface>

Example:

sudo suricata -c /etc/suricata/suricata.yaml -i enp0s3

Check whether the service is running:

sudo systemctl status suricata

Start the service:

sudo systemctl start suricata

Enable Suricata at boot:

sudo systemctl enable suricata

---

📊 Monitoring Alerts

Suricata generates logs in:

/var/log/suricata/

View fast alerts:

sudo tail -f /var/log/suricata/fast.log

View structured alerts:

/var/log/suricata/eve.json

The "eve.json" file contains detailed information about detected events, including:

- Timestamp
- Source IP
- Destination IP
- Source port
- Destination port
- Protocol
- Alert signature
- Severity
- Rule ID

---

🔎 Traffic Analysis with Wireshark

Wireshark is used to capture and analyze packets.

Example display filters:

ICMP traffic

icmp

TCP traffic

tcp

Specific IP

ip.addr == 192.168.56.101

DNS traffic

dns

Wireshark helps verify whether the traffic that triggered a Suricata alert actually occurred.

---

🧪 Testing the IDS

From Kali Linux, controlled traffic can be generated against the Ubuntu lab machine.

ICMP Test

ping <ubuntu-ip>

For example:

ping 192.168.56.102

Suricata should detect the ICMP traffic if the corresponding rule is enabled.

---

Nmap Scan Test

From Kali:

nmap <ubuntu-ip>

Example:

nmap 192.168.56.102

The scan generates network traffic that can be monitored using Wireshark and Suricata.

«Only perform scanning against machines in your own lab or systems where you have explicit authorization.»

---

🔍 Alert Investigation Workflow

The investigation process follows a simplified SOC Analyst workflow:

Network Traffic
      ↓
Suricata Monitoring
      ↓
Rule Match
      ↓
Security Alert
      ↓
Alert Validation
      ↓
Wireshark Packet Analysis
      ↓
Source/Destination Investigation
      ↓
Determine Severity
      ↓
Document Findings
      ↓
Recommended Response

---

📋 Example Analyst Investigation

Alert

Alert: ICMP Ping Detected
Source IP: 192.168.56.101
Destination IP: 192.168.56.102
Protocol: ICMP
Severity: Low

Investigation

1. Identify the source IP.
2. Identify the destination IP.
3. Verify whether the source system belongs to the lab.
4. Check the corresponding packets in Wireshark.
5. Determine whether the traffic is expected or suspicious.
6. Record the investigation result.

Example Conclusion

The alert was generated due to ICMP traffic from the Kali Linux
testing machine to the Ubuntu IDS machine. The traffic was
generated intentionally as part of the authorized lab test.

Classification: Benign / Expected Activity

---

📁 Project Structure

network-intrusion-detection/
│
├── README.md
│
├── rules/
│   └── custom.rules
│
├── screenshots/
│   ├── suricata-running.png
│   ├── custom-rule.png
│   ├── wireshark-capture.png
│   └── suricata-alert.png
│
├── alerts/
│   └── sample-alert.json
│
├── reports/
│   └── investigation-report.md
│
└── documentation/
    └── lab-setup.md

---

📸 Evidence

Screenshots and packet captures can be added to demonstrate:

- Virtual machine network configuration
- Suricata service status
- Custom Suricata rules
- Kali traffic generation
- Wireshark packet capture
- Suricata alerts
- Alert investigation

---

🛡️ Security Concepts Demonstrated

This project demonstrates practical knowledge of:

- Network monitoring
- Packet analysis
- Intrusion detection
- Signature-based detection
- Custom IDS rules
- IP addresses and ports
- TCP/IP
- ICMP
- Network scanning
- Security alerts
- Alert triage
- Basic incident investigation
- SOC Analyst L1 workflow

---

📈 Future Improvements

The project can be extended by adding:

- ELK Stack integration
- Wazuh integration
- Splunk log ingestion
- Automated alert dashboards
- More custom Suricata rules
- MITRE ATT&CK mapping
- Automated alert classification
- Email/Telegram notifications
- Centralized log management

---

🎓 Learning Outcome

Through this project, I gained hands-on experience in setting up a network security monitoring environment, writing and testing Suricata rules, analyzing packets using Wireshark, and investigating security alerts.

The project also helped me understand the basic workflow followed by a SOC Analyst L1 during alert investigation.

---

⚠️ Disclaimer

This project is intended for educational and authorized security testing purposes only.

All scanning and traffic-generation activities should be performed only against systems that you own or have explicit permission to test.

---

👨‍💻 Author

Muthupandi

Computer Science Student
Cybersecurity / SOC Analyst L1 Learner

---

⭐ Project Highlights

✔ Ubuntu + Suricata IDS
✔ Kali Linux testing environment
✔ Wireshark packet analysis
✔ Custom detection rules
✔ Security alert generation
✔ Alert investigation workflow
✔ SOC Analyst L1 practical experience