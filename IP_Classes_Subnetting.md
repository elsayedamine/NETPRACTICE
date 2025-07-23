# 🧮 IP Addressing, CIDR & Subnetting – Systems-Level Deep Dive

---

## 📌 Context & Significance

IPv4 utilizes **32-bit addresses**, split into **network** and **host** components. Efficient allocation of this space is central to:

- 🔄 **Scalability** in IPv4-era networks  
- 🔍 **Routing optimization** and aggregation  
- 🔒 **Security segmentation** of subnets  

### 👇 Why CIDR + VLSM Changed Everything

- **CIDR** (Classless Inter-Domain Routing) introduces **prefix-length** (e.g., `/24`), replacing rigid classful A/B/C models and enabling route aggregation ([turn0search0],[turn0search17]).  
- **VLSM** (Variable-Length Subnet Masking) allows **subdividing a single IP block into multiple sized subnets**, aligning address space precisely with need ([turn0search1],[turn0search15]).

This combo mitigates IPv4 exhaustion and drastically improves routing table efficiency.

---

## 1️⃣ Classful Addressing (Legacy Overview)

| Class | Leading Bits | Range                      | Default Mask | Hosts      |
|-------|--------------|----------------------------|--------------|------------|
| A     | 0            | 1.0.0.0 – 126.255.255.255  | `/8`         | ~16 million |
| B     | 10           | 128.0.0.0 – 191.255.255.255| `/16`        | ~65 thousand |
| C     | 110          | 192.0.0.0 – 223.255.255.255| `/24`        | 254        |

Rigid blocks led to massive address waste — hence the need for classless design.

---

## 2️⃣ CIDR Notation Essentials

- Represents addresses like `192.168.1.0/24` → first 24 bits are **network prefix**, 8 bits for hosts.  
- Enables **supernetting** (route summarization), like merging contiguous blocks into single advertisements — reducing global routing table size ([turn0search17],[turn0search0]).

---

## 3️⃣ FLSM vs VLSM – Strategic Trade-offs

- **FLSM**: All subnets use the same mask — easier but wasteful.  
- **VLSM**: Subnets use different masks scaled to host count — efficient, but more complex to plan & require classless routing (e.g., OSPF, BGP, RIPv2) ([turn0search1],[turn0search15]).

---

## 4️⃣ VLSM Design Workflow

1. **List host groups**, descending by size.
2. **Choose smallest prefix** covering required hosts (+2 addresses) — `/h` where `2^(32−h) ≥ hosts + 2`.
3. **Allocate subnets sequentially**, avoiding overlaps.
4. **Configure routers** with correct masks/routes.
5. **Use compatible routing protocols** (OSPF, EIGRP, RIPv2) ([turn0search15],[turn0search2]).

### 📊 Example Case

Requirement groups: 120, 60, 30, 5 hosts:

- /25 → 128‑2 = 126 usable (for 120 hosts)  
- /26 → 64‑2 = 62 usable (for 60 hosts)  
- /27 → 32‑2 = 30 usable (for 30 hosts)  
- /29 → 8‑2 = 6 usable (for 5 hosts)

Efficient use of the remaining space for growth or other needs.

---

## 5️⃣ Binary Math & Mask Tables

Subnet mask bits: network=1s, host=0s.

- **Hosts/Subnet** = 2^(host_bits) − 2  
- **Subnets** = 2^(borrowed_bits)

| Prefix | Mask Decimal         | Total Addr | Usable Hosts |
|--------|----------------------|------------|---------------|
| /24    | 255.255.255.0        | 256        | 254           |
| /25    | 255.255.255.128      | 128        | 126           |
| /26    | 255.255.255.192      | 64         | 62            |
| /27    | 255.255.255.224      | 32         | 30            |
| /28    | 255.255.255.240      | 16         | 14            |
| /29    | 255.255.255.248      | 8          | 6             |
| /30    | 255.255.255.252      | 4          | 2             |

---

## 6️⃣ Route Aggregation Techniques

Combine multiple subnets into a larger summary route:

- E.g., Use `/23` to represent both `.0/24` and `.1/24` blocks.  
- Impact: fewer routing entries, faster routing convergence ([turn0search17]).

⚠️ **Caution**: Misalignment or overlapping subnets may cause routing ambiguity or leakage.

---

## 7️⃣ Advanced VLSM: Real-World Examples

- **Stacked subnets**: hierarchy → large LAN → smaller VLANs → /30 links → loopbacks.  
- **WAN links** often use `/30`, `/31`, or `/32` for point-to-point efficiency ([turn0search6]).

### Rich Use Cases:

- **Loopback interfaces** use `/32`.  
- **Point-to-point** routers often use `/31`, `/30`.  
- **VLANs for small subnets** (e.g., /28 to /27).  
- **Supernets** in ISP backbones reduce table size.

---

## 🔐 Security & Stability Considerations

- Avoid **discontiguous networks**: break VLSM allocations across routers → routing intricacies.  
- Gnarly overlapping may lead to unreachable hosts.  
- Enforce **classless routing protocols** — classful ones (like original RIP v1) ignore masks.

---

## 📌 Final Summary

- 🧠 **CIDR** + **VLSM** = precision IP architecture.  
- Efficiency: dramatically lower IP waste and improved XOR-level aggregation.  
- Scale: suitable for both enterprise LANs and ISP-level routing.  
- Real-World: supports IPv4’s lifespan while preparing the foundation for IPv6.

---
