# 🛡️ IDS Lab - Snort & Suricata

## Overview
A hands-on home lab simulating a real SOC environment using two industry-standard 
Intrusion Detection Systems. Kali Linux was used as the attacker machine to generate 
malicious traffic, while Ubuntu monitored and detected threats in real time.

## 🎯 Objective
Demonstrate the ability to deploy, configure, and validate IDS tools used in 
SOC environments for network threat detection and alert triage.

## 🛠️ Tools & Technologies
- Snort 2.9.20
- Suricata 7.0.3
- Kali Linux (attacker)
- Ubuntu 24.04 (defender/monitor)
- VirtualBox (lab environment)
- Nmap (attack simulation)

## 🔬 Lab Architecture
[Kali Linux] --> (attack traffic) --> [Ubuntu IDS]
- Network: Host-only adapter (192.168.56.0/24)
- Kali IP: 192.168.56.101
- Ubuntu IP: 192.168.56.102

## ⚔️ Attacks Simulated & Detected
| Attack | Tool Used | Alert Triggered |
|--------|-----------|----------------|
| ICMP Ping Sweep | ping | ICMP Ping Detected |
| SYN Port Scan | nmap -sS | Port Scan Detected |
| SSH Brute Force Attempt | nmap | SSH Connection Attempt |

## 📋 Custom Rules Written
### Snort
alert icmp any any -> any any (msg:"ICMP Ping Detected"; sid:1000001; rev:1;)
alert tcp any any -> $HOME_NET any (msg:"Port Scan Detected"; flags:S; sid:1000002; rev:1;)
alert tcp any any -> $HOME_NET 22 (msg:"SSH Connection Attempt"; sid:1000003; rev:1;)

### Suricata
alert icmp any any -> $HOME_NET any (msg:"ICMP Ping Detected"; sid:9000001; rev:1;)
alert tcp any any -> $HOME_NET any (msg:"Port Scan Detected"; flags:S; sid:9000002; rev:1;)
alert tcp any any -> $HOME_NET 22 (msg:"SSH Connection Attempt"; sid:9000003; rev:1;)

## 📊 Snort vs Suricata Comparison
| Feature | Snort | Suricata |
|---------|-------|----------|
| Version | 2.9.20 | 7.0.3 |
| Threading | Single-threaded | Multi-threaded |
| Alert Output | Console (fast) | fast.log + eve.json |
| Rule Format | Snort rules | Snort-compatible + extras |
| Performance | Good for low traffic | Better for high traffic |
| Log Format | Text | JSON (eve.json) |

## 🔑 Key Skills Demonstrated
- IDS deployment and configuration
- Custom rule writing for threat detection
- Network traffic analysis
- Attack simulation and detection validation
- SOC alert triage workflow
- Linux system administration
- Virtualized lab environment setup

## 📸 Screenshots
See /screenshots folder for evidence of detections.

## 👤 Author
GitHub: raphsec
