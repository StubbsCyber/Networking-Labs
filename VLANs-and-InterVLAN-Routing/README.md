# Lab: Configuring VLANs

This lab demonstrates how to create VLANs, assign switchports to VLANs, and verify VLAN segmentation in a small multi-department network using Cisco Packet Tracer.

---

## 📌 Purpose

Virtual LANs (VLANs) segment a physical switch into multiple logical networks, improving:

- **Security** (traffic separation)
- **Broadcast domain reduction**
- **Network organization** (by department or function)

This lab focuses on:

- Creating VLANs  
- Assigning ports to VLANs  
- Verifying segmentation using CLI commands  
- Testing communication within and across VLANs  

---

## 📁 Topology

The network consists of:

- 1 Cisco switch  
- 2 devices in the **Development** VLAN  
- 2 devices in the **Marketing** VLAN  
- No trunking / no inter-VLAN routing in this lab  

![Topology](Screenshots/Config_VLAN_Topology.png)

---

## 🛠️ Configuration Steps

### **1. Create VLANs**

```text
vlan 10
 name DEVELOPMENT
vlan 20
 name MARKETING

