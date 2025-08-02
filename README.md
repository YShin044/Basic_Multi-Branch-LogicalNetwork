# Enterprise Network Architecture & Security Lab

<p align="center">
  <em>"This project was created as a practice exercise to strengthen my networking skills in preparation for the CCNA certification. As such, it may contain certain limitations or inaccuracies and should be considered for reference purposes only."</em>
  <br/><br/>
  <img src="https://github.com/YShin044/Basic_Multi-Branch-LogicalNetwork/blob/master/assets/Topology.jpg" alt="Full Network Topology">
</p>

## ► Project Overview

This project simulates a robust and scalable network infrastructure for a corporation with a main headquarters (HQ) and multiple remote branches. Designed and implemented entirely within **Cisco Packet Tracer**, this topology showcases a hierarchical and multi-zone security architecture.

The core design principles are **security, redundancy, and scalability**, applying a wide range of networking concepts to create a resilient and manageable enterprise environment.

### Key Architectural Features:
- **Hierarchical Design:** The HQ network utilizes the 3-layer model (Core, Distribution, Access) for efficient traffic flow and scalability.
- **Multi-Zone Security:** A central **Cisco ASA Firewall** segments the network into distinct security zones: `inside` (HQ), `dmz` (Public Services), `outside` (WAN), and a separate zone for the District 9 branch.
- **High Availability (HA):** Redundancy is engineered at multiple layers, including **HSRP** for default gateway failover and **EtherChannel (LACP)** for link aggregation between Core and Distribution switches.
- **Hybrid Routing Strategy:** **EIGRP** is deployed for dynamic routing across the WAN, while **Static Routing** is used to enforce controlled traffic paths through the firewall.
- **Centralized Services:** Key network services like **DHCP** and **DNS** are centralized and served to multiple VLANs using the `ip helper-address` command.

---

## ► Network Segmentation & IP Schema

The network is logically segmented into VLANs and security zones, each with a dedicated IP subnet.

### 📍 Headquarters (District 7 - `inside` Zone)
*   **Core Device & Gateway:** `CoreSW` (L3 Switch) with HSRP for gateway redundancy (Virtual IP: `.254`).
*   **VLANs & Departments:**
    - **VLAN 10 (`192.168.10.0/24`):** Marketing Department
    - **VLAN 11 (`192.168.11.0/24`):** Sales Department
    - **VLAN 12 (`192.168.12.0/24`):** Wireless Access (APs)
    - **VLAN 20 (`192.168.20.0/24`):** Accounting Department (Ke_Toan)
    - **VLAN 30 (`192.168.30.0/24`):** Technical Department (Ki_Thuat)
    - **VLAN 44 (`192.168.44.0/24`):** IT Administration (ADMIN)
    - **VLAN 55 (`192.168.55.0/24`):** Internal Services (DHCP/DNS Servers)
    - **VLAN 99 (`192.168.1.0/24`):** Transit Link to ASA Firewall

### 🛡️ DMZ (Demilitarized Zone)
*   **Gateway:** `ASA0` Firewall (`192.168.100.254`).
*   **Network:** `192.168.100.0/24`
*   **Services:** Web Server (`.10`), Email Server (`.20`).

### 🌍 WAN & Remote Site (`outside` Zone)
*   **Routing Protocol:** EIGRP (AS 100) with `redistribute static` on `Router0`.
*   **Networks:**
    - **Remote LAN:** `192.168.200.0/24`
    - **WAN Links:** `10.0.0.0/30`, `10.0.0.4/30`
    - **Transit Link (ASA-Router0):** `172.16.0.0/30`

### 🏢 Branch Office (District 9)
*   *(Note: This branch is depicted in the topology but its integration requires connecting it to a dedicated ASA interface and configuring relevant security policies and routes.)*
*   **VLANs defined:**
    - **VLAN 10:** Accounting (Ke_Toan)
    - **VLAN 20:** Human Resources (HR)
    - **VLAN 30:** Technical (Ki_Thuat)
    - **VLAN 40:** Server Zone

---

## ► Core Technologies & CCNA Concepts Implemented

This project is a practical application of key concepts from the CCNA curriculum and beyond.

<table>
  <tr>
    <td valign="top" width="33%">
      <h4>Layer 2 Technologies</h4>
      <ul>
        <li><b>VLANs & 802.1Q Trunking:</b> Network segmentation for security and broadcast domain reduction.</li>
        <li><b>EtherChannel (LACP):</b> Link aggregation for increased bandwidth and redundancy.</li>
        <li><b>Spanning Tree Protocol (STP):</b> Loop prevention in the redundant switched network.</li>
      </ul>
    </td>
    <td valign="top" width="33%">
      <h4>Layer 3 Technologies</h4>
      <ul>
        <li><b>Inter-VLAN Routing:</b> SVI configuration on L3 switches for routing between VLANs.</li>
        <li><b>Static & Default Routing:</b> Precise control of traffic flow to and from the ASA firewall.</li>
        <li><b>EIGRP:</b> Dynamic routing for the WAN environment, including route redistribution.</li>
        <li><b>HSRP:</b> First Hop Redundancy Protocol for a highly available default gateway.</li>
      </ul>
    </td>
    <td valign="top" width="33%">
      <h4>Security & Services</h4>
      <ul>
        <li><b>ASA Firewall Policies:</b> Zone-based security using `nameif` and `security-level`.</li>
        <li><b>Access Control Lists (ACLs):</b> Granular traffic filtering between zones.</li>
        <li><b>Stateful Inspection:</b> `global_policy` inspection for protocols like ICMP, DNS, HTTP.</li>
        <li><b>DHCP Relay:</b> `ip helper-address` to centralize DHCP services.</li>
        <li><b>SSH Management:</b> Secure remote access configured on network devices.</li>
      </ul>
    </td>
  </tr>
</table>

---

## ► How to Run This Simulation

1.  **Download:** Clone this repository or download the `.pkt` file.
2.  **Software:** Open the file using **Cisco Packet Tracer version 8.x or higher**.
3.  **Explore:** Access the CLI of key devices (`CoreSW`, `ASA0`, `Router0`) to review the detailed configurations.
4.  **Test Connectivity:**
    - **Internal:** Ping from a PC in VLAN 10 to a PC in VLAN 20.
    - **To DMZ:** Use the Web Browser on an internal PC to access the Web Server at `http://192.168.100.10`.
    - **Across WAN:** Ping from an internal PC (e.g., PC0) to the remote PC (`PC5` at `192.168.200.10`).

---

*"This project was created as a practice exercise to strengthen my networking skills in preparation for the CCNA certification. As such, it may contain certain limitations or inaccuracies and should be considered for reference purposes only."*
