# 12. Computer Networks

> **Part B1 — Core Computer Science** | SIU PET Complete Study Guide

---

## 12.1 Network Models

### OSI Model (7 Layers)

The **Open Systems Interconnection** model is a conceptual framework that standardizes how different systems communicate.

| Layer | Name | Function | PDU | Key Protocols/Devices |
|-------|------|----------|-----|----------------------|
| 7 | **Application** | User-facing services | Data | HTTP, FTP, SMTP, DNS, DHCP, SSH |
| 6 | **Presentation** | Data format, encryption, compression | Data | SSL/TLS, JPEG, MPEG, ASCII, Unicode |
| 5 | **Session** | Session management, dialog control | Data | NetBIOS, RPC, SIP |
| 4 | **Transport** | End-to-end delivery, reliability | Segment | TCP, UDP; **Port numbers** |
| 3 | **Network** | Routing, logical addressing | Packet | IP, ICMP, ARP, OSPF; **Router** |
| 2 | **Data Link** | Framing, MAC addressing, error detection | Frame | Ethernet, WiFi, PPP; **Switch, Bridge** |
| 1 | **Physical** | Bits over physical medium | Bits | Cables, Hubs, signals, frequencies |

**Mnemonic (top-down):** "**A**ll **P**eople **S**eem **T**o **N**eed **D**ata **P**rocessing"

### TCP/IP Model (4 Layers)

| TCP/IP Layer | OSI Equivalent | Key Protocols |
|-------------|---------------|---------------|
| **Application** | Application + Presentation + Session | HTTP, DNS, FTP, SMTP, SSH |
| **Transport** | Transport | TCP, UDP |
| **Internet** | Network | IP, ICMP, ARP |
| **Network Access** | Data Link + Physical | Ethernet, WiFi, MAC |

### How Data Flows Through Layers

```
Sender                                          Receiver
Application: [DATA]                        Application: [DATA]
Transport:   [TCP HDR][DATA]               Transport:   [TCP HDR][DATA]
Network:     [IP HDR][TCP HDR][DATA]       Network:     [IP HDR][TCP HDR][DATA]
Data Link:   [ETH][IP HDR][TCP][DATA][FCS] Data Link:   [ETH][IP HDR][TCP][DATA][FCS]
Physical:    10110011101001010...           Physical:    10110011101001010...
                     ↓                                          ↑
            ════════ NETWORK MEDIUM ════════════════════════════
```

Each layer adds its header (encapsulation) going down; removes it (decapsulation) going up.

---

## 12.2 Key Protocols

### TCP (Transmission Control Protocol)

**Connection-oriented, reliable, ordered delivery.**

**Three-Way Handshake (connection establishment):**
```
Client               Server
  │                     │
  │──── SYN ──────────→│  Step 1: Client sends SYN (seq=x)
  │                     │
  │←── SYN-ACK ────────│  Step 2: Server replies SYN-ACK (seq=y, ack=x+1)
  │                     │
  │──── ACK ──────────→│  Step 3: Client sends ACK (ack=y+1)
  │                     │
  │   Connection established
```

**Four-Way Termination:**
```
Client               Server
  │──── FIN ──────────→│  Step 1: Client wants to close
  │←── ACK ────────────│  Step 2: Server acknowledges
  │←── FIN ────────────│  Step 3: Server also wants to close
  │──── ACK ──────────→│  Step 4: Client acknowledges
```

**Features:** Reliability (ACK + retransmission), flow control (sliding window), congestion control, ordered delivery.

### UDP (User Datagram Protocol)

**Connectionless, unreliable, fast.**

| Feature | TCP | UDP |
|---------|-----|-----|
| Connection | Connection-oriented | Connectionless |
| Reliability | Guaranteed delivery | Best-effort |
| Ordering | Ordered | No ordering |
| Speed | Slower (overhead) | Faster |
| Header size | 20 bytes | 8 bytes |
| Use cases | Web, email, file transfer | DNS, video streaming, gaming, VoIP |

### HTTP / HTTPS

- **HTTP (Hypertext Transfer Protocol):** Application layer protocol for web communication
  - Methods: GET, POST, PUT, DELETE, PATCH
  - Status codes: 200 (OK), 301 (Redirect), 404 (Not Found), 500 (Server Error)
- **HTTPS:** HTTP + TLS encryption (port 443 instead of 80)

### DNS (Domain Name System)

