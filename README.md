# Enterprise Network Architecture & Security Lab

<p align="center">
 <em>**** A comprehensive Cisco Packet Tracer simulation of a secure, multi-branch enterprise network. ****</em><br/>
 <em> "This project was created as a practice exercise to strengthen my networking skills in preparation for the CCNA certification. As such, it may contain certain limitations or inaccuracies and should be considered for reference purposes only."</em>
 <br/><br/>
 <img src="https://github.com/YShin044/Basic_Multi-Branch-LogicalNetwork/blob/master/assets/Topology.jpg" alt="Full Network Topology">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Cisco%20Packet%20Tracer-1BA0D7?style=for-the-badge&logo=cisco&logoColor=white" alt="Packet Tracer"/>
  <img src="https://img.shields.io/badge/TCP/IP-000000?style=for-the-badge" alt="TCP/IP"/>
  <img src="https://img.shields.io/badge/EIGRP-ED1C24?style=for-the-badge" alt="EIGRP"/>
  <img src="https://img.shields.io/badge/HSRP-4A90E2?style=for-the-badge" alt="HSRP"/>
  <img src="https://img.shields.io/badge/VLAN-8A2BE2?style=for-the-badge" alt="VLAN"/>
  <img src="https://img.shields.io/badge/Cisco%20ASA-ED1C24?style=for-the-badge&logo=cisco&logoColor=white" alt="Cisco ASA"/>
  <img src="https://img.shields.io/badge/IPSec%20VPN-0059B3?style=for-the-badge" alt="IPSec VPN"/>
</p>

---

## 🎯 Project Objective

This project simulates a scalable and secure enterprise network architecture for a company with a main headquarters and multiple remote branches. It reflects real-world IT infrastructure used in small to medium-sized businesses (SMBs), incorporating essential elements that an IT Helpdesk or Network Administrator may encounter.

Key objectives include:
- Enhancing network segmentation and security via VLANs, ACLs, and firewall zones.
- Implementing centralized services (DHCP, DNS) with redundancy (HSRP, EtherChannel).
- Demonstrating inter-site connectivity via WAN and site-to-site VPNs.
- Applying CCNA-level concepts in a practical simulation environment.

---

## 👨‍💻 My Role

I independently designed and implemented the entire network topology using Cisco Packet Tracer, including:
- IP subnetting and VLAN planning for multiple departments.
- Configuring Cisco routers, Layer 2/3 switches, and ASA firewall.
- Deploying DHCP relay, DNS, ACLs, NAT, and static/dynamic routing (EIGRP).
- Testing communication between departments, zones, and across WAN links.
- Documenting the architecture and producing a test plan for validation.

---

## ► Project Overview

This topology demonstrates a hierarchical, multi-zone security architecture with centralized services and WAN connectivity.

### Key Architectural Features:
- **Hierarchical Design:** The HQ network follows the 3-tier model (Core, Distribution, Access).
- **Multi-Zone Security:** ASA Firewall segments traffic into `inside`, `dmz`, `outside`, and `branch` zones.
- **Redundancy:** Implemented using HSRP for gateway failover and EtherChannel (LACP) for aggregated links.
- **Routing:** EIGRP for dynamic WAN routing, static routes for firewall zone control.
- **Centralized Services:** DHCP and DNS centrally hosted and served using `ip helper-address`.

---

## ► Network Segmentation & IP Schema

### 📍 Headquarters (District 7 - `inside` Zone)
- **Core Gateway:** `CoreSW` (L3 Switch) + HSRP (Virtual IP `.254`)
- **VLANs:**
  - VLAN 10: Marketing – `192.168.10.0/24`
  - VLAN 11: Sales – `192.168.11.0/24`
  - VLAN 12: Wireless (APs) – `192.168.12.0/24`
  - VLAN 20: Accounting – `192.168.20.0/24`
  - VLAN 30: Technical – `192.168.30.0/24`
  - VLAN 44: IT Admin – `192.168.44.0/24`
  - VLAN 55: Internal Services – `192.168.55.0/24`
  - VLAN 99: Transit to ASA – `192.168.1.0/24`

### 🛡️ DMZ (Demilitarized Zone)
- Gateway: ASA0 – `192.168.100.254`
- Network: `192.168.100.0/24`
- Services: Web Server (`.10`), Email Server (`.20`)

### 🌍 WAN & Remote Site (`outside` Zone)
- Routing: EIGRP (AS 100) with static redistribution
- Networks:
  - Remote LAN: `192.168.200.0/24`
  - WAN Links: `10.0.0.0/30`, `10.0.0.4/30`
  - ASA Transit: `172.16.0.0/30`

### 🏢 Branch Office (District 9)
- VLANs:
  - VLAN 10: Accounting
  - VLAN 20: Human Resources
  - VLAN 30: Technical
  - VLAN 40: Server Zone

---

## ► Technologies & Concepts Implemented

| Layer 2                        | Layer 3                              | Security & Services                      |
|-------------------------------|--------------------------------------|------------------------------------------|
| VLANs & 802.1Q Trunking       | Inter-VLAN Routing (SVI)             | Cisco ASA Firewall (Zone-based)          |
| EtherChannel (LACP)           | Static Routing & EIGRP               | ACLs for zone filtering                  |
| Spanning Tree Protocol (STP)  | HSRP for Gateway Redundancy          | DHCP Relay via `ip helper-address`       |
|                               | WAN site-to-site VPN                 | Stateful inspection & NAT                |
|                               |                                      | SSH for remote device management         |

---

## 🧪 How to Run and Test This Simulation

### Requirements:
- Cisco Packet Tracer **v8.x or later**
- File: `Basic_Multi-Branch-LogicalNetwork.pkt`

### Steps:
1. Open the `.pkt` file in Packet Tracer.
2. Power on all devices (if powered off).
3. Use CLI to explore configurations (`enable → show run`).
4. Run the following tests:

#### Internal Communication:
- `Ping` between VLAN 10 (PC0) and VLAN 20 (PC2)
- DHCP assignment verification on PCs

#### DMZ Access:
- On PC0, open Web Browser → access: `http://192.168.100.10`
- Ping Email Server at `192.168.100.20`

#### Remote Connectivity:
- `Ping` from PC0 (HQ) to PC5 (Remote Site) – `192.168.200.10`
- Verify VPN tunnel via `show crypto` on ASA (if configured)

#### Redundancy Test (Optional):
- Shut down one of the HSRP routers and confirm gateway continuity via `show standby`

---

## 🛠️ Skills Demonstrated

- Enterprise network architecture design
- VLAN and subnetting strategies
- DHCP/DNS relay and centralization
- Cisco ASA firewall configuration
- WAN routing and VPN site-to-site
- High availability and link aggregation
- Troubleshooting via ping, traceroute, and ACL review

---

## 📚 Useful For

- CCNA Lab Practice  
- Entry-level Network Admin / IT Helpdesk Portfolio  
- Training & Documentation Reference  

---

<p align="center">
  <em>"This project was created as a practice exercise to strengthen my networking skills in preparation for the CCNA certification. As such, it may contain certain limitations or inaccuracies and should be considered for reference purposes only."</em>
</p>
