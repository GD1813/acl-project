# ACL Project (Standard to Extended ACL Upgrade) - Cisco Packet Tracer

## 📌 Project Overview
This project demonstrates the implementation and upgrade of Access Control Lists (ACLs) in Cisco Packet Tracer.

In Version 1, a Standard ACL is used to filter traffic based only on the source IP address.  
In Version 2, the project is upgraded to an Extended ACL, which filters traffic based on source IP address, destination IP address, and protocol type.

The upgraded Extended ACL blocks ICMP (Ping) traffic from PC0 to PC1 while allowing all other traffic.

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
- Configure a Standard ACL using source IP filtering  
- Upgrade from Standard ACL to Extended ACL  
- Block ICMP (Ping) traffic from PC0 to PC1 using Extended ACL  
- Allow all other traffic  
- Understand the difference between Standard and Extended ACLs  

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
- Enabled router interfaces using `no shutdown`  

### 2. PC Configuration
- Assigned IP addresses to PCs  
- Configured default gateways  

### 3. Connectivity Verification
- Verified communication between PC0 and PC1 using ping before applying ACL  

### 4. Standard ACL Configuration (Version 1)
- Created a Standard ACL to deny traffic from PC0 based on source IP address  
- Applied the Standard ACL inbound on router interface g0/0  

### 5. Extended ACL Upgrade (Version 2)
- Removed the previous Standard ACL  
- Created an Extended ACL to deny ICMP traffic from PC0 to PC1  
- Allowed all remaining traffic using `permit ip any any`  

### 6. ACL Application
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
```

---

### 🔹 Standard ACL Configuration (Version 1)

```bash
access-list 10 deny host 192.168.10.2
access-list 10 permit any
```

### 🔹 Apply Standard ACL to Interface

```bash
interface g0/0
ip access-group 10 in
exit
```

---

### 🔹 Remove Standard ACL Before Upgrade

```bash
interface g0/0
no ip access-group 10 in
exit

no access-list 10
```

---

### 🔹 Extended ACL Configuration (Version 2)

```bash
access-list 100 deny icmp host 192.168.10.2 host 192.168.20.2
access-list 100 permit ip any any
```

### 🔹 Apply Extended ACL to Interface

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

### Verify Running Configuration

```bash
show running-config
```

---

## ✅ Testing & Verification

### Before ACL
- PC0 successfully pinged PC1  

### After Standard ACL
- Traffic from PC0 was blocked based on source IP address  
- Standard ACL filtering was verified using `show access-lists`  

### After Extended ACL Upgrade
- PC0 could not ping PC1  
- ICMP traffic was blocked successfully  
- Remaining IP traffic was allowed using `permit ip any any`  
- ACL rules were verified using `show access-lists`  
- ACL placement was verified using `show ip interface g0/0`  

---

## 🧠 Skills Learned
- Difference between Standard ACL and Extended ACL  
- Standard ACL configuration  
- Extended ACL configuration  
- Source IP-based filtering  
- Source and destination IP-based filtering  
- Protocol-based access control  
- ICMP traffic filtering  
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
This project demonstrates the upgrade from Standard ACL to Extended ACL in Cisco Packet Tracer.

The Standard ACL version helped in understanding basic source IP-based filtering. The upgraded Extended ACL version provided more precise traffic control by blocking ICMP traffic from PC0 to PC1 while allowing all other traffic.

Through this project, I gained practical understanding of ACL configuration, traffic filtering, protocol-based access control, and basic network security implementation.
