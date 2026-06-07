# ACL Project (Standard to Extended ACL Upgrade) - Cisco Packet Tracer

## 📌 Project Overview
This project demonstrates the upgrade from a **Standard Access Control List (ACL)** to an **Extended Access Control List (ACL)** in Cisco Packet Tracer.

In the first version, a Standard ACL was used to filter traffic based only on the source IP address. In this upgraded version, an Extended ACL is used to block ICMP (Ping) traffic from a specific source device to a specific destination device while allowing all other traffic.

This project helps in understanding how Extended ACLs provide more control by filtering traffic based on source IP address, destination IP address, and protocol type.

---

## 🧱 Network Design
- 1 Router  
- 2 Switches  
- 2 PCs  

### 📡 Connections
- PC0 → Switch0  
- Switch0 → Router (g0/0)  
- Router (g0/1) → Switch1  
- Switch1 → PC1  

---

## 🖼️ Packet Tracer Topology Diagram

![Topology](images/topology.png)

---

## 🎯 Project Goal
- Verify normal communication before applying ACL  
- Upgrade from Standard ACL to Extended ACL  
- Block ICMP (Ping) traffic from PC0 to PC1  
- Allow all other traffic  
- Understand protocol-based traffic filtering  

---

## 🖥️ IP Addressing

### PC0
- IP Address: 192.168.10.2  
- Subnet Mask: 255.255.255.0  
- Default Gateway: 192.168.10.1  

### Router

#### g0/0
- IP Address: 192.168.10.1  
- Subnet Mask: 255.255.255.0  

#### g0/1
- IP Address: 192.168.20.1  
- Subnet Mask: 255.255.255.0  

### PC1
- IP Address: 192.168.20.2  
- Subnet Mask: 255.255.255.0  
- Default Gateway: 192.168.20.1  

---

## ⚙️ Configuration Steps

### 1. Router Interface Configuration
- Assigned IP addresses to router interfaces  
- Enabled interfaces using `no shutdown`  

### 2. PC Configuration
- Assigned IP addresses to PCs  
- Configured default gateways  

### 3. Connectivity Verification
- Verified communication using ping before ACL configuration  

### 4. Extended ACL Configuration
- Created an Extended ACL to deny ICMP traffic from PC0 to PC1  
- Allowed all remaining traffic using `permit ip any any`  

### 5. ACL Application
- Applied the Extended ACL inbound on router interface g0/0, close to the source network  

---

## 💻 CLI Configuration

### 🔹 Router Interface Configuration
```bash
enable
configure terminal

interface g0/0
ip address 192.168.10.1 255.255.255.0
no shutdown
exit

interface g0/1
ip address 192.168.20.1 255.255.255.0
no shutdown
exit

### 🔹 Extended ACL Configuration

```bash
access-list 100 deny icmp host 192.168.10.2 host 192.168.20.2
access-list 100 permit ip any any
```

### 🔹 Apply ACL to Interface

```bash
interface g0/0
ip access-group 100 in
exit

end
write memory
```

---

## 🔍 Verification Commands

### Check Connectivity Before ACL

```bash
ping 192.168.20.2
```

### Verify ACL Rules

```bash
show access-lists
```

### Verify ACL Applied on Interface

```bash
show ip interface g0/0
```

---

## ✅ Testing & Verification

### Before ACL

- PC0 successfully pinged PC1  

### After Extended ACL

- PC0 could not ping PC1  
- ICMP traffic was blocked successfully  
- Other traffic was allowed using `permit ip any any`  
- ACL rules were verified using `show access-lists`  
- ACL placement was verified using `show ip interface g0/0`  

---

## 🧠 Skills Learned

- Difference between Standard ACL and Extended ACL  
- Extended ACL configuration  
- ICMP traffic filtering  
- Source and destination IP-based filtering  
- Protocol-based access control  
- ACL placement close to the source  
- Network traffic control and troubleshooting  

---

## 🔄 Project Evolution

- Version 1: Standard ACL using source IP filtering  
- Version 2: Extended ACL using source IP, destination IP, and protocol filtering  

---

## 📂 Project Files

- acl-standard-project.pkt  
- acl-extended-project.pkt  
- images/topology.png  

---

## 📌 Conclusion

This project demonstrates the upgrade from Standard ACL to Extended ACL in Cisco Packet Tracer. The Extended ACL was used to block ICMP traffic from PC0 to PC1 while allowing all other traffic.

Through this project, I understood how Extended ACLs provide more precise control than Standard ACLs by filtering traffic based on source IP address, destination IP address, and protocol type. This project helped build practical knowledge of traffic filtering and basic network security.
