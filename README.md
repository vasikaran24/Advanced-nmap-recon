
# Advanced Nmap Reconnaissance Lab

## Overview

This project demonstrates advanced reconnaissance and vulnerability assessment techniques using Nmap in a controlled lab environment. The objective of this project is to understand how penetration testers and security analysts perform network discovery, service enumeration, vulnerability detection, and IDS evasion during security assessments.

The project covers multiple Nmap scanning techniques including TCP scans, UDP scans, stealth scanning, NSE vulnerability detection, evasion techniques, professional output management, and automation scripting.

---

## Objectives

- Understand advanced Nmap scan types
- Perform UDP service discovery
- Enumerate services using NSE scripts
- Identify potential vulnerabilities
- Apply IDS/Firewall evasion techniques
- Automate scanning workflows
- Generate professional scan outputs

---

## Lab Environment

| System | IP Address |
|--------|------------|
| Kali Linux | 192.168.56.101 |
| Windows Target VM | 192.168.56.105 |

---

## Tools Used

- Nmap
- Kali Linux
- Windows Virtual Machine
- Bash Scripting

---

# Methodology

The project followed a structured reconnaissance methodology:

1. Host Discovery
2. Port Scanning
3. Service Enumeration
4. Vulnerability Detection
5. Evasion Testing
6. Output Documentation
7. Automation Scripting

---

# Advanced Scan Types

## SYN Scan

```bash
sudo nmap -sS 192.168.56.105

```
<img width="940" height="272" alt="image" src="https://github.com/user-attachments/assets/c6d8bebd-10f6-4a94-8678-8109ebb0a2ed" />


### Features
- Stealth scanning
- Half TCP handshake
- Faster scanning
- Lower detection probability

### Observation
The SYN scan generated fewer logs compared to a full TCP Connect scan, making it useful for stealth reconnaissance.

---

## TCP Connect Scan

```bash
nmap -sT 192.168.56.105
```
<img width="940" height="241" alt="image" src="https://github.com/user-attachments/assets/89dac476-336c-46c4-b9fd-d93049073307" />

### Features
- Full TCP connection
- No root privileges required
- Easily detectable by security logs

### Observation
The Windows target logged the full connection attempt, demonstrating how TCP Connect scans are more visible to monitoring systems.

---

## FIN Scan

```bash
sudo nmap -sF 192.168.56.105
```
<img width="940" height="232" alt="image" src="https://github.com/user-attachments/assets/62d111ca-314b-4230-a85d-35f2e4c9450b" />


### Result
Returned:
```text
open|filtered
```

### Observation
Windows systems handle FIN packets differently, causing unreliable FIN scan results.

---

## NULL Scan

```bash
sudo nmap -sN 192.168.56.105
```
<img width="940" height="229" alt="image" src="https://github.com/user-attachments/assets/5543cee3-1d27-4282-9c2a-c256b0025b4c" />

### Features
- No TCP flags set
- Useful for firewall behavior analysis

---

## XMAS Scan

```bash
sudo nmap -sX 192.168.56.105
```
<img width="940" height="226" alt="image" src="https://github.com/user-attachments/assets/bb8c6056-b40d-4c52-92f3-6b75e09b24aa" />

### Features
- FIN + PSH + URG flags enabled
- Used for stealth and firewall testing

---

# Scan Comparison

| Scan Type | Stealth | Speed | Detection Risk | Purpose |
|-----------|----------|-------|----------------|---------|
| SYN Scan | High | Fast | Low | Best reconnaissance scan |
| TCP Connect | Low | Medium | High | Standard connection testing |
| FIN Scan | Medium | Fast | Medium | Firewall testing |
| NULL Scan | Medium | Fast | Medium | Firewall testing |
| XMAS Scan | Medium | Fast | Medium | Firewall testing |

---

# UDP Scanning

UDP scanning helps identify services that do not rely on TCP.

## Targeted UDP Scan

```bash
sudo nmap -sU -p 53,123,161,137,138 192.168.56.105
```
<img width="940" height="352" alt="image" src="https://github.com/user-attachments/assets/267e5c95-83b4-4433-b601-71e8bb7f1fa7" />

## Top UDP Ports Scan

```bash
sudo nmap -sU --top-ports 100 192.168.56.105
```
<img width="940" height="226" alt="image" src="https://github.com/user-attachments/assets/d856e9eb-f8b7-4be7-b92a-5c7cbef1d375" />

---

## UDP Scan Results

| Port | Service | Status |
|------|---------|---------|
| 53 | DNS | Open\|Filtered |
| 123 | NTP | Open\|Filtered |
| 161 | SNMP | Open\|Filtered |
| 137 | NetBIOS | Open\|Filtered |
| 138 | NetBIOS | Open\|Filtered |

