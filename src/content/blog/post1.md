---

title: "Lab Network using Cisco Packet Tracer"
description: "Design and simulate a four‐floor Lab network with segmented VLANs, high‐speed trunks, and centralized services using Cisco Packet Tracer."
pubDate: "Jun 08 2025"
heroImage: "/overall.png"
badge: "Networking"
tags: ["networking", "packet-tracer", "vlans", "college-lab"]
--------------------------------------------------------------

# LAB-NETWORK-USING-CISCO-PACKET-TRACER

## 📖 Table of Contents

1. [Project Overview](#project-overview)
2. [Network Topology](#network-topology)
3. [Floor-by-Floor Breakdown](#floor-by-floor-breakdown)
4. [IP & VLAN Schema](#ip--vlan-schema)
5. [Key Components](#key-components)
6. [Data Flow](#data-flow)
7. [Images](#images)
8. [Security & Manageability](#security--manageability)
9. [Benefits](#benefits)
10. [Getting Started](#getting-started)

---

## 🚀 Project Overview

Simulate and document a **four‐story college building** network in Cisco Packet Tracer. Each of the first three floors hosts an Admin office and two student labs; the fourth floor adds a dedicated Server Room with file, authentication, backup, and storage servers. All floor switches connect via 1 Gbps trunks to a core switch/router, ensuring high throughput, segmentation, and centralized management.

**Goal:** Deliver a scalable, secure, and easily maintainable campus‐style network supporting staff, students, and services.

---

## 🌐 Network Topology

```
                              ┌─────────────────┐  
                              │    Internet     │  
                              └─────────────────┘  
                                       ↓         
                               ┌───────────────┐  
                               │ Core Router   │  
                               └───────────────┘  
                                       ↕         
                               ┌───────────────┐  
                               │ Core Switch   │  
                               └───────────────┘  
             ┌──────┬──────────┴──────────┬──────┐
             │      │                     │      │
         Floor 1  Floor 2              Floor 3  Floor 4
       Switches Switches            Switches   Switches
        (Admin & (Admin &            (Admin &   + Server
         Labs A/B) Labs A/B)          Labs A/B)   Room)
```

---

## 🏢 Floor-by-Floor Breakdown

### Floors 1–3

* **Admin Office Switch**

  * 2–4 staff PCs (ports Fa0/1–Fa0/4)
  * Shared office printer (Fa0/5)
  * VLAN 10 “Admin”

* **Lab Switch A (VLAN 20) & Lab Switch B (VLAN 20)**

  * 15–20 student PCs each (ports Fa0/1–Fa0/20)
  * Lab printer (Fa0/21)
  * Uplink to Floor switch as trunk (Gi0/24)

### Floor 4

* **Admin Office & Labs** (as above)
* **Server‐Room Switch**

  * File Server (Gi0/1) – VLAN 30
  * Authentication Server (Gi0/2) – VLAN 30
  * Backup Server (Gi0/3) – VLAN 30
  * NAS Storage Appliance (Gi0/4) – VLAN 30
  * Trunk to Core Switch (Gi0/24)

---

## 🗺️ IP & VLAN Schema

| VLAN ID | Name       | Subnet           | Gateway      |
| ------- | ---------- | ---------------- | ------------ |
| 10      | Admin      | 192.168.10.0 /24 | 192.168.10.1 |
| 20      | StudentLab | 192.168.20.0 /24 | 192.168.20.1 |
| 30      | Servers    | 192.168.30.0 /24 | 192.168.30.1 |

* **Trunk ports** carry VLAN 10, 20, 30 with 802.1Q tagging.
* **Core Router** interface Fa0/0 sub‐interfaces configured for each VLAN.

---

## 🔧 Key Components

| Component               | Role                                                           |
| ----------------------- | -------------------------------------------------------------- |
| **Core Router**         | Inter‐VLAN routing & Internet gateway                          |
| **Core Switch**         | Central distribution—1 Gbps fiber uplinks to each floor switch |
| **Floor Switches**      | Aggregation for Admin & Labs; trunks to Core Switch            |
| **Server‐Room Switch**  | Dedicated VLAN 30 hub for all servers                          |
| **Cisco Packet Tracer** | Simulation & configuration testing                             |
| **Servers & NAS**       | File, auth, backup, and storage services                       |

---

## 🔄 Data Flow

1. **Local Print Job** (Lab PC → Lab Printer)
   Stays within same switch, VLAN 20.

2. **Cross-Floor File Access**
   Lab PC → Lab Switch → Floor Switch → Core Switch → Floor 4 Switch → File Server.

3. **Internet Browsing**
   PC → Floor Switch → Core Switch → Core Router → Internet.

---

## 🖼️ Images

**Overall Topology**  
![Overall Network](/overall.png)

**Floor 1 Layout**  
![Floor 1](/f1.png)

**Floor 2 & 3 Layout**  
![Floor 2 & 3](/f23.png)

**Floor 4 & Server Room**  
![Floor 4](/f4.png)

**Floor Router**  
![Floor Router](/rou.png)

---

## 🔒 Security & Manageability

* **VLAN Segmentation:** Keeps admin, student, and server traffic isolated.
* **Port Security:** Limits MAC addresses on access ports to prevent spoofing.
* **ACLs & Firewall:** Core Router applies ACLs to block unauthorized VLAN 30 access.
* **STP Root Bridge:** Core Switch is root to prevent loops.
* **Monitoring:** SNMP & NetFlow on Core for traffic analysis.
* **Redundancy:** Dual uplinks on critical switches; STP ensures failover.

---

## 🎯 Benefits

* **Scalable Architecture:** Add floors or labs by extending VLANs and trunks.
* **Fault Isolation:** VLAN-based segmentation prevents broadcast storms from spreading.
* **High Performance:** 1 Gbps+ trunks avoid bottlenecks during peak usage.
* **Centralized Services:** Servers consolidated on VLAN 30, simplifying backups and security policies.

---

## 🛠️ Getting Started

1. **Clone the repository**

   ```bash
   git clone https://github.com/Abhinav-1524/LAB-NETWORK-USING-CISCO-PACKET-TRACER.git
   cd LAB-NETWORK-USING-CISCO-PACKET-TRACER
   ```

2. **Open Packet Tracer file**

   * `network_topology.pkt` in the root directory.

3. **Review configurations**

   * `/docs/configs/` for CLI scripts and switch/router setups.

4. **Simulate & Test**

   * Verify VLANs, trunking, inter-VLAN routing, and server access.

5. **Customize**

   * Adjust VLAN IDs, IP subnets, or add new services as needed.
