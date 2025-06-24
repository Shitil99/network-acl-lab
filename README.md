# 🔒 Advanced Network ACL Configuration (Cisco Packet Tracer Lab)

This project demonstrates the configuration of **Extended Access Control Lists (ACLs)** in a simulated enterprise network using **Cisco Packet Tracer**. The lab enforces selective traffic filtering based on IP addresses, protocols (e.g., Telnet, TFTP, HTTP), and security policies. The goal is to simulate how real-world organizations control internal and external access to services using router-based ACLs.

---

## 📁 Project Files

| File                         | Description                                 |
|------------------------------|---------------------------------------------|
| `network-acl-lab.pkt`        | Cisco Packet Tracer file with full topology |
| `project-report.pdf`         | Detailed report with IPs, ACL configs       |
| `diagrams/acl-topology.png`  | Network topology image                      |

---

## 🧠 Objective

Design and configure a routed network to:
- Implement **extended ACLs** for filtering traffic
- Allow/deny based on **source/destination IPs and ports**
- Secure access to internal servers
- Block unauthorized access from external users

---

## 🖥️ Network Topology

The lab topology includes:
- 3 routers (R1, R2, R3)
- 1 ISP router
- 4 internal PCs (PC1–PC4)
- 2 servers: Web/TFTP Server and Public Web Server
- 1 external host (simulated attacker)

![Network ACL Topology](diagrams/acl-topology.png)

---

## 🌐 IP Addressing Summary (Sample)

| Device              | Interface   | IP Address        | Subnet Mask       |
|---------------------|-------------|-------------------|-------------------|
| R1                  | Fa0/0       | 192.168.10.1      | 255.255.255.0     |
| R2                  | Fa0/0       | 192.168.20.1      | 255.255.255.0     |
| R3                  | Fa0/0       | 192.168.30.1      | 255.255.255.0     |
| PC1                 | NIC         | 192.168.10.10     | 255.255.255.0     |
| WEB/TFTP Server     | NIC         | 192.168.20.254    | 255.255.255.0     |
| WEB Server          | NIC         | 209.165.201.30    | 255.255.255.224   |
| Outside Host        | NIC         | 209.165.202.158   | 255.255.255.224   |

---

## 🔧 ACL Requirements & Configuration

### ✅ Task 1: Routing & Connectivity
- Configured **EIGRP** between all routers
- Verified full reachability using `ping` and routing tables

---

### 🚫 Task 2: Block Telnet from 192.168.10.0/24
```bash
access-list 100 deny tcp 192.168.10.0 0.0.0.255 any eq 23
access-list 100 permit ip any any

```

### 🔐 Task 3: Allow TFTP and HTTP from 192.168.30.0/24
```bash
access-list 110 permit udp 192.168.30.0 0.0.0.255 host 192.168.20.254 eq 69
access-list 110 permit tcp 192.168.30.0 0.0.0.255 host 209.165.201.30 eq 80
access-list 110 deny ip 192.168.30.0 0.0.0.255 any

```

### 🌐 Task 4: Allow Web Access from Outside Host Only
```bash
access-list 120 permit tcp host 209.165.202.156 host 209.165.201.30 eq 80
access-list 120 deny ip host 209.165.202.156 any

```

## 🧪 Tools & Skills Demonstrated
-Cisco Packet Tracer
-Extended ACL syntax and placement
-IP subnetting and interface configuration
-Dynamic routing with EIGRP
-Simulating traffic and validation with ping & telnet

## ✅ Outcome
-This project successfully showcases how to:
-Enforce traffic segmentation
-Restrict service-level access
-Implement firewall-like policies using router ACLs
-It replicates core functions of perimeter firewalls, useful in both small enterprise and academic networks.
