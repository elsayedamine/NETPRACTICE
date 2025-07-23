# 🧭 Routing Tables & Network Routing – Elite Level Reference

---

## 🚀 What is Routing?

Routing is the **process of selecting an optimal path** for data to travel from source to destination across one or more networks.

Routers use **routing tables** to make this decision based on:

- Network destination
- Next-hop (gateway)
- Interface
- Metric/cost

---

## 📋 Anatomy of a Routing Table

| Destination | Netmask   | Gateway     | Interface | Metric |
| ----------- | --------- | ----------- | --------- | ------ |
| 10.0.0.0    | 255.0.0.0 | 10.0.0.1    | eth0      | 1      |
| 0.0.0.0     | 0.0.0.0   | 192.168.1.1 | wlan0     | 10     |

- **Destination**: Target network.
- **Netmask**: Helps determine how many bits define the network.
- **Gateway**: Where to send the packet next.
- **Interface**: Which NIC to use.
- **Metric**: Cost (lower = preferred).

---

## ⚖️ Static vs Dynamic Routing

### 🔒 Static Routing

- Manually configured.
- No adaptation to failures.
- Best for small or secure networks.

### 🔄 Dynamic Routing

- Uses **routing protocols** to learn/update routes.

#### 🔑 Key Protocols:

| Protocol | Type            | Use Case            | Notes                      |
| -------- | --------------- | ------------------- | -------------------------- |
| RIP      | Distance-Vector | Small networks      | Max hop = 15, slow updates |
| OSPF     | Link-State      | Enterprise networks | Uses Dijkstra’s algorithm  |
| BGP      | Path-Vector     | Internet routing    | Between autonomous systems |

---

## 🧠 Routing Algorithm Categories

### 📦 Distance Vector

- Sends entire routing tables.
- Example: RIP

### 🌐 Link State

- Sends updates about immediate neighbors only.
- Example: OSPF, IS-IS
- Uses complete network map for optimal pathing.

### 🧭 Path Vector

- Used in inter-domain routing (e.g., BGP)
- Focuses on policies and path attributes.

---

## 🥇 Route Selection Principles

1. **Longest Prefix Match** (most specific match wins)
2. **Lowest Metric** (cost of the route)
3. **Administrative Distance** (trustworthiness of source)

---

## 🌍 Default Route (Gateway of Last Resort)

- Matches `0.0.0.0/0`
- Used to reach destinations **outside local routing knowledge** (e.g., the Internet)

---

## 🔧 Linux Commands

- Show routing table:

```bash
ip route
netstat -rn
```

- Add static route:

```bash
ip route add 10.10.0.0/16 via 192.168.1.1 dev eth0
```

---

## 🧠 Final Thoughts

Mastering routing means knowing **how packets decide where to go**, how to manipulate that decision, and how to troubleshoot when things go wrong.

> 🏁 You've now completed the **elite networking file series**. This is your arsenal for NetPractice, real-world sysadmin tasks, and beyond.

