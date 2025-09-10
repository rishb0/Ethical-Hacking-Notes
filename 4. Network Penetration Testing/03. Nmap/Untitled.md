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


![[Pasted image 20250910140804.png]]