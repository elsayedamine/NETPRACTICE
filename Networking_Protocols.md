# 📡 Networking Protocols – Protocol-Level Mastery for Systems Engineers

---

## 🎯 Why Protocols Matter

Protocols define **how devices agree** to communicate — structure, timing, semantics, and recovery. Mastering them makes you fluent in **packet-level traffic**, debugging tools like **Wireshark**, **Nmap**, and building software that speaks TCP/IP natively.

---

## 🔐 ARP (Address Resolution Protocol)

### 🌍 Layer: Link Layer (L2)

### 🧭 Purpose:
Map **IPv4 addresses to MAC addresses** on a local subnet.

### 📦 Workflow:
1. Host broadcasts an **ARP Request**:
   > “Who has `192.168.1.1`? Tell `192.168.1.100`.”
2. Target host responds **unicast** with its MAC.

### 🛡️ Security:
- ARP Spoofing → causes **MITM attacks**
- Defenses: Dynamic ARP Inspection (DAI), static ARP tables

---

## 🚀 DHCP (Dynamic Host Configuration Protocol)

### 🌍 Layer: Application (L7)

### 🧭 Purpose:
Dynamically assign:
- IP address
- Subnet mask
- Default gateway
- DNS servers

### 🧬 The DORA Lifecycle:

### 🔌 Ports:
- UDP 67 (server)
- UDP 68 (client)

### 🛡️ Vulnerabilities:
- DHCP starvation
- Rogue DHCP servers

---

## 🧩 DNS (Domain Name System)

### 🌍 Layer: Application

### 🧭 Purpose:
Resolve **domain names → IPs**

### 📦 Query types:
- A: IPv4 address
- AAAA: IPv6 address
- MX: Mail server
- TXT: Metadata (used in SPF, DKIM)
- CNAME: Canonical alias
- NS: Authoritative name server

### 🔁 DNS Resolution Chain:
1. Query local cache
2. Ask recursive DNS (e.g. 8.8.8.8)
3. Go to root → TLD (.com) → authoritative DNS

### ⚙️ DNS Tools:
- `dig`, `nslookup`, `host`
- DNSSEC (authenticity & integrity)

---

## 🔀 NAT (Network Address Translation)

### 🌍 Layer: Router-Level (between IP layers)

### 🧭 Purpose:
Translate **private IPs ↔ public IPs**

### 🧪 Types:
| Type       | Description                    |
|------------|--------------------------------|
| Static NAT | 1:1 fixed mapping               |
| Dynamic NAT| Pool-based, IP cycling         |
| PAT (SNAT) | Many-to-one, ports distinguish |

### 🧱 Why NAT?
- IPv4 conservation
- Firewall-like behavior
- Topology hiding

---

## 💣 ICMP (Internet Control Message Protocol)

### 🌍 Layer: Network (L3)

### 🧭 Purpose:
- Diagnostics (ping, traceroute)
- Error signaling (e.g. unreachable, TTL exceeded)

### 🧩 ICMP Packet Types:
| Type | Name               | Use Case          |
|------|--------------------|-------------------|
| 0    | Echo Reply         | ping              |
| 3    | Destination Unreachable | routing error   |
| 5    | Redirect           | better next hop   |
| 8    | Echo Request       | ping              |
| 11   | Time Exceeded      | TTL in traceroute |

### 🛡️ Security Risks:
- ICMP Tunneling
- Ping floods (DoS)
- Best practice: rate-limit or filter ICMP types

---

## 💬 SMTP, POP3, IMAP – Mail Stack

### 📩 SMTP – Simple Mail Transfer Protocol
- Used to **send** email between clients and servers
- Port 25 (legacy), 587 (secure), 465 (SSL)

### 📥 POP3 – Post Office Protocol v3
- Downloads email, then deletes it from server
- Port 110 (insecure), 995 (SSL)

### 📥 IMAP – Internet Message Access Protocol
- Syncs email without deleting from server
- Port 143 (insecure), 993 (SSL)

### 🧠 Modern Mail Servers Use:
- SMTP for sending
- IMAP for retrieving
- TLS or STARTTLS for encryption

---

## 📁 FTP, SFTP, SCP – File Transfer

### 📦 FTP (File Transfer Protocol)
- Control Port: 21
- Data Port: 20
- Modes: Active & Passive
- 🔓 Insecure → use only in private LANs

### 🔐 SFTP (SSH File Transfer Protocol)
- Built on SSH (Port 22)
- Encrypted

### 🔁 SCP (Secure Copy)
- Point-to-point file transfer using SSH
- Ideal for CLI automation

---

## 🌐 HTTP/HTTPS – The Web Backbone

### 📬 HTTP – HyperText Transfer Protocol
- Stateless, clear-text, request/response
- Port 80
- Methods: GET, POST, PUT, DELETE, PATCH, OPTIONS

### 🔒 HTTPS
- HTTP + TLS encryption (Port 443)
- Uses public key encryption, X.509 certs, and symmetric keys

### 🧠 TLS Features:
- Authentication (via certs)
- Confidentiality (AES, ChaCha20)
- Integrity (HMAC)

---

## 🧠 Rare But Powerful Protocols

### 🛰️ IGMP – Internet Group Management Protocol
- Multicast group management
- Used by routers for IPTV

### 📦 SCTP – Stream Control Transmission Protocol
- Supports multihoming, message-based delivery
- Used in telecom signaling (e.g. SS7 over IP)

### 🔐 IPSec
- Encrypts at Layer 3 (IP level)
- Modes: Tunnel (VPNs) and Transport
- Protocols: AH, ESP

### 🧰 SNMP – Simple Network Management Protocol
- Manage network devices remotely
- Ports 161 (query), 162 (trap)
- Versions: v1 (plaintext), v2c, v3 (secure)

---

## 🧠 Final Thoughts

Protocols aren’t just about ports — they’re **philosophies of communication**. Each encapsulates a **trust model**, a **structure**, and a **fail strategy**.

> 🏁 You now command the most battle-tested, surgically sharp protocol knowledge in networking.

> ⏭️ Next: Modes of transmission, casting techniques, full/half duplex — optimized channel control.

