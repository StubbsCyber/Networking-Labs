# 🧪 Lab: DHCP Router — Using a Cisco Router as a DHCP Server

This lab demonstrates how to configure a Cisco router to provide DHCP services to multiple networks.  
Instead of using a dedicated DHCP server, the router assigns IPv4 addresses dynamically to end devices based on the configured DHCP pools.

You will configure DHCP pools, exclude IP addresses, verify DHCP bindings, and test connectivity.

---

## 🎯 Purpose

This lab teaches:

- How a router can act as a DHCP server
- How to create DHCP pools for different VLANs or networks
- How to exclude IPs from the DHCP pool
- How DHCP leases work and how clients obtain addresses
- How to verify DHCP configuration using CLI commands

You will practice:

- Creating DHCP address pools  
- Excluding IP ranges  
- Assigning default gateway + DNS  
- Verifying DHCP bindings  
- Using end devices to obtain dynamic addressing  
- Ping testing across networks

---

## 🗺️ Topology

Your exact topology screenshot should be inserted here:

```
![Topology](Screenshots/Topology.png)
```

The topology includes:

- 1 Cisco router acting as a DHCP server  
- 1 or more switches  
- Multiple PCs receiving DHCP  
- Several networks (ex: 10.1.1.0/24, 10.1.2.0/24, etc.)  
- No external DHCP server

---

## ⚙️ Configuration Steps

Below are the commands used to configure the router as a DHCP server.

---

### **1️⃣ Exclude DHCP Reserved IPs**

```
Router(config)# ip dhcp excluded-address 10.1.1.1 10.1.1.10
Router(config)# ip dhcp excluded-address 10.1.2.1 10.1.2.10
```

Replace the IPs based on your topology as needed.

---

### **2️⃣ Create DHCP Pools**

#### **Pool for Network 10.1.1.0/24**
```
Router(config)# ip dhcp pool SALES
Router(dhcp-config)# network 10.1.1.0 255.255.255.0
Router(dhcp-config)# default-router 10.1.1.1
Router(dhcp-config)# dns-server 8.8.8.8
```

#### **Pool for Network 10.1.2.0/24**
```
Router(config)# ip dhcp pool FINANCE
Router(dhcp-config)# network 10.1.2.0 255.255.255.0
Router(dhcp-config)# default-router 10.1.2.1
Router(dhcp-config)# dns-server 8.8.8.8
```

(Use your pool names + networks from Packet Tracer.)

---

### **3️⃣ Configure Router Interfaces for Each Network**

Example:

```
Router(config)# interface g0/0
Router(config-if)# ip address 10.1.1.1 255.255.255.0
Router(config-if)# no shutdown

Router(config)# interface g0/1
Router(config-if)# ip address 10.1.2.1 255.255.255.0
Router(config-if)# no shutdown
```

---

## 🖥️ Screenshots to Include (place in `/Screenshots` folder)

These filenames MUST match your folder:

```
Screenshots/Topology.png
Screenshots/DHCP_Router_Config.png
Screenshots/PC_IP_DHCP.png
Screenshots/Ping_Test.png
```

### Required screenshots:

### ✔️ 1. Topology  
Your Packet Tracer workspace screenshot.

### ✔️ 2. Router DHCP Configuration  
From CLI **show run | section dhcp**  
Or GUI if your lab uses GUI.

### ✔️ 3. DHCP Client Address Assignment  
On each PC:

Desktop → IP Configuration → DHCP (showing the obtained IPv4)

### ✔️ 4. Ping Test  
PC attempting to ping a device in another network (or default gateway).

---

## 🔍 Verification Commands

Use these to confirm DHCP operation:

```
Router# show ip dhcp binding
Router# show ip dhcp pool
Router# show running-config
```

---

## 🧪 Testing

On each PC:

1. Go to Desktop → IP Configuration  
2. Select “DHCP”  
3. Verify:
   - IPv4 Address  
   - Subnet Mask  
   - Default Gateway  
   - DNS  

Then:

```
PC> ping 10.1.1.1
PC> ping 10.1.2.50
PC> ping 8.8.8.8   (optional)
```

All pings should succeed if routing is correct.

---

## 📦 Files Included in This Folder

```
Stubbs-DHCP_Router_Fall_25_A.pka
README.md
/Screenshots
    Topology.png
    DHCP_Router_Config.png
    PC_IP_DHCP.png
    Ping_Test.png
    placeholder.txt
```

---

## ✅ Completion Checklist

- [x] DHCP pools configured  
- [x] Excluded addresses added  
- [x] Router interfaces up  
- [x] PCs obtaining IP via DHCP  
- [x] Screenshot folder created  
- [x] README added  
- [x] Packet Tracer file uploaded  

---

### ✔️ Lab Complete!
You now have a fully documented DHCP Router lab ready for your networking portfolio.
