# ACL Project (Standard ACL) - Cisco Packet Tracer

## 📌 Project Overview
This project demonstrates how to configure a Standard Access Control List (ACL) in Cisco Packet Tracer to control network traffic between two networks.

The ACL is configured on the router to block traffic from a specific PC while allowing all other traffic. This project helps in understanding how ACLs improve network security by filtering packets based on source IP addresses.

---

## 🧱 Network Design
- 1 Router  
- 2 Switches  
- 2 PCs  

### 📡 Connections
- PC1 → Switch1  
- Switch1 → Router (g00)  
- Router (g01) → Switch2  
- Switch2 → PC2  

---

## 🖼️ Packet Tracer Topology Diagram

```text
![Topology](images/topology.png)
```

---

## 🎯 Project Goal
- Allow normal communication initially  
- Configure Standard ACL to block PC1 traffic  
- Prevent PC1 from accessing Network 192.168.20.024  
- Allow all other traffic  

---

## 🖥️ IP Addressing

### PC1
- IP Address 192.168.10.2  
- Subnet Mask 255.255.255.0  
- Default Gateway 192.168.10.1  

### Router

#### g00
- IP Address 192.168.10.1  
- Subnet Mask 255.255.255.0  

#### g01
- IP Address 192.168.20.1  
- Subnet Mask 255.255.255.0  

### PC2
- IP Address 192.168.20.2  
- Subnet Mask 255.255.255.0  
- Default Gateway 192.168.20.1  

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

### 4. Standard ACL Configuration
- Created ACL to deny traffic from PC1  
- Allowed all remaining traffic using `permit any`  

### 5. ACL Application
- Applied ACL inbound on router interface g00  

---

## 💻 CLI Configuration

### 🔹 Router Interface Configuration
```bash
enable
configure terminal

interface g00
ip address 192.168.10.1 255.255.255.0
no shutdown
exit

interface g01
ip address 192.168.20.1 255.255.255.0
no shutdown
exit
```

### 🔹 Standard ACL Configuration
```bash
access-list 10 deny host 192.168.10.2
access-list 10 permit any
```

### 🔹 Apply ACL to Interface
```bash
interface g00
ip access-group 10 in
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

### Verify ACL
```bash
show access-lists
```

### Verify Interface ACL
```bash
show ip interface g00
```

---

## ✅ Testing & Verification
- Verified successful communication before ACL configuration  
- Confirmed ACL blocked traffic from PC1  
- Verified ACL rules using `show access-lists`  
- Confirmed only specified traffic was denied  
- Tested network connectivity after ACL application  

---

## 🧠 Skills Learned
- Standard ACL configuration  
- Packet filtering using source IP  
- Permit and deny statements  
- ACL placement (Inbound)  
- Network traffic control  
- Basic network security implementation  
- Troubleshooting ACL behavior  

---

## 📂 Project Files
- acl-standard-project.pkt  
- imagestopology.png  

---

## 📌 Conclusion
This project demonstrates how Standard ACLs are used to filter network traffic and improve network security. By configuring ACL rules on a router, traffic from a specific source device was successfully blocked while allowing all other communication. This project provided practical understanding of packet filtering and access control in networking