Translates human-readable domain names to IP addresses.

```
Browser: "www.google.com" → ?
    │
    ↓
Local DNS Cache → miss
    │
    ↓
Recursive Resolver → Root Server (.com)
    │                     │
    │                     ↓
    │            TLD Server (google.com) → Authoritative Server
    │                                           │
    │←──────── IP: 142.250.192.78 ─────────────┘
```

- Uses UDP port 53 (small queries), TCP for zone transfers
- **Record types:** A (IPv4), AAAA (IPv6), CNAME (alias), MX (mail), NS (nameserver)

### DHCP (Dynamic Host Configuration Protocol)

Automatically assigns IP addresses to devices on a network.

**DORA Process:**
1. **Discover:** Client broadcasts "I need an IP"
2. **Offer:** DHCP server offers an IP
3. **Request:** Client accepts the offer
4. **ACK:** Server confirms the assignment

### ARP (Address Resolution Protocol)

Resolves IP addresses to MAC addresses (Layer 3 → Layer 2).
- "Who has IP 192.168.1.5? Tell 192.168.1.1"
- The device with that IP replies with its MAC address

---

## 12.3 IP Addressing

### IPv4

**Format:** 32-bit address, written in dotted decimal: `192.168.1.100`
**Total addresses:** 2³² ≈ 4.3 billion

### Classful Addressing

| Class | Range | Default Mask | Networks | Hosts/Network |
|-------|-------|-------------|---------|---------------|
| **A** | 1.0.0.0 – 126.255.255.255 | 255.0.0.0 (/8) | 126 | ~16.7 million |
| **B** | 128.0.0.0 – 191.255.255.255 | 255.255.0.0 (/16) | ~16,000 | ~65,000 |
| **C** | 192.0.0.0 – 223.255.255.255 | 255.255.255.0 (/24) | ~2 million | 254 |
| **D** | 224.0.0.0 – 239.255.255.255 | — | Multicast | — |
| **E** | 240.0.0.0 – 255.255.255.255 | — | Experimental | — |

**Special addresses:**
- 127.0.0.1: Loopback (localhost)
- 0.0.0.0: Default route / "this network"
- 255.255.255.255: Broadcast

### Private IP Ranges (Not routable on the Internet)

| Range | Class | CIDR |
|-------|-------|------|
| 10.0.0.0 – 10.255.255.255 | A | 10.0.0.0/8 |
| 172.16.0.0 – 172.31.255.255 | B | 172.16.0.0/12 |
| 192.168.0.0 – 192.168.255.255 | C | 192.168.0.0/16 |

### Subnetting

Divides a network into smaller sub-networks.

**CIDR Notation:** IP/prefix-length (e.g., 192.168.1.0/26)

**Example:**
> Given: 192.168.1.0/26
> Subnet mask: 255.255.255.192 (26 bits for network, 6 bits for host)
> Number of hosts: 2⁶ − 2 = **62** usable hosts per subnet
> Number of subnets: depends on original class

### IPv6

- **128-bit** address: `2001:0db8:85a3:0000:0000:8a2e:0370:7334`
- Practically unlimited addresses: 2¹²⁸ ≈ 3.4 × 10³⁸
- No broadcast (uses multicast instead)
- Built-in IPsec (security)
- Simplified header

---

## 12.4 Routing

### Routing Types

| Type | Algorithm | Protocol | Scope |
|------|-----------|----------|-------|
| **Distance Vector** | Bellman-Ford | RIP | Intra-AS (within organization) |
| **Link State** | Dijkstra | OSPF | Intra-AS |
| **Path Vector** | — | BGP | Inter-AS (between organizations / ISPs) |

**Distance Vector (RIP):**
- Each router knows the distance (hops) to every destination
- Periodically shares routing table with neighbors
- **Problem:** Count-to-infinity (slow convergence)
- Max hop count: 15 (RIP limitation)

**Link State (OSPF):**
- Each router knows the ENTIRE network topology
- Uses Dijkstra's algorithm to compute shortest paths
- Faster convergence, more scalable
- Used in large enterprise networks

**BGP (Border Gateway Protocol):**
- Routes traffic between Autonomous Systems (ASes) — the "backbone" of the Internet
- Policy-based routing (not just shortest path)

### TCP Congestion Control

Prevents network congestion by controlling the sender's rate.

