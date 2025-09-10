# Nmap (Network Mapper)

---

## What is Nmap?

*   **Purpose:** Nmap is an open-source utility for network discovery and security auditing. It maps networks by discovering hosts and services.
*   **How it Works:** Sends specially crafted packets to target hosts and analyzes responses to identify hosts, services, operating systems, and firewall types.
*   **Compatibility:** Runs on Linux, Windows, macOS, BSD, Solaris, etc., with command-line and GUI (Zenmap) interfaces.

---

## Key Features

*   Supports advanced techniques including TCP, UDP, ICMP and IP protocol scans.
*   Handles large network scans and single hosts efficiently.
*   Includes Nmap Scripting Engine (NSE) for automated vulnerability detection.
*   Widely used, awarded, and featured in films and publications.

---

## Nmap Interaction with OSI Model Layers

### 1. Network Layer (Layer 3)

*   Sends raw IP packets for host discovery, ping sweeps, and protocol scans.
*   Manipulates IP packets: fragmentation (-f), TTL (--ttl), source IP spoofing (-S).
*   Supports firewall/IDS evasion using decoys (-D), fragmentation, and custom routing.
*   Commands:
    *   `nmap -f 192.168.1.1` (fragmented packets)
    *   `nmap -sO 192.168.1.1` (protocol scan)
    *   `nmap -S 192.168.1.100 192.168.1.1` (IP spoofing)

---
### 2. Transport Layer (Layer 4)

*   Port scanning (TCP & UDP) with various techniques:
    *   TCP SYN scan (-sS), Connect scan (-sT), FIN scan (-sF), Null scan (-sN), Xmas scan (-sX)
    *   UDP scan (-sU)
*   Service and version detection (-sV)
*   Firewall/IDS evasion: scan speed control (--scan-delay, --max-retries)
*   Sample commands:
    *   `nmap -sS 192.168.1.1`
    *   `nmap -sU -p 53 192.168.1.1`
    *   `nmap -sV 192.168.1.1`


![[Pasted image 20250910140804.png]]

## Nmap Commands and Examples

*   Host discovery (ping sweep): `nmap -sn 192.168.1.0/24`
*   Scan single host: `nmap 192.168.1.1`
*   Scan port range: `nmap -p 1-1000 192.168.1.1`
*   Service version identification: `nmap -sV 192.168.1.1`
*   Operating system detection: `nmap -O 192.168.1.1`
*   Use decoy scan for stealth: `nmap -sS -D decoy1,decoy2 192.168.1.1`

---

## Protocol Header Fields Manipulation in Nmap

| Protocol | Header Field | Nmap Usage Description |
| :--- | :--- | :--- |
| IP | TTL | OS detection and hop counting (-O, --ttl) |
| | Flags | Fragmentation and stealth scans (-f) |
| | Source IP | IP spoofing (-S) |
| | Protocol | IP protocol scan (-sO) |
| TCP | Flags | Scan types (SYN, FIN, ACK, etc.) (-sS, -sF, -sA) |
| | Source Port | Spoofing to evade firewalls (--source-port) |
| | Destination Port | Target ports (-p) |
| | Options | Custom TCP packet crafting (--tcp-options) |
| UDP | Source Port | Set source port to bypass filtering (--source-port) |
| | Destination Port | Target UDP services (-p) |
| ICMP | Type | Used in ping and traceroute (Types 0, 3, 8, 11) |
| | Code | Provides additional message info |

---

## TCP Three-Way Handshake in Nmap Scans

*   **SYN:** Client initiates connection, sends initial sequence number.
*   **SYN-ACK:** Server acknowledges and sends its sequence number.
*   **ACK:** Client acknowledges server's sequence, connection established.
*   **Importance:** Ensures reliable communication, sequence tracking for data integrity and filtering evasion.

---
---
