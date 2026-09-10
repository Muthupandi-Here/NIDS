# Investigation 02 – TCP SYN Port Scan

## Objective

Detect and investigate TCP SYN port scanning activity
using Suricata IDS.

## Source

Kali Linux

## Destination

Ubuntu Linux

## Attack Technique

TCP SYN Port Scan

## Tool

Nmap

## Detection

Suricata custom IDS rule

## Command Used

nmap -sS -p 1-1000 <192.168.56.103>

## Alert

NIDS ALERT - Possible TCP SYN Port Scan

## Source IP

192.168.56.101

## Destination IP

192.168.56.103

## Protocol

TCP

## Severity

Medium

## MITRE ATT&CK

T1046 – Network Service Scanning

## Analyst Assessment

The traffic indicates network reconnaissance activity originating
from the Kali Linux host. Multiple TCP SYN packets were observed
against multiple destination ports on the Ubuntu host.

The activity is consistent with a TCP SYN port scan.

## Conclusion

The activity was confirmed as a controlled port-scanning test
performed from the Kali test machine against the Ubuntu monitored
host.

## Recommended Action

In a production environment, investigate the source host,
correlate the activity with firewall and endpoint logs, and
determine whether the scanning is authorized.