---

# NSE Script Enumeration

## SMB Enumeration

```bash
sudo nmap -p 445 --script smb-os-discovery,smb-enum-shares,smb-enum-users 192.168.56.105
```
<img width="784" height="506" alt="image" src="https://github.com/user-attachments/assets/7b9e45c0-006e-4b60-b706-4ac6cb804445" />

<img width="940" height="210" alt="image" src="https://github.com/user-attachments/assets/919ec4a1-80ad-4fe2-a0d8-f6ed00a7cb73" />

### Purpose
- Identify SMB services
- Enumerate shared folders
- Gather user information

---

## RDP Enumeration

```bash
sudo nmap -p 3389 --script rdp-enum-encryption 192.168.56.105
```
<img width="719" height="306" alt="image" src="https://github.com/user-attachments/assets/d38840be-d7c1-44f1-8987-7712c1aec563" />

<img width="940" height="280" alt="image" src="https://github.com/user-attachments/assets/39b8fcea-ae97-4c13-acfa-f5fe0394ce2d" />


### Observation
Firewall filtering prevented complete service identification, indicating defensive security controls were active.

---



# IDS Evasion Techniques

## Packet Fragmentation

```bash
sudo nmap -f 192.168.56.105
```
<img width="940" height="263" alt="image" src="https://github.com/user-attachments/assets/159bf855-cf70-458e-a2af-91fcf89c79e8" />


### Purpose
Fragment packets to evade simple IDS detection systems.

---

## Decoy Scan

```bash
sudo nmap -D 192.168.56.10,192.168.56.20,ME 192.168.56.105
```
<img width="940" height="263" alt="image" src="https://github.com/user-attachments/assets/2b127f33-655e-4bf7-a710-00cc23a71feb" />


### Purpose
Hide the real attacker source among decoy IP addresses.

---

# Timing Templates

| Level | Meaning |
|------|---------|
| T0 | Paranoid |
| T1 | Sneaky |
| T2 | Polite |
| T3 | Normal |
| T4 | Aggressive |
| T5 | Insane |

sudo namp -T4 192.168.52.1

<img width="940" height="460" alt="image" src="https://github.com/user-attachments/assets/0fdf47f9-4d4f-4fdd-bfc1-a4e38794ad71" />

---

# Output Management

Professional penetration testing requires proper result storage.

```bash
sudo nmap -sS -sV -O 192.168.56.105 -oA deep_scan
```
<img width="940" height="221" alt="image" src="https://github.com/user-attachments/assets/a0616f15-a0b2-4a28-ab35-26b91191ac48" />

<img width="940" height="348" alt="image" src="https://github.com/user-attachments/assets/fa9cfafc-ca56-4fa7-89b3-d279f05cbe44" />

<img width="940" height="87" alt="image" src="https://github.com/user-attachments/assets/b3fd0d3d-af36-4f0b-8189-c56ebb55e582" />


### Output Files Generated
- XML Output
- Normal Output
- Grepable Output

---

# Automation Script

```bash
#!/bin/bash

TARGET="192.168.56.105"

echo "[+] Starting Deep Scan..."

sudo nmap -sS -sV -O $TARGET -oA deep_scan

echo "[+] Running Vulnerability Scripts..."

sudo nmap --script vuln $TARGET -oN vuln_scan.txt

echo "[+] Scan Completed."
```
<img width="940" height="482" alt="image" src="https://github.com/user-attachments/assets/9fa45dc2-84a3-488a-b92a-02e5eee3b764" />

<img width="940" height="149" alt="image" src="https://github.com/user-attachments/assets/b873c677-823a-48cb-9c45-af1b9ee41a0d" />

<img width="940" height="144" alt="image" src="https://github.com/user-attachments/assets/0c3d7ebb-b3ae-49cc-8182-e7c6662a5927" />

---

# Learning Outcomes

After completing this project, the following skills were developed:

- Advanced Nmap scanning techniques
- Service enumeration
- Vulnerability assessment
- IDS evasion basics
- Security documentation
- Bash automation scripting
- Professional reconnaissance methodology

---

# Ethical Use Notice

This project was conducted in a controlled virtual lab environment for educational and defensive security purposes only. Unauthorized scanning of public systems is illegal and unethical.

---

# Conclusion

This project demonstrated how advanced Nmap techniques can be used for reconnaissance, service enumeration, vulnerability assessment, and IDS evasion in a controlled environment. Different scan types revealed varying levels of stealth, speed, and detectability, highlighting the importance of selecting the appropriate technique during security assessments.

The project also emphasized the importance of automation, structured documentation, and professional reporting practices in cybersecurity operations.

---


# Author

Vasikaran  
Aspiring soc analyst | Network security
