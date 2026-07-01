# CTF-3
This is my write-up for the WestWild Edited CTF, done as a lab exercise on Kali against a target VM. I've tried  to keep the steps in the order I actually did them, including a couple of dead ends, instead of just writing a clean  version after the fact. 
# WestWild Edited CTF - Cybersecurity Lab Report

## Overview

This repository contains the complete walkthrough and technical report for the **WestWild Edited CTF** machine. The assessment was performed in a controlled lab environment using **Kali Linux** as the attacker machine against a vulnerable **Ubuntu-based virtual machine**.

The objective was to perform reconnaissance, enumerate exposed services, gain initial access, escalate privileges, and retrieve the available flags.

> **Status:** ✅ Root Access Successfully Obtained

---

## Lab Environment

| Component | Details |
|----------|----------|
| Target Machine | WestWild VM |
| Operating System | Ubuntu 14.04 |
| Attacker Machine | Kali Linux |
| Virtualization | VMware Workstation |
| Network | NAT |
| Target IP | 192.168.207.131 |

---

## Objectives

- Discover the target machine
- Enumerate available services
- Exploit SMB misconfigurations
- Gain SSH access
- Escalate privileges
- Obtain root access
- Capture available flags

---

## Tools Used

- Nmap
- ARP Scan
- Enum4linux
- SMBClient
- SSH
- Linux Command Line
- Base64
- Find

---

## Attack Path

### Phase 1 – Reconnaissance

- Performed ARP scan to discover the target
- Conducted aggressive Nmap scan

Discovered services:

- SSH (22)
- HTTP (80)
- SMB (139,445)

---

### Phase 2 – SMB Enumeration

Using **enum4linux**:

- Anonymous SMB login enabled
- Users discovered:
  - wavex
  - aveng
  - root

---

### Phase 3 – SMB Share Enumeration

Connected anonymously using SMBClient.

Discovered:

- FLAG1.txt
- message_from_aveng.txt

Decoded FLAG1.txt using Base64 to obtain:

- First flag
- SSH credentials

---

### Phase 4 – Initial Access

Logged into the target via SSH using the leaked credentials.

Successfully obtained a shell as:

```

wavex

```

---

### Phase 5 – Privilege Escalation

Performed writable directory enumeration:

```

find / -writable -type d 2>/dev/null

```

Discovered a writable directory containing a script that exposed another set of credentials.

Switched user:

```

su aveng

```

Escalated privileges:

```

sudo su

```

Successfully obtained root access.

---

### Phase 6 – Root Access

Retrieved the second flag from:

```

/root/FLAG2.txt

```

---

## Flags Obtained

### Flag 1

```

Flag1{Welcome_T0_THE-W3ST-W1LD-B0rder}

```

Source:

- Anonymous SMB Share

---

### Flag 2

```

Flag2{Weeeeeeeeeeeellco0o0om_T0_WestWild}

```

Source:

- /root/FLAG2.txt

---

## Key Vulnerabilities

- Anonymous SMB access enabled
- Sensitive information exposed via shared files
- Plaintext credentials stored on the system
- Password reuse across users
- Writable directories exposing privileged information
- Excessive sudo permissions

---

## Skills Demonstrated

- Network Reconnaissance
- Service Enumeration
- SMB Enumeration
- Credential Harvesting
- SSH Access
- Linux Privilege Escalation
- Password Reuse Exploitation
- Post Exploitation
- Documentation

---

## Lessons Learned

This lab demonstrates how poor security practices can lead to complete system compromise without exploiting software vulnerabilities.

Critical security issues included:

- Misconfigured SMB shares
- Credential leakage
- Weak operational security
- Insecure file permissions
- Password reuse

The compromise relied entirely on enumeration and exposed credentials rather than software exploits.

---

## Repository Structure

```

├── README.md
├── Report Cyber CTF3.pdf
├── screenshots/
└── images/

```

---

## Disclaimer

This project was completed in a legal and isolated laboratory environment for educational and cybersecurity training purposes only.

Do not attempt these techniques on systems without explicit authorization.

---

## Author

**Riya Sahani**

MCA Student

Cybersecurity Enthusiast

---

## License

This project is intended for educational purposes only.
