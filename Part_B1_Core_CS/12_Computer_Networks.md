# 12. Computer Networks

> **Part B1 — Core Computer Science** | SIU PET Study Guide

---

- [ ] **OSI Model** (7 Layers)

  | Layer | Name | Function | Protocols/Devices |
  |-------|------|----------|------------------|
  | 7 | Application | User interface | HTTP, FTP, SMTP, DNS, DHCP |
  | 6 | Presentation | Data format, encryption | SSL/TLS, JPEG, MPEG |
  | 5 | Session | Session management | NetBIOS, RPC |
  | 4 | Transport | End-to-end delivery | TCP, UDP |
  | 3 | Network | Routing, logical addressing | IP, ICMP, ARP; Router |
  | 2 | Data Link | Framing, MAC addressing | Ethernet, PPP; Switch, Bridge |
  | 1 | Physical | Bits over medium | Hub, cables, signals |

- [ ] **TCP/IP Model** (4 Layers)
  - Application, Transport, Internet, Network Access

- [ ] **Key Protocols**
  - **TCP**: Connection-oriented, reliable, 3-way handshake (SYN, SYN-ACK, ACK)
  - **UDP**: Connectionless, fast, no guarantees (used in DNS, video streaming)
  - **HTTP/HTTPS**: Web communication; HTTPS = HTTP + TLS
  - **DNS**: Domain → IP resolution
  - **DHCP**: Dynamic IP assignment
  - **ARP**: IP → MAC resolution

- [ ] **IP Addressing**
  - IPv4: 32-bit, dotted decimal (e.g., 192.168.1.1)
  - Classes: A (1-126), B (128-191), C (192-223), D (multicast), E (experimental)
  - **Subnetting**: Subnet mask, CIDR notation (/24)
  - IPv6: 128-bit, hexadecimal notation
  - Private IP ranges: 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16

- [ ] **Routing**
  - Distance vector: RIP (Bellman-Ford based)
  - Link state: OSPF (Dijkstra based)
  - Path vector: BGP (inter-AS routing)
  - Congestion control: slow start, congestion avoidance, fast retransmit

- [ ] **Network Security**
  - Symmetric encryption: AES, DES
  - Asymmetric encryption: RSA, Diffie-Hellman
  - Digital signatures, certificates, PKI
  - Firewalls, VPN, IDS/IPS

---

### Recommended Resources
- **Book**: *Computer Networking: A Top-Down Approach* — Kurose & Ross
- **Book**: *Data Communications and Networking* — Behrouz Forouzan