| Phase | Mechanism | Behavior |
|-------|-----------|----------|
| **Slow Start** | Window size doubles every RTT | Exponential growth |
| **Congestion Avoidance** | Window increases by 1 per RTT (after threshold) | Linear growth |
| **Fast Retransmit** | Retransmit on 3 duplicate ACKs (don't wait for timeout) | Quick recovery |
| **Fast Recovery** | Halve the congestion window, don't go to slow start | Avoid drastic slowdown |

---

## 12.5 Network Security

### Encryption Types

| Type | Key | Speed | Use Case | Examples |
|------|-----|-------|----------|---------|
| **Symmetric** | Same key for encrypt + decrypt | Fast | Bulk data encryption | AES, DES, 3DES |
| **Asymmetric** | Public key (encrypt) + Private key (decrypt) | Slow | Key exchange, digital signatures | RSA, ECC, Diffie-Hellman |

**How HTTPS Works (simplified):**
1. Client connects to server on port 443
2. Server sends its **digital certificate** (with public key)
3. Client verifies certificate with a trusted CA (Certificate Authority)
4. Client generates a random **session key** and encrypts it with the server's public key
5. Server decrypts with its private key → both have the session key
6. All subsequent communication uses symmetric encryption (AES) with the session key

### Security Concepts

| Concept | Description |
|---------|-------------|
| **Digital Signature** | Encrypt hash of message with sender's private key → proves authenticity |
| **Digital Certificate** | Server's identity + public key, signed by a Certificate Authority (CA) |
| **PKI** | Public Key Infrastructure — the system of CAs and certificates |
| **Firewall** | Filters traffic based on rules (allow/block by IP, port, protocol) |
| **VPN** | Virtual Private Network — encrypted tunnel over the Internet |
| **IDS/IPS** | Intrusion Detection/Prevention System — monitors and blocks attacks |

---

## 12.6 Network Devices

| Device | Layer | Function |
|--------|-------|----------|
| **Hub** | 1 (Physical) | Broadcasts data to all ports (dumb) |
| **Switch** | 2 (Data Link) | Forwards data to specific port using MAC address table |
| **Router** | 3 (Network) | Routes packets between networks using IP addresses |
| **Gateway** | 7 (Application) | Connects networks with different protocols |
| **Modem** | 1-2 | Converts digital ↔ analog signals |

---

## 12.7 Practice Questions

**Q1.** Explain the three-way handshake in TCP. Why is it necessary?
> **Answer:** (1) Client sends SYN with sequence number x. (2) Server replies with SYN-ACK containing its own sequence number y and acknowledgment x+1. (3) Client sends ACK with acknowledgment y+1. It's necessary to **synchronize sequence numbers** between both sides, confirm both can send and receive, and establish a reliable connection before data transfer begins.

**Q2.** Given the IP address 192.168.10.0/28, how many usable host addresses are available?
> **Answer:** /28 means 28 bits for network, 4 bits for hosts. Total hosts = 2⁴ = 16. Usable = 16 − 2 = **14** (subtract network address and broadcast address).

**Q3.** What is the difference between a switch and a router?
> **Answer:** A **switch** operates at Layer 2 (Data Link), uses MAC addresses to forward frames within the same network (LAN). A **router** operates at Layer 3 (Network), uses IP addresses to forward packets between different networks. A switch can't route traffic between subnets; a router can.

**Q4.** Why does DNS primarily use UDP instead of TCP?
> **Answer:** DNS queries are typically small (fit in one UDP datagram) and need to be fast. UDP's connectionless nature avoids the overhead of TCP's three-way handshake. For a simple DNS query-response, UDP's single request + single reply is much faster. However, DNS uses TCP for zone transfers (large data) and responses exceeding 512 bytes.

**Q5.** Explain the difference between symmetric and asymmetric encryption. Why does HTTPS use both?
> **Answer:** **Symmetric:** Same key for encryption and decryption — fast but requires secure key exchange. **Asymmetric:** Different keys (public/private) — slow but solves key distribution problem. HTTPS uses **both** in a hybrid approach: asymmetric encryption (RSA) for the initial key exchange (securely sharing a session key), then symmetric encryption (AES) for the actual data transfer (because it's much faster). This gives both security and performance.

---

*Previous: [Chapter 11 — Operating Systems](11_Operating_Systems.md) | Next: [Chapter 13 — Theory of Computation](13_Theory_of_Computation.md)